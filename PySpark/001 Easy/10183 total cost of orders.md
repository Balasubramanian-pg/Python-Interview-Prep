# StrataScratch Question ID: 10183 - Total Cost Of Orders

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10183` |
| **Title** | **Total Cost Of Orders** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10183) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Total Cost Of Orders.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10183.
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

# we group by cust_id and do sum of total order cost.
orders_detail = orders.groupBy('cust_id') .agg( 
    F.sum('total_order_cost').alias('total_cost'))
    
# then we inner join both dataframes customers and order_detail
customer_order_detail = orders_detail.join(
    customers,
    orders_detail.cust_id == customers.id,
    "inner"
    )
    
# we select only bussiness required information 
customers = customer_order_detail.select("id","first_name","total_cost").orderBy('first_name')

# To validate your solution, convert your final pySpark df to a pandas df
customers.toPandas()

#Performance: groupBy collapses the data before the join, reducing Network I/O (Shuffle).
#Safety: Using F.sum() prevents the MISSING_AGGREGATION error and ensures mathematical accuracy.
#Readability: Chaining with () or \ keeps the Transformation DAG clean and maintainable.
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10183").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10183\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
