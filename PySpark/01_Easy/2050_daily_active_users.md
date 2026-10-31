# StrataScratch Question ID: 2050 - Daily Active Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2050` |
| **Title** | **Daily Active Users** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2050) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Daily Active Users.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2050.
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

# we required only january data so we first filter required data.
sf_events = sf_events.filter((F.col('record_date') >= '2021-01-01') & (F.col('record_date') <= '2021-01-31'))

# here we take only distinct user day wise 
daily_active = sf_events.groupBy('record_date','account_id').agg(F.countDistinct('user_id').alias('daily_active_user'))

# we calculate average of daily active users
sf_events = daily_active.groupBy('account_id').agg(F.avg('daily_active_user').alias('avg_daily_active_users'))
# To validate your solution, convert your final pySpark df to a pandas df
sf_events.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2050").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2050\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
