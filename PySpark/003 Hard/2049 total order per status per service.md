# StrataScratch Question ID: 2049 - Total Order Per Status Per Service

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2049` |
| **Title** | **Total Order Per Status Per Service** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Uber** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2049) |

---

## 1. Problem Description

Uber is interested in identifying gaps in their business. Calculate the count of orders for each status of each service. Your output should include the service name, status of the order, and the number of orders.

---

## 2. Input Tables & Schema

```text
<uber_orders>
order_date              datetime
number_of_orders        int
status_of_order         varchar
monetary_value          float
service_name            varchar
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
# -- logic: count status for each service

-- simple groupby
SELECT service_name, status_of_order, SUM(number_of_orders) AS order_sum
FROM uber_orders
GROUP BY 1, 2;
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2049").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- logic: count status for each service

-- simple groupby
SELECT service_name, status_of_order, SUM(number_of_orders) AS order_sum
FROM uber_orders
GROUP BY 1, 2;
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
