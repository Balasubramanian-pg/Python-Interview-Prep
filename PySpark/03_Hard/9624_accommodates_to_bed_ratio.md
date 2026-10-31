# StrataScratch Question ID: 9624 - Accommodates-to-bed Ratio

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9624` |
| **Title** | **Accommodates-to-bed Ratio** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9624) |

---

## 1. Problem Description

Find the average accommodates-to-beds ratio for shared rooms in each city. Sort your results by listing cities with the highest ratios

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
-- 1. find the individual accommodates2bed ratio per listing first
-- 2. avg a2b ratio by each city
-- 3. order by desc in highest ratio

SELECT city,
       AVG(a2b_ratio) AS city_a2b
FROM (
    SELECT id,
           city,
           (accommodates/beds::float) AS a2b_ratio
    FROM airbnb_search_details
    