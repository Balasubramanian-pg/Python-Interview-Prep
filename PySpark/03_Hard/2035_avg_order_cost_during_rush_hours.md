# StrataScratch Question ID: 2035 - Avg Order Cost During Rush Hours

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2035` |
| **Title** | **Avg Order Cost During Rush Hours** |
| **Difficulty** | `Hard` |
| **Company Tag** | **DoorDash** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2035) |

---

## 1. Problem Description

Write a query that returns the average order cost per hour during hours 3 PM -6 PM (15-18) in San Jose. For calculating time period use 'Customer placed order datetime' field. Earnings value is 'Order total' field. Order output by hour.

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
-- find avg order cost during hours 15 - 18
-- in SAN JOSE

-- logic:
-- filter orders by SAN JOSE and hours between 15 - 18
-- AVG(order_total)
-- group by rush hours
-- order by rush hours

-- output:
-- hour, avg(total_cost)

SELECT EXTRACT(HOUR FROM customer_placed_order_datetime) AS hour,
       AVG(order_total) avg_order_cost
FROM doordash_delivery
WHERE (EXTRACT(HOUR FROM customer