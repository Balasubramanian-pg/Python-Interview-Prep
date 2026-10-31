# StrataScratch Question ID: 10299 - Finding Updated Records

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10299` |
| **Title** | **Finding Updated Records** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Microsoft** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10299) |

---

## 1. Problem Description

We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. 
Find the current salary of each employee assuming that salaries increase each year. 
Output their id, first name, last name, department ID, and current salary. 
Order your list by employee ID in ascending order.


ms_employee_salary

id:bigint
first_name:string
last_name:string
salary:bigint
department_id:bigint

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10299.
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
from pyspark.sql.window import Window
from pyspark.sql.functions import col,max, first
# Start writing code


window_spec = Window.partitionBy(col('id')).orderBy(col('salary').desc())
ms_employee_salary = ms_employee_salary.withColumn('current_salar