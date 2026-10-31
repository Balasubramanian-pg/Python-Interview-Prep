# StrataScratch Question ID: 10073 - Favorite Host Nationality

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10073` |
| **Title** | **Favorite Host Nationality** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Airbnb** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10073) |

---

## 1. Problem Description

For each guest reviewer, find the nationality of the reviewer’s favorite host based on the guest’s highest review score given to a host. Output the user ID of the guest along with their favorite host’s nationality.

---

## 2. Input Tables & Schema

```text
<airbnb_reviews>
from_user               int
to_user                 int
from_type               varchar
to_type                 varchar
review_score            int

<airbnb_hosts>
host_id                 int
nationality             varchar
gender                  varchar
age                     int
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
-- find the highest review score given by each guest user
-- find the host_id given the highest review
-- output the user id and the host nationality

-- assumption:
-- each user only has 1 highest review score
-- possibly more than 1 host has the same highest review score
-- if same country we can remove the duplicated host nationality

-- logic:
-- max(review_score) per user
-- filter host_id that received that the highest id
-- output the user id and their host nationality

-- retrieve the host nationality
-- remove duplicates as well
SELECT DISTINCT u.from_user,
       h.nationality
FROM (
    -- select the particular reviews that were given the highest score for each user
    SELECT r.*
    FROM airbnb_reviews r
    JOIN (
        -- select the highest review given by each guest user
        SELECT from_user,
               MAX(review_score) AS highest_score
        FROM airbnb_reviews
        WHERE from_type = 'guest'
        GROUP BY 1
    ) highest_review_score
        ON r.from_user = highest_review_score.from_user
        AND r.review_score = highest_review_score.highest_score
    -- ensure that score remains from a guest perspective
    WHERE from_type = 'guest'
) u
JOIN airbnb_hosts h
    ON u.to_user = h.host_id
ORDER BY 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10073").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- 