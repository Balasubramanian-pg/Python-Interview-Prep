# StrataScratch Question ID: 9845 - April Admin Employees

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9845` |
| **Title** | **April Admin Employees** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9845) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: April Admin Employees.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9845.
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

# Start writing code
worker = worker.filter(F.col('department') == 'Admin').filter(F.month(F.col('joining_date')) >= 4).agg(F.count(F.col('worker_id')))

# To validate your solution, convert your final pySpark df to a pandas df
worker.toP