# StrataScratch Question ID: 10087 - Find All Posts Which Were Reacted To With A Heart

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10087` |
| **Title** | **Find All Posts Which Were Reacted To With A Heart** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10087) |

---

## 1. Problem Description

Find all posts which were reacted to with a heart.

---

## 2. Input Tables & Schema

```text
<facebook_reactions>
poster                  int
friend                  int
reaction                varchar
date_day                int
post_id                 int

<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime
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
# we 1st filter out data on reactions(heart),there have multiple hearts for single post. so we only select distinct post_id which help us during join two tables.
facebook_reactions = facebook_reactions.filter(F.col('reaction') == 'heart').select('post_id').distinct()

# then we join("inner")  both tables based on post_id and select all required attriibutes for output
facebook_posts_reactions = facebook_posts.join(facebook_reactions,facebook_reactions.post_id == facebook_reactions.post_id,"inner").select(facebook_posts["*"])

# To validate your solution, convert your final pySpark df to a pandas df
facebook_posts_reactions.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10087").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find post that has has reaction="heart"

-- assumption:
-- post can have many reactions, but we just need "heart"
-- one post can have many hearts by different users
-- we just need distinct post_id

-- logic:
-- find reaction='heart'
-- find the post_id that associates with it
-- filter the post is in the post_id

-- select all details about the post
SELECT *
FROM facebook_posts fp
WHERE fp.post_id IN (
    -- find reaction='heart'
    SELECT DISTINCT post_id
    FROM facebook_reactions
    WHERE reaction='heart'
)
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
