# StrataScratch Question ID: 10304 - Risky Projects

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10304` |
| **Title** | **Risky Projects** |
| **Difficulty** | `Hard` |
| **Company Tag** | **LinkedIn** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10304) |

---

## 1. Problem Description

Solve the 'Risky Projects' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
<linkedin_projects>
id              int
title           varchar
budget          int
start_date      datetime
end_date        datetime

<linkedin_emp_projects>
emp_id          int
project_id      int

<linkedin_employees>
id              int
first_name      varchar
last_name       varchar
salary          int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations until final aggregations.

---

## 4. PySpark DataFrame API Solution

```python
# Import your libraries
import pyspark
from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Execute solution using Spark SQL or DataFrame API:
# spark.sql('''
# -- objective:
-- FIND projects that are at risk of overbudget
-- Overbudget: cost of all emps assigned  > budget of project

-- assumption:
-- not all projects are rated at 1 year, some are less than that
-- need to prorate (salary of emp (cost) must feedback pro-rated rate)
-- pro-rate is by days

-- logic:
-- LEFT JOIN emp_projects, employees ON projects
-- COMPUTE project duration in months
-- SUM(salary) GROUP BY projects.id
-- Pro-rate SUM(salary) based on projects.start_date, projects.end_date
-- ROUND(emp cost) to the next dollar amount

-- output:
-- project name, proj budget, prorated total employee expenses (rounded to next dollar amount)
SELECT project_title,
       project_budget,
       CEILING(emp_costs * (duration/365::float)) total_costs
FROM (
    SELECT title AS project_title,
          budget AS project_budget,
          duration,
          SUM(salary) AS emp_costs
    FROM (
        SELECT p.*,
              p.end_date - p.start_date AS duration,
              ep.emp_id,
              e.salary
        FROM linkedin_projects p
        LEFT JOIN linkedin_emp_projects ep
            ON p.id = ep.project_id
        JOIN linkedin_employees e
            ON ep.emp_id = e.id
    ) proj_infos
    GROUP BY 1, 2, 3
) costs
WHERE emp_costs * (duration/365::float) > project_budget
ORDER BY 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10304").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- FIND projects that are at 