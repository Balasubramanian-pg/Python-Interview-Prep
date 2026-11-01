# StrataScratch Question ID: 9669 - Count The Number Of Speakers Per Each Language

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9669` |
| **Title** | **Count The Number Of Speakers Per Each Language** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9669) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Number_of_Speakers _By_Language.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9669.
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
from pyspark.sql import functions as f

# we take only required things from fact table to reduce load on clusters memory.
event_details = playbook_events.select('user_id','location')

# insted of sort-merge we use broadcast join, because our dim table is very samll. and using broadcast helps to reduce shuffling 
playbook_events = (
    event_details.join(f.broadcast(playbook_users),on = 'user_id', how = 'inner').
    groupBy(f.col('location').alias('country'),'language').
    agg(f.countDistinct("user_id").alias("n_speakers"))
    .orderBy('country')
    )
# To validate your solution, convert your final pySpark df to a pandas df
playbook_events.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9669").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 9669\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
