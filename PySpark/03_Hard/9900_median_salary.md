# StrataScratch Question ID: 9900 - Median Salary

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9900` |
| **Title** | **Median Salary** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9900) |

---

## 1. Problem Description

Find the median employee salary of each department.
Output the department name along with the corresponding salary rounded to the nearest whole dollar.

---

## 2. Input Tables & Schema

```text
employee
id                  int
first_name          varchar
last_name           varchar
age                 int
sex                 varchar
employee_title      varchar
department          varchar
salary              int
target              int
bonus               int
email               varchar
city                varchar
address             varchar
manager_id          int
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
-- find median salary aggregated by department

-- logic:
-- PERCENTILE_CONT(0.5) for all salary per department
-- ROUND(median salary)

-- output:
-- department, median salary

SELECT department,
       PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY s