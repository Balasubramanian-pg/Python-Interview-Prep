# StrataScratch Question ID: 2024 - Unique Users Per Client Per Month

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2024` |
| **Title** | **Unique Users Per Client Per Month** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2024) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Unique Users Per Client Per Month.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2024.
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
fact_events = fact_events.withColumn("month",F.month(F.col('time_id'))).groupBy('client_id','month').agg(F.countDistinct('user_id').alias('users_num'))
 
# To validate your solution, convert your final pySpark df to a pandas df
fact_events.toPandas()


# 1st we transfer month in integer format. then we group it by using client_id and month buckets, then major unique quantities from every bucket.
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2024").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2024\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
