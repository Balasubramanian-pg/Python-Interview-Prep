# StrataScratch Question ID: 10161 - Ranking Hosts By Beds

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10161` |
| **Title** | **Ranking Hosts By Beds** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10161) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Ranking Hosts By Beds.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10161.
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
from pyspark.sql.window import Window 

# here count bed host_wise 
beds_per_count = airbnb_apartments.groupBy("host_id").agg(F.sum('n_beds').alias('bed_counts'))

# Create window for rank 
window_spec = Window.orderBy(F.col('bed_counts').desc())

# final result as per bussiness requirements.
final_df = beds_per_count.select(
    "host_id",
    "bed_counts",
    F.dense_rank().over(window_spec).alias('rank')
    )
