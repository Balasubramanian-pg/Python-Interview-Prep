# StrataScratch Question ID: 9847 - Workers By Department Since April

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9847` |
| **Title** | **Workers By Department Since April** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9847) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Workers by Department Since April.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9847.
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

# 1st we filter data on date .. then group it as per department and then count as per id.
worker =  worker.filter(F.col('joining_date')>= '2014-04-01').groupBy('department').agg(F.count('worker_id').alias('total_workers')).orderBy(F.col('total_workers').desc())

# To validate your solution, convert