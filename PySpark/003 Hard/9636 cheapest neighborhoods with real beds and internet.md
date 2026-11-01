# StrataScratch Question ID: 9636 - Cheapest Neighborhoods With Real Beds And Internet

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9636` |
| **Title** | **Cheapest Neighborhoods With Real Beds And Internet** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9636) |

---

## 1. Problem Description

Find neighborhoods where you can sleep on a real bed in a villa with internet while paying the lowest price possible.

---

## 2. Input Tables & Schema

```text
<airbnb_search_details>
id                      int
price                   float
property_type           varchar
room_type               varchar
amenities               varchar
accommodates            int
bathrooms               int
bed_type                varchar
cancellation_policy     varchar
cleaning_fee            bool
city                    varchar
host_identity_verified  varchar
host_response_rate      varchar
host_since              datetime
neighbourhood           varchar
number_of_reviews       int
review_scores_rating    float
zipcode                 int
bedrooms                int
beds                    int
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
-- 1. filter for internet, bed_type and property_type
-- 2. rank by price
-- 3. get the lowest price

SELECT neighbourhood
FROM (
    SELECT neighbourhood,
           RANK() OVER(ORDER BY price ASC) AS price_rank
    FROM (
        SELECT id,
               neighbourhood,
               price
        FROM airbnb_search_details
        WHERE amenities LIKE '%Wireless Internet%'
            AND property_type = 'Villa'
            AND bed_type = 'Real Bed'
    ) price_ranking
) cheapest_house
WHERE price_rank = 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9636").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic:
-- 1. filter for internet, bed_type and property_type
-- 2. rank by price
-- 3. get the lowest price

SELECT neighbourhood
FROM (
    SELECT neighbourhood,
           RANK() OVER(ORDER BY price ASC) AS price_rank
    FROM (
        SELECT id,
               neighbourhood,
               price
        FROM airbnb_search_details
        WHERE amenities LIKE '%Wireless Internet%'
            AND property_type = 'Villa'
            AND bed_type = 'Real Bed'
    ) price_ranking
) cheapest_house
WHERE price_rank = 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
