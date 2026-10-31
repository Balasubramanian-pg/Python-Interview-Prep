# StrataScratch Question ID: 2125 - Process A Refund

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2125` |
| **Title** | **Process A Refund** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2125) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Process a Refund.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2125.
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

# we filter required accounts as per our requirement.
filtered_noom_signups = noom_signups.filter(F.col("started_at") >= "2019-01-01")

# now we need to join filtered_noom_signups and noom_transactions.so we perform inner join and keep only relatable data
filtered_signups_transactions = filtered_noom_signups.join(
    noom_transactions,
    "signup_id",
    "inner"
    )
    
# here we need to do filtered_signups_transactions join with noom_plans, because key factor in our solution is done by "billing_cycle_in_months" so we need to do join.

full_joined_df = filtered_signups_transactions.join(
    noom_plans,
    "plan_id",
    "inner"
    )
    
    
# we calculate refund days at below for every row in full_joined_df
refund_days_df = full_joined_df.withColumn("refund_days",F.datediff(F.col("refunded_at"), F.col("settled_at")))

    
# so now we perform group_by and aggreation here for our final answer.
final_df = refund_days_df.groupBy("billing_cycle_in_months").agg(
    F.min("refund_days").alias("min_days"),
    F.avg("refund_days").alias("avg_days"),
    F.max("refund_days").alias("max_days")
    ).orderBy("billing_cycle_in_months")

final_df.explain(True)
# To validate your solution, convert your final pySpark df to a pandas df
final_df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2125").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2125\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
