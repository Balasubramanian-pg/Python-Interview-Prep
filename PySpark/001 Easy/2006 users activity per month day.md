# StrataScratch Question ID: 2006 - Users Activity Per Month Day

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2006` |
| **Title** | **Users Activity Per Month Day** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2006) |

---

## 1. Problem Description

Return a distribution of users activity per day of the month

Table:
<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2006.
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

# (trim) we create separate column for month. beacause on month we need to aggregate.
facebook_posts = facebook_posts.withColumn("month",F.month(F.col('post_date')))

# group by months 
facebook_posts = facebook_posts.groupby("month").agg(F.count('*')).alias("total number")
 
# To validate your solution, convert your final pySpark df to a pandas df
facebook_posts.toPandas()

# The Goal: We wanted to see post count for months, regardless of which year it.

# The Extraction: We didn't look at the full date. because we need only month. If it says "January 2019" or "January 2025," we just mark them both as "Month 1".

# Bucket (The Shuffle): We set out 12 buckets on the floor (one for each month). We tossed every post into its matching month's bucket. This is where the GroupBy happened.

# Count: Finally, we just counted how many pieces of paper were in each bucket.

# note : We ignored the "trash" data (user IDs, post text, and years) and only moved the Month number across our network. its efficient and fast .
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2006").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- select user activity per day of the month

-- logic
-- groupby day of month
-- count users

SELECT EXTRACT('day' FROM post_date) AS dom,
       COUNT(*)
FROM facebook_posts
GROUP BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
