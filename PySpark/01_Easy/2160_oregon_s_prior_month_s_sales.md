# StrataScratch Question ID: 2160 - Oregon's Prior Month's Sales

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2160` |
| **Title** | **Oregon's Prior Month's Sales** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2160) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Oregon's Prior Month's Sales.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2160.
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

# we filter online_orders as per requirement 
online_orders = online_orders.filter((F.month('date_sold') == 4) & (F.year('date_sold') == 2022))

# we filter online_customer as per requirement 
online_customers = online_customers.filter(F.col('state') == 'Oregon')

# join both DF
online_customer_orders = online_orders.join(
    online_customers,
    online_orders.customer_id  == online_customers.id,
    "inner"
    )

#aggreagte as per our final requirement (revenue)
# revenue  = unit * cost
online_customer_orders = online_customer_orders.withColumn("revenue", F.col('cost_in_dollars')*F.col('units_sold')).agg(F.sum('revenue').alias('total revenue'))


# To validat*F.col(''e your solution, conv