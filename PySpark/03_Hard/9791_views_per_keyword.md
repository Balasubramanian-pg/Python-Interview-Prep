# StrataScratch Question ID: 9791 - Views Per Keyword

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9791` |
| **Title** | **Views Per Keyword** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9791) |

---

## 1. Problem Description

Solve the 'Views Per Keyword' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime

facebook_post_views
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
-- find views each keyword has

-- assumption:
-- 1 post may have many keywords
-- for every single view -> may be attributed to many keywords
-- keywords -> what's the format?

-- logic:
-- btrim '[]' from post_keywords
-- string_to_array() turns string to an array
-- unnest() posts into individual rows with each tagged keywords
-- join the count(views) to each post_id
-- sort by highest views

-- extract keywords
SELECT UNNEST(STRING_TO_ARRAY(BTRIM(p.post_keywords, '[]#'), ',')) AS keywords,
       COALESCE(SUM(view_counts), 0) AS view_counts
FROM facebook_posts p
-- attaching views to each post_id -> keyword as well
LEFT JOIN (
    -- counts views of each post
    SELECT post_id,
           COUNT(*) as view_counts
    FROM facebook_post_views
    GROUP BY 1
) count_views
    ON p.post_id = count_views.post_id
GROUP BY 1
ORDER BY 2 DESC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataSc