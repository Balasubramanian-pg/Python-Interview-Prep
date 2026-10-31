# StrataScratch Question ID: 10322 - Finding User Purchases

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10322` |
| **Title** | **Finding User Purchases** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Amazon** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10322) |

---

## 1. Problem Description

Write a query that'll identify returning active users. 
A returning active user is a user that has made a second purchase within 7 days of any other of their purchases. Output a list of user_ids of these returning active users.

---

## 2. Input Tables & Schema

```text
<amazon_transactions>
id                      int
user_id                 int
item                    varchar
created_at              datetime
revenue                 int
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
from pyspark.sql.functions import *
from pyspark.sql import *
# Start writing code
# amazon_transactions.show(50,truncate=False)
df=amazon_transactions
window_spec = Window.partitionBy(col("user_id")).orderBy(col("created_at"))
df=df.withColumn("flag",datediff(col("created_at"),lag(col("created_at")).over(window_spec)))
df=df.filter(col("flag")<=7).select("user_id").distinct()
# df.show(50,truncate=False)
df.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# amazon_transactions.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10322").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- we need identify RETURNING ACTIVE USERS
-- RETURNING: make a 2nd purchase within 7 days

-- we only need user_id
SELECT DISTINCT(p.user_id)
FROM amazon_transactions p
JOIN amazon_transactions n
    ON p.user_id = n.user_id
    -- we do not need compare two same purchase
WHERE p.id <> n.id
    -- calculate the difference between two purchase dates
    AND DATEDIFF(n.created_at, p.created_at) BETWEEN 0 AND 7
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
