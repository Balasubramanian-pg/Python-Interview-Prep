# StrataScratch Question ID: 2019 - Top 2 Users With Most Calls

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2019` |
| **Title** | **Top 2 Users With Most Calls** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2019) |

---

## 1. Problem Description

Return the top 2 users in each company that called the most. Output the company_id, user_id, and the user's rank. If there are multiple users in the same rank, keep all of them.

---

## 2. Input Tables & Schema

```text
<rc_calls>
user_id     int
datedate    time
call_id     int

<rc_users>
user_id     int
status      varchar
company_id  int
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
# -- logic: we need top 2 users that called the most
-- need: a ranking of users, ranking keeps all users with similar profiles

-- get the aggregation (count) of calls by users
WITH user_call_count AS (
    SELECT user_id, COUNT(*) AS call_count
    FROM rc_calls
    GROUP BY user_id
)

-- filter the rank up to top 2 user(s)
SELECT *
FROM (
    -- rank call count by company level for each user
    SELECT rcu.company_id,
           rcu.user_id,
           DENSE_RANK() OVER (PARTITION BY rcu.company_id
                              ORDER BY ucc.call_count DESC) AS rank
    FROM rc_users rcu
    JOIN user_call_count ucc
        ON rcu.user_id = ucc.user_id
) call_count_ranking
WHERE rank <= 2;
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2019").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic: we need top 2 users that called the most
-- need: a ranking of users, ranking keeps all users with similar profiles

-- get the aggregation (count) of calls by users
WITH user_call_count AS (
    SELECT user_id, COUNT(*) AS call_count
    FROM rc_calls
    GROUP BY user_id
)

-- filter the rank up to top 2 user(s)
SELECT *
FROM (
    -- rank call count by company level for each user
    SELECT rcu.company_id,
           rcu.user_id,
           DENSE_RANK() OVER (PARTITION BY rcu.company_id
                              ORDER BY ucc.call_count DESC) AS rank
    FROM rc_users rcu
    JOIN user_call_count ucc
        ON rcu.user_id = ucc.user_id
) call_count_ranking
WHERE rank <= 2;
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
