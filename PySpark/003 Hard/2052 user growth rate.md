# StrataScratch Question ID: 2052 - User Growth Rate

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2052` |
| **Title** | **User Growth Rate** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Salesforce** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2052) |

---

## 1. Problem Description

Find the growth rate of active users for Dec 2020 to Jan 2021 for each account. The growth rate is defined as the number of users in January 2021 divided by the number of users in Dec 2020. Output the account_id and growth rate.

---

## 2. Input Tables & Schema

```text
<sf_events>
date                datetime
account_id          varchar
user_id             varchar
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
# -- logic: we need count users across two time period for each account_id
-- assumption: all users present are counted as active

-- growth rate: (after distinct users / before distinct users)
SELECT b.account_id, a.distinct_users/ b.distinct_users::float AS growth_rate
-- counting the distinct users before
FROM (
    SELECT account_id, COUNT(DISTINCT user_id) as distinct_users
    FROM sf_events
    -- getting the year-month
    WHERE LEFT(date::varchar, 7) = '2020-12'
    GROUP BY 1
) b
-- counting the distinct users after
JOIN (
    SELECT account_id, COUNT(DISTINCT user_id) as distinct_users
    FROM sf_events
    -- getting the year-month
    WHERE LEFT(date::varchar, 7) = '2021-01'
    GROUP BY 1
) a
ON b.account_id = a.account_id
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2052").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic: we need count users across two time period for each account_id
-- assumption: all users present are counted as active

-- growth rate: (after distinct users / before distinct users)
SELECT b.account_id, a.distinct_users/ b.distinct_users::float AS growth_rate
-- counting the distinct users before
FROM (
    SELECT account_id, COUNT(DISTINCT user_id) as distinct_users
    FROM sf_events
    -- getting the year-month
    WHERE LEFT(date::varchar, 7) = '2020-12'
    GROUP BY 1
) b
-- counting the distinct users after
JOIN (
    SELECT account_id, COUNT(DISTINCT user_id) as distinct_users
    FROM sf_events
    -- getting the year-month
    WHERE LEFT(date::varchar, 7) = '2021-01'
    GROUP BY 1
) a
ON b.account_id = a.account_id
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
