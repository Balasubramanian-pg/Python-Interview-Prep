# StrataScratch Question ID: 9628 - Reviews Bins On Reviews Number

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9628` |
| **Title** | **Reviews Bins On Reviews Number** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9628) |

---

## 1. Problem Description

To better understand the effect of the review count on the price, categorize the number of reviews into the following groups along with the price.
    0 reviews: NO
    1 to 5 reviews: FEW
    6 to 15 reviews: SOME
    16 to 40 reviews: MANY
    more than 40 reviews: A LOT

Table:
<airbnb_search_details>
id                          int
price                       float
property_type               varchar
room_type                   varchar
amenities                   varchar
accommodates                int
bathrooms                   int
bed_type                    varchar
cancellation_policy         varchar
cleaning_fee                bool
city                        varchar
host_identity_verified      varchar
host_response_rate          varchar
host_since                  datetime
neighbourhood               varchar
number_of_reviews           int
review_scores_rating        float
zipcode                     int
bedrooms                    int
beds                        int

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9628.
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
# -- logic:
-- create column to group number of reviews (case when)
-- display review qualification and price

SELECT CASE
    WHEN number_of_reviews BETWEEN 1 AND 5 THEN 'FEW'
    WHEN number_of_reviews BETWEEN 6 AND 15 THEN 'SOME'
    WHEN number_of_reviews BETWEEN 16 AND 40 THEN 'MANY'
    WHEN number_of_reviews > 40 THEN 'A LOT'
    ELSE 'NO'
END AS reviews_qualification,
price
FROM airbnb_search_details
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9628").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic:
-- create column to group number of reviews (case when)
-- display review qualification and price

SELECT CASE
    WHEN number_of_reviews BETWEEN 1 AND 5 THEN 'FEW'
    WHEN number_of_reviews BETWEEN 6 AND 15 THEN 'SOME'
    WHEN number_of_reviews BETWEEN 16 AND 40 THEN 'MANY'
    WHEN number_of_reviews > 40 THEN 'A LOT'
    ELSE 'NO'
END AS reviews_qualification,
price
FROM airbnb_search_details
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
