# StrataScratch Question ID: 10324 - Distances Traveled

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10324` |
| **Title** | **Distances Traveled** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Lyft** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10324) |

---

## 1. Problem Description

Find the top 10 users that have traveled the greatest distance. Output their id, name and a total distance traveled.

---

## 2. Input Tables & Schema

```text
<lyft_rides_log>
id              int
user_id         int
distance        int

<lyft_users>
id              int
name            varchar
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
from pyspark.sql.window import Window

# Execute solution using Spark SQL or DataFrame API:
# spark.sql('''
# -- logic: we need find the user and their total distance travelled (sum)
-- group by on a user level
-- assumption: since we are not looking at a value, there might be a tie-breaker that we need to take care of
-- dense_rank() might be a good option

-- we need the id, name and total distance
SELECT lu.id, lu.name, user_distance.traveled_distance
FROM (
    -- this calculates the total travelled distance and compute the ranks of user based on their travelled distance
    SELECT user_id,
           SUM(distance) as traveled_distance,
           DENSE_RANK() OVER (ORDER BY SUM(distance) DESC) AS rank
    FROM lyft_rides_log
    GROUP BY user_id
) AS user_distance
JOIN lyft_users lu
    ON user_distance.user_id = lu.id
-- filter by ranking only top 10
ORDER BY user_distance.traveled_distance DESC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10324").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic: we need find the user and their total distance travelled (sum)
-- group by on a user level
-- assumption: since we are not looking at a value, there might be a tie-breaker that we need to take care of
-- dense_rank() might be a good option

-- we need the id, name and total distance
SELECT lu.id, lu.name, user_distance.traveled_distance
FROM (
    -- this calculates the total travelled distance and compute the ranks of user based on their travelled distance
    SELECT user_id,
           SUM(distance) as traveled_distance,
           DENSE_RANK() OVER (ORDER BY SUM(distance) DESC) AS rank
    FROM lyft_rides_log
    GROUP BY user_id
) AS user_distance
JOIN lyft_users lu
    ON user_distance.user_id = lu.id
-- filter by ranking only top 10
ORDER BY user_distance.traveled_distance DESC
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
