# StrataScratch Question ID: 2079 - City With Most Customers

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2079` |
| **Title** | **City With Most Customers** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Lyft** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2079) |

---

## 1. Problem Description

For each city, find the number of rides in August 2021 that were not paid for using promotional codes. 
Output the city or cities where this number was the highest.

---

## 2. Input Tables & Schema

```text
(lyft_orders)
order_id                int
customer_id             varchar
driver_id               varchar
country                 varchar
city                    varchar

(lyft_payments)
order_id                int
order_date              datetime
promo_code              bool
order_fare              float
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
# -- required: city and number of rides (in Aug 2021)
-- filter: not using promo code
-- order: yes, highest ONLY

WITH total_qualified_orders AS (
    -- 1. join orders with its payment details
    SELECT o.city, COUNT(o.order_id) total_orders
    FROM lyft_orders o
    JOIN lyft_payments p
        on o.order_id = p.order_id
    -- 2. we need to filter for month criteria and promo_code
    WHERE p.promo_code IS FALSE
        AND EXTRACT(MONTH from order_date) = 8        
        AND EXTRACT(YEAR from order_date) = 2021
    GROUP BY 1
),

-- 3. output city with the highest order count
-- NOTE: we might have city with a tie
city_rank AS (
    SELECT city,
           total_orders,
           RANK() OVER (ORDER BY total_orders DESC) AS city_rank
    FROM total_qualified_orders
)

SELECT city
FROM city_rank
WHERE city_rank = 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2079").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- required: city and number of rides (in Aug 2021)
-- filter: not using promo code
-- order: yes, highest ONLY

WITH total_qualified_orders AS (
    -- 1. join orders with its payment details
    SELECT o.city, COUNT(o.order_id) total_orders
    FROM lyft_orders o
    JOIN lyft_payments p
        on o.order_id = p.order_id
    -- 2. we need to filter for month criteria and promo_code
    WHERE p.promo_code IS FALSE
        AND EXTRACT(MONTH from order_date) = 8        
        AND EXTRACT(YEAR from order_date) = 2021
    GROUP BY 1
),

-- 3. output city with the highest order count
-- NOTE: we might have city with a tie
city_rank AS (
    SELECT city,
           total_orders,
           RANK() OVER (ORDER BY total_orders DESC) AS city_rank
    FROM total_qualified_orders
)

SELECT city
FROM city_rank
WHERE city_rank = 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
