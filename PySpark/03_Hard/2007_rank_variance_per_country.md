# StrataScratch Question ID: 2007 - Rank Variance Per Country

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2007` |
| **Title** | **Rank Variance Per Country** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2007) |

---

## 1. Problem Description

Which countries have risen in the rankings based on the number of comments between Dec 2019 vs Jan 2020? Hint: Avoid gaps between ranks when ranking countries.

---

## 2. Input Tables & Schema

```text
<fb_comments_count>
user_id                 int
created_at              datetime
number_of_comments      int

<fb_active_users>
user_id                 int
name                    varchar
status                  varchar
country                 varchar
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
# -- logic: rank countries in dec 2019 and jan 2020 seperately
-- join by country
-- compare former and latter rank
-- filter country where latter rank < former rank

-- assumption: earlier period might not have comments
-- hence we need to right join on latter summary
-- we need 1,2,3,4 no gaps in rank so dense_rank()

-- ranking summary for dec 2019
WITH dec_2019_rank AS (
    SELECT u.country,
           COUNT(*) AS no_comments,
           DENSE_RANK() OVER (ORDER BY COUNT(*) DESC) AS rank
    FROM fb_comments_count c
    JOIN fb_active_users u
        ON c.user_id = u.user_id
    WHERE LEFT(c.created_at::varchar, 7) = '2019-12'
    GROUP BY 1
),

-- ranking summary jan 2020
jan_2020_rank AS (
    SELECT u.country,
           COUNT(*) AS no_comments,
           DENSE_RANK() OVER (ORDER BY COUNT(*) DESC) AS rank
    FROM fb_comments_count c
    JOIN fb_active_users u
        ON c.user_id = u.user_id
    WHERE LEFT(c.created_at::varchar, 7) = '2020-01'
    GROUP BY 1
)

SELECT j.country
FROM dec_2019_rank d
RIGHT JOIN jan_2020_rank j
    ON d.country = j.country
-- filter by either earlier period is null (0 comments, so latter period with comments will boost ranking regardless) or latter rank < former rank
WHERE (j.rank < d.rank) OR d.rank IS NULL;
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2007").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic: rank countries in dec 2019 an