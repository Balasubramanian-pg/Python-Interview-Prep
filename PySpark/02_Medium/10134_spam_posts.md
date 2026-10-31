# StrataScratch Question ID: 10134 - Spam Posts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10134` |
| **Title** | **Spam Posts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10134) |

---

## 1. Problem Description

Calculate the percentage of spam posts in all viewed posts by day. Note that the facebook_posts table stores all posts posted by users. The facebook_post_views table is an action table denoting if a user has viewed a post.

---

## 2. Input Tables & Schema

```text
<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime

<facebook_post_views>
post_id                 int
viewer_id               int
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
-- % spam post in all VIEWED post by day

-- logic:
-- RIGHT join facebook_posts on facebook_post_views
-- count viewed post by day, count "spam" viewed post by day
-- JOIN on day -> get post by day, "spam" viewed post by day
-- compute percentage of spam post / total viewed post

WITH viewed_posts AS (
    SELECT p.post_id,
           p.post_keywords,
           p.post_date,
           pv.viewer_id
    FROM facebook_posts p
    RIGHT JOIN facebook_post_views pv
    ON p.post_id = pv.post_id
),

post_counts AS (
    SELECT a.post_date,
           COUNT(*) OVER(PARTITION BY a.post_date) AS total_views,
           b.spam_views
    FROM viewed_posts a
    JOIN (
        SELECT b.post_date,
               COUNT(*) AS spam_views
        FROM viewed_posts b
        WHERE post_keywords = '[#spam#]'
        GROUP BY 1
    ) b
        ON a.post_date = b.post_date
)

SELECT DISTINCT post_date,
       spam_views/total_views::float * 100 AS spam_share
FROM post_counts
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10134").getOrCreate