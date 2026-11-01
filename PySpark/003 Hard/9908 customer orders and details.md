# StrataScratch Question ID: 9908 - Customer Orders And Details

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9908` |
| **Title** | **Customer Orders And Details** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9908) |

---

## 1. Problem Description

Find the number of orders, the number of customers, and the total cost of orders for each city. Only include cities that have made at least 5 orders and count all customers in each city even if they did not place an order.

Output each calculation along with the corresponding city name.

---

## 2. Input Tables & Schema

```text
<customers>
id                  int
first_name          varchar
last_name           varchar
city                varchar
address             varchar
phone_number        varchar

orders
id                  int
cust_id             int
order_date          datetime
order_details       varchar
total_order_cost    int
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
-- aggregation by city

-- assumption:
-- only include cities with at least 5 orders
-- count all customers in each city even if they did not place an order

-- logic:
-- LEFT JOIN orders on customers
-- GROUPBY(city) to aggregate by city
-- COUNT(orders.id) for number of orders per city
-- COUNT(customers.id) for number of customer per city
-- COALESCE(SUM(total_order_cost)) total cost of orders, 0 if no COUNT(orders.id)

-- output:
-- city, no. orders, no. custs, total_order_cost


SELECT city,
       COUNT(o.id) AS no_orders,
       COUNT(DISTINCT c.id) AS no_customers,
       COALESCE(SUM(total_order_cost), 0) AS total_order_cost
FROM customers c
LEFT JOIN orders o
    ON c.id = o.cust_id
GROUP BY 1
HAVING COUNT(o.id) >= 5
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9908").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- aggregation by city

-- assumption:
-- only include cities with at least 5 orders
-- count all customers in each city even if they did not place an order

-- logic:
-- LEFT JOIN orders on customers
-- GROUPBY(city) to aggregate by city
-- COUNT(orders.id) for number of orders per city
-- COUNT(customers.id) for number of customer per city
-- COALESCE(SUM(total_order_cost)) total cost of orders, 0 if no COUNT(orders.id)

-- output:
-- city, no. orders, no. custs, total_order_cost


SELECT city,
       COUNT(o.id) AS no_orders,
       COUNT(DISTINCT c.id) AS no_customers,
       COALESCE(SUM(total_order_cost), 0) AS total_order_cost
FROM customers c
LEFT JOIN orders o
    ON c.id = o.cust_id
GROUP BY 1
HAVING COUNT(o.id) >= 5
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
