# StrataScratch Question ID: 2012 - Viewers Turned Streamers

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2012` |
| **Title** | **Viewers Turned Streamers** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2012) |

---

## 1. Problem Description

From users who had their first session as a viewer, how many streamer sessions have they had? Return the user id and number of sessions in descending order. In case there are users with the same number of sessions, order them by ascending user id.

---

## 2. Input Tables & Schema

```text
<twitch_sessions<
user_id                     int
session_start               datetime
session_end                 datetime
session_id                  int
session_type                varchar
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
# -- assumption:
-- data is clean
-- session_type is either 'viewer' or 'streamer'
-- each session must end first before another occurs, hence each row is a complete session by its own

-- logic:
-- rank each user's session by date (earliest is number 1)
-- filter for user whose first session_type = 'viewer'
-- count users with session_type = 'streamer'
-- order by num_session desc asc user id

-- count the number of session_type 'streamer'
-- if there is, means they turn into streamers
SELECT user_id,
       COUNT(*)
FROM twitch_sessions
WHERE user_id IN (
    -- we want to select the first event
    SELECT user_id
    FROM (
        -- ranking of sessions for users
        -- asc order of time
        SELECT user_id,
               session_type,
               RANK() OVER(PARTITION BY user_id ORDER BY session_start ASC) session_order
        FROM twitch_sessions
    ) session_orders
    -- filter user whose first session_type = 'viewer'
    WHERE session_order = 1
        AND session_type = 'viewer'
) AND session_type = 'streamer'
GROUP BY 1
-- order by asc user id
ORDER BY 2 DESC, 1 ASC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2012").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- assumption:
-- data is clean
-- session_type is either 'viewer' or 'streamer'
-- each session must end first before another occurs, hence each row is a complete session by its own

-- logic:
-- rank each user's session by date (earliest is number 1)
-- filter for user whose first session_type = 'viewer'
-- count users with session_type = 'streamer'
-- order by num_session desc asc user id

-- count the number of session_type 'streamer'
-- if there is, means they turn into streamers
SELECT user_id,
       COUNT(*)
FROM twitch_sessions
WHERE user_id IN (
    -- we want to select the first event
    SELECT user_id
    FROM (
        -- ranking of sessions for users
        -- asc order of time
        SELECT user_id,
               session_type,
               RANK() OVER(PARTITION BY user_id ORDER BY session_start ASC) session_order
        FROM twitch_sessions
    ) session_orders
    -- filter user whose first session_type = 'viewer'
    WHERE session_order = 1
        AND session_type = 'viewer'
) AND session_type = 'streamer'
GROUP BY 1
-- order by asc user id
ORDER BY 2 DESC, 1 ASC
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
