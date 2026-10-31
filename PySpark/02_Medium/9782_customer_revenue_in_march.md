# StrataScratch Question ID: 9782 - Customer Revenue In March

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9782` |
| **Title** | **Customer Revenue In March** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9782) |

---

## 1. Problem Description

Calculate the total revenue from each customer in March 2019.

Output the revenue along with the customer id and sort the results based on the revenue in descending order.

---

## 2. Input Tables & Schema

```text
<orders>
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
from pyspark.sql.functions import *
from pyspark.sql import *
# Start writing code
df=orders
df=df.withColumn("date",date_format(to_date("order_date","yyyy-MM-dd"),"yyyy-MM"))
df=df.filter(col("date")=="2019-03")
# df.show(truncate=False)
df=df.groupBy(col("cust_id")).agg(sum(col("total_order_cost")).alias("revenue"))
df=df.orderBy(col("revenue").desc())
# df.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
df.toPandas()
# orders.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9782").getOrCreate()

# If using raw SQL query on registered temporary