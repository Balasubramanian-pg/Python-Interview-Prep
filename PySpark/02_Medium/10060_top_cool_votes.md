# StrataScratch Question ID: 10060 - Top Cool Votes

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10060` |
| **Title** | **Top Cool Votes** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Yelp** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10060) |

---

## 1. Problem Description

Find the review_text that received the highest number of  'cool' votes.
Output the business name along with the review text with the highest numbef of 'cool' votes.

---

## 2. Input Tables & Schema

```text
<yelp_reviews>
business_name       varchar
review_id           varchar
user_id             varchar
stars               varchar
review_date         datetime
review_text         varchar
funny               int
useful              int
cool                int
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
-- FIND review_text with most 'cool' votes

-- output:
-- business_name, review_view

SELECT business_name,
       review_text
FROM yelp_reviews
WHERE cool = (
    SELECT MAX(cool)
    F