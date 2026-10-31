# StrataScratch Question ID: 2150 - Customers Who Purchased The Same Product

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2150` |
| **Title** | **Customers Who Purchased The Same Product** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2150) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Customers Who Purchased the Same Product.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2150.
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
from pyspark.sql import functions as F

# we filter our data as per our requirements 
filtered_online_products = online_products.filter(F.col('product_class') == 'FURNITURE').select ('product_id','brand_name')

# now we perform join between furniture products with orders
joined_df = filtered_online_products.join(
        online_orders,
        filtered_online_products['product_id'] == online_orders['product_id'],
        "inner"
    ).select(
        filtered_online_products['product_id'],
        "brand_name",
        "customer_id"
)

# group by product and brand .
final_df = joined_df.groupBy(
    "product_id",
    "brand_name"
    ).agg(
        F.collect_set("customer_id").