# StrataScratch Question ID: 9762 - Find The Day Of The Week That Most People Check In

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9762` |
| **Title** | **Find The Day Of The Week That Most People Check In** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9762) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the day of the week that most people check in.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9762.
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

# here we find out particular day as per date.
day_list_df = airbnb_contacts.withColumn(
    "week_days",
    F.date_format(F.col("ds_checkin"), 'UUUU')
)


# final output
final_count_df = (
    day_list_df
    .groupBy("week_days")
    .agg(F.count('*') .alias ("check-in count"))
    .orderBy(F.desc('check-in count'))
)
# To validate your solution, convert your final pySpark df to a pandas df
final_count_df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9762").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 9762\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
