# StrataScratch Question ID: 9712 - Find The First And Last Times The Maximum Score Was Awarded

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9712` |
| **Title** | **Find The First And Last Times The Maximum Score Was Awarded** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9712) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the first and last times the maximum score was awarded.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9712.
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

# now we wants to check highest score 
high_score = los_angeles_restaurant_health_inspections.agg(
    F.max("score").alias('max_score')
    ).collect()[0]['max_score']

# we filter data as per max score 
filtered_df = los_angeles_restaurant_health_inspections.filter(
    F.col('score') == high_score
    )
    
# final df get first and last date of max score 
final_df = filtered_df.agg(
    F.min("activity_date").alias("first_time"),
    F.max('activity_date').alias("last_time")
    )

# To validate your solution, convert your final pySpark df to a pandas df
los_angeles_restaurant_health_inspections.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9712").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 9712\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
