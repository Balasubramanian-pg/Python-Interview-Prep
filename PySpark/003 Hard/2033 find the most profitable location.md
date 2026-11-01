# StrataScratch Question ID: 2033 - Find The Most Profitable Location

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2033` |
| **Title** | **Find The Most Profitable Location** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2033) |

---

## 1. Problem Description

Find the most profitable location. Write a query that calculates the average signup duration and average revenue for each location, and then compare these two measures together by taking the ratio of the average revenue and average duration for each location.

Your output should include the location, average duration, average revenue, and ratio. Sort your results from highest ratio to lowest.

---

## 2. Input Tables & Schema

```text
<signups>
signup_id               int
signup_start_date       datetime
signup_stop_date        datetime
plan_id                 int
location                varchar

<transactions>
transaction_id          int
signup_id               int
transaction_start_date  datetime
amt                     float
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
# -- objective:
-- MOST profitable location
-- FIND average signup duration, average to compute ratio

-- logic:
-- COMPUTE avg duration signup_stop_date - signup_start_date
-- AVG(duration) / signup, AVG(amt) / signup per location
-- COMPUTE ratio: avg_revenue / avg_duration
-- ORDER BY ratio

-- output:
-- location, avg_duration, avg_revenue, ratio
-- order by ratio DESC

SELECT DISTINCT location,
       avg_duration,
       avg_revenue,
       avg_revenue/avg_duration::float AS ratio
FROM (
    SELECT s2.location,
           AVG(s2.signup_stop_date - s2.signup_start_date) OVER(PARTITION BY s2.location) AS avg_duration,
           avg_revenue
    FROM signups s2
    JOIN (
        SELECT location,
               AVG(amt) OVER(PARTITION BY location) AS avg_revenue
        FROM transactions t1
        JOIN signups s1
            ON s1.signup_id = t1.signup_id
    ) t2
        ON s2.location = t2.location
) avg_metrics
ORDER BY 4 DESC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2033").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- MOST profitable location
-- FIND average signup duration, average to compute ratio

-- logic:
-- COMPUTE avg duration signup_stop_date - signup_start_date
-- AVG(duration) / signup, AVG(amt) / signup per location
-- COMPUTE ratio: avg_revenue / avg_duration
-- ORDER BY ratio

-- output:
-- location, avg_duration, avg_revenue, ratio
-- order by ratio DESC

SELECT DISTINCT location,
       avg_duration,
       avg_revenue,
       avg_revenue/avg_duration::float AS ratio
FROM (
    SELECT s2.location,
           AVG(s2.signup_stop_date - s2.signup_start_date) OVER(PARTITION BY s2.location) AS avg_duration,
           avg_revenue
    FROM signups s2
    JOIN (
        SELECT location,
               AVG(amt) OVER(PARTITION BY location) AS avg_revenue
        FROM transactions t1
        JOIN signups s1
            ON s1.signup_id = t1.signup_id
    ) t2
        ON s2.location = t2.location
) avg_metrics
ORDER BY 4 DESC
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
