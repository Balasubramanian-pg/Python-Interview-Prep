# StrataScratch Question ID: 2060 - Manager Of The Largest Department

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2060` |
| **Title** | **Manager Of The Largest Department** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2060) |

---

## 1. Problem Description

Given a list of a company's employees, find the name of the manager from the largest department. Output their first and last name.

Table:
<az_employees>
id                  int
first_name          varchar
last_name           varchar
department_id       int
department_name     varchar
position            varchar

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2060.
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
# -- logic: count employees per department, filter for manager
-- assumption: manager is counted as one of the employee, manager can be either 'Manager' or 'Interim Manager'

-- filter for top-ranked department and select manager name
SELECT az.first_name, az.last_name
FROM (
    -- rank department by employee count
    SELECT department_id,
           employee_count,
           DENSE_RANK() OVER (ORDER BY employee_count DESC) AS rank
    FROM (
        SELECT department_id,
        COUNT(*) AS employee_count
        FROM az_employees
        GROUP BY department_id
    ) no_employees_by_department
) employee_count_rank
JOIN az_employees az
ON az.department_id = employee_count_rank.department_id
-- filter for top rank department and either manager position
WHERE employee_count_rank.rank = 1 AND az.position ILIKE '%manager%';
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.app