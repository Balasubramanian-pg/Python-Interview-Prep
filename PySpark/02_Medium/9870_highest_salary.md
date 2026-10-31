# StrataScratch Question ID: 9870 - Highest Salary

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9870` |
| **Title** | **Highest Salary** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9870) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Highest Salary.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9870.
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
from pyspark.sql import functions as F

# here we find out highest salary using max aggregation function.
max_salary = worker.agg(F.max("salary").alias("max_salary")).collect()[0]['max_salary']

# now Filter employees with max salary
final_df = worker.filter(F.col("salary") == max_salary).select("first_name","salary")

# To validate your solution, convert your final pySpar