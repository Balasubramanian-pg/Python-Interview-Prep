# StrataScratch Question ID: 2039 - Products Report Summary

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2039` |
| **Title** | **Products Report Summary** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2039) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Products Report Summary.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2039.
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
import pyspark
from pyspark.sql import functions as s 

# Start writing code
wfm_transactions = wfm_transactions.join(
    wfm_products, wfm_transactions.product_id == wfm_products.product_id
).groupBy("product_category").agg(
    s.count_distinct("customer_id").alias("customers")
).sort(s.col("customers").desc())
# count_distinct: The "Loyalty" check. If one person bought 10 items,
# count_distinct only c