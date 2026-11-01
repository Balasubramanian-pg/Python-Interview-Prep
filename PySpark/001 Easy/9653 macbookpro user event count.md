# StrataScratch Question ID: 9653 - Macbookpro User Event Count

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9653` |
| **Title** | **Macbookpro User Event Count** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9653) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: MacBookPro User Event Count.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9653.
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
from pyspark.sql import functions as F

# 1. THE CLEANUP (Standardize and Filter)
playbook_events = playbook_events.filter(
    F.lower(F.col("device")) == 'macbook pro'
)
# lower() kills case-sensitivity bugs.

# 2. THE BUCKETING (Group and Count)
playbook_events = playbook_events.groupBy("event_name").agg(
    F.count("*").alias("event_count")
).sort("event_name")
# groupBy: Creates a bucket for every unique action (login, home_page, etc.)
# agg: The "math mode" trigger. Tells Spark to start calculating.
# count("*"): Counts every single row sitting inside each bucket.


# 3. THE HANDOVER (Local Python)
playbook_events.toPandas()
#toPandas: Moves data from the massive cluster to a small local table.


# filter un-necessary data keep only "macbook pro" -> macbook users hav eenrolled in multiple events so we create event wise bucket using groupBy -> then count rows in every bucket -> after that we sort it with the name of event . -> then with the help of topanda() Moves data from the massive cluster to a small local table.
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9653").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 9653\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
