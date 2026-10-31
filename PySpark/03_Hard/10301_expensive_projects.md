# StrataScratch Question ID: 10301 - Expensive Projects

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10301` |
| **Title** | **Expensive Projects** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Microsoft** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10301) |

---

## 1. Problem Description

Given a list of projects and employees mapped to each project, calculate by the amount of project budget allocated to each employee . The output should include the project title and the project budget per employee as an integer. Order your list by projects with the highest budget per employee first.

---

## 2. Input Tables & Schema

```text
<ms_projects>
id                  int
title               varchar
budget              int

<ms_emp_projects>
emp_id              int
project_id          int
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
-- calculate the amount of budget to each employee

-- assumption:
-- one employee may have multiple project budgets

-- output:
-- project title, project budget per employee

-- logic:
-- count number of employee per budget
-- compute budget / no. employees
-- order budget/employee DESC

-- calculate the budget/employee
SELECT title,
       budget/no_employees::integer budget_per_emp
FROM (
    -- join the two tables first
    -- this will result in duplicates
    SELECT DISTINCT title,
           budget,
           -- find the total employee per project
           COUNT(*) OVER(PARTITION BY title) no_employees
    FROM ms_projects
    JOIN ms_emp_projects
        ON ms_projects.id = ms_emp_projects.project_id
) budget_emps
-- sort them by desc order
ORDER BY 2 DESC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark =