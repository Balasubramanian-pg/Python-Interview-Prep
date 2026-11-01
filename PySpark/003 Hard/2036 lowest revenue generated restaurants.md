# StrataScratch Question ID: 2036 - Lowest Revenue Generated Restaurants

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2036` |
| **Title** | **Lowest Revenue Generated Restaurants** |
| **Difficulty** | `Hard` |
| **Company Tag** | **DoorDash** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2036) |

---

## 1. Problem Description

Write a query that returns a list of the bottom 2% revenue generating restaurants. Return a list of restaurant IDs and their total revenue from when customers placed orders in May 2020.

You can calculate the total revenue by summing the order_total column. And you should calculate the bottom 2% by partitioning the total revenue into evenly distributed buckets.

---

## 2. Input Tables & Schema

```text
<doordash_delivery>
customer_placed_order_datetime          datetime
placed_order_with_restaurant_datetime   datetime
driver_at_restaurant_datetime           datetime
delivered_to_consumer_datetime          datetime
driver_id                               int
restaurant_id                           int
consumer_id                             int
is_new                                  bool
delivery_region                         varchar
is_asap                                 bool
order_total                             float
discount_amount                         float
tip_amount                              float
refunded_amount                         float
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
-- find restaurant and their revenue which falls in the bottom 2%

-- logic:
-- sum the total revenue for may 2020
-- ntile(total_revenue) and bottom 2%
-- filter restaurant if ntile = 1 (for ntile(50)) or ntile <= 2 (for ntile(100))

SELECT restaurant_id,
       total_revenue
FROM (
    SELECT restaurant_id,
           SUM(order_total) total_revenue,
           NTILE(50) OVER(ORDER BY SUM(order_total)) AS ntile
    FROM doordash_delivery
    WHERE EXTRACT('MONTH' FROM customer_placed_order_datetime) = 5
        AND EXTRACT('YEAR' FROM customer_placed_order_datetime) = 2020
    GROUP BY 1
) restaurant_revenue
WHERE ntile = 1
ORDER BY 2 DESC
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2036").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find restaurant and their revenue which falls in the bottom 2%

-- logic:
-- sum the total revenue for may 2020
-- ntile(total_revenue) and bottom 2%
-- filter restaurant if ntile = 1 (for ntile(50)) or ntile <= 2 (for ntile(100))

SELECT restaurant_id,
       total_revenue
FROM (
    SELECT restaurant_id,
           SUM(order_total) total_revenue,
           NTILE(50) OVER(ORDER BY SUM(order_total)) AS ntile
    FROM doordash_delivery
    WHERE EXTRACT('MONTH' FROM customer_placed_order_datetime) = 5
        AND EXTRACT('YEAR' FROM customer_placed_order_datetime) = 2020
    GROUP BY 1
) restaurant_revenue
WHERE ntile = 1
ORDER BY 2 DESC
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
