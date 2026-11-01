# StrataScratch Question ID: 2059 - Player With Longest Streak

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2059` |
| **Title** | **Player With Longest Streak** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2059) |

---

## 1. Problem Description

You are given a table of tennis players and their matches that they could either win (W) or lose (L). Find the longest streak of wins. A streak is a set of consecutive won matches of one player. The streak ends once a player loses their next match. Output the ID of the player or players and the length of the streak.

---

## 2. Input Tables & Schema

```text
<players_results>
player_id           int
match_date          datetime
match_result        varchar
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
# -- logic:
-- 1. combined all results into a single string
-- 2. break string into individual streaks delimited by 'L' (only keep track of consecutive wins)
-- 3. break strings in array into individual rows
-- 4. replace all agg delimiter into ''
-- 5. count the number of Ws for each valid winning streak
-- 6. rank each streak by the player
-- 7. select top ranked streak

WITH result_seqs AS (
    SELECT player_id,
           STRING_AGG(match_result, ',') AS result_seq
    FROM players_results
    GROUP BY player_id
),

retrieve_w AS (
    SELECT player_id,
           LENGTH(REPLACE(result_seq, ',', '')) AS winning_streak
    FROM (
        SELECT player_id,
               UNNEST(STRING_TO_ARRAY(result_seq, 'L')) AS result_seq
        FROM result_seqs
        ) AS retrieve_w_only
)

SELECT player_id,
       winning_streak
FROM (
    SELECT player_id,
           winning_streak,
           RANK() OVER(ORDER BY winning_streak DESC) AS streak_rank
    FROM retrieve_w
) rank_w_streak
WHERE streak_rank = 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2059").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic:
-- 1. combined all results into a single string
-- 2. break string into individual streaks delimited by 'L' (only keep track of consecutive wins)
-- 3. break strings in array into individual rows
-- 4. replace all agg delimiter into ''
-- 5. count the number of Ws for each valid winning streak
-- 6. rank each streak by the player
-- 7. select top ranked streak

WITH result_seqs AS (
    SELECT player_id,
           STRING_AGG(match_result, ',') AS result_seq
    FROM players_results
    GROUP BY player_id
),

retrieve_w AS (
    SELECT player_id,
           LENGTH(REPLACE(result_seq, ',', '')) AS winning_streak
    FROM (
        SELECT player_id,
               UNNEST(STRING_TO_ARRAY(result_seq, 'L')) AS result_seq
        FROM result_seqs
        ) AS retrieve_w_only
)

SELECT player_id,
       winning_streak
FROM (
    SELECT player_id,
           winning_streak,
           RANK() OVER(ORDER BY winning_streak DESC) AS streak_rank
    FROM retrieve_w
) rank_w_streak
WHERE streak_rank = 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
