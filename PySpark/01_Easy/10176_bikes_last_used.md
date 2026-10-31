# StrataScratch Question ID: 10176 - Bikes Last Used

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10176` |
| **Title** | **Bikes Last Used** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10176) |

---

## 1. Problem Description

Find the last time each bike was in use. Output both the bike number and the date-timestamp of the bike's last use (i.e., the date-time the bike was returned). Order the results by bikes that were most recently used.

---

## 2. Input Tables & Schema

```text
<dc_bikeshare_q1_2012>
duration                    varchar
duration_seconds            int
start_time                  datetime
start_station               varchar
start_terminal              int
end_time                    datetime
end_station                 varchar
end_terminal                int
bike_number                 varchar
rider_type                  varchar
id                          int
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

# Start writing code
dc_bikeshare_q1_2012 = dc_bikeshare_q1_2012.groupBy("bike_number").agg(F.max("end_time").alias('last_used')).orderBy(F.col("last_used").desc())

# To validate your solution, convert your final pySpark df to a pandas df
dc_bikeshare_q1_2012.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10176").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective: for each bike, we want to find the last time it was used
-- output: bike_number, end_time
-- sequence: end_time DESC (latest)

-- assumption: all bikes are returned, no bikes are still in used (no end_time yet)

-- logic:
-- group by bike_number
-- rank() end_time DESC
-- take the top-rank (latest end time)

-- group by bike_number find the latest end_time
SELECT bike_number,
      end_time
FROM (
    SELECT bike_number,
          end_time,
          RANK() OVER(PARTITION BY bike_number ORDER BY end_time DESC) last_time_used_rank
    FROM dc_bikeshare_q1_2012
) end_time_rank
-- getting the latest end time
WHERE last_time_used_rank = 1
ORDER BY end_time DESC;

-- simpler solution
SELECT bike_number,
       MAX(end_time) AS latest_use_time
FROM dc_bikeshare_q1_2012
GROUP BY 1
ORDER BY 2 DESC
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
