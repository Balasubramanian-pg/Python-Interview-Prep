# StrataScratch Question ID: 9913 - Order Details

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9913` |
| **Title** | **Order Details** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9913) |

---

## 1. Problem Description

Find order details made by Jill and Eva.
Consider the Jill and Eva as first names of customers.
Output the order date, details and cost along with the first name.
Order records based on the customer id in ascending order.

---

## 2. Input Tables & Schema

```text
<customers>
id                          int
first_name                  varchar
last_name                   varchar
city                        varchar
address                     varchar
phone_number                varchar

<orders>
id                          int
cust_id                     int
order_date                  datetime
order_details               varchar
total_order_cost            int
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


# here we filter the dimensins as per bussiness neeed 
customers = customers.filter(F.col("first_name").isin("Jill","Eva"))

# now we inner join facts and dimensions
customers_orders = orders.join(customers, customers.id == orders.cust_id , "inner" ).select(
    F.col("order_date"),F.col("order_details"),F.col("total_order_cost"),F.col("first_name")).orderBy(F.col("cust_id").asc())
    

# To validate your sol