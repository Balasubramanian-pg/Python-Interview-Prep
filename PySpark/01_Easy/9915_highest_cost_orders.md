# StrataScratch Question ID: 9915 - Highest Cost Orders

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9915` |
| **Title** | **Highest Cost Orders** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9915) |

---

## 1. Problem Description

Find the customer with the highest total order cost between 2019-02-01 to 2019-05-01. If customer had more than one order on a certain day, sum the order costs on daily basis. Output their first name, total cost of their items, and the date.

For simplicity, you can assume that every first name in the dataset is unique.

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
from pyspark.sql.types import *

# Start writing code
df = customers.join(orders, customers.id == orders.cust_id,"right")
# df.show(truncate=False)
# print(df.count())
df1 = df.filter((df.order_date>='2019-02-01') & (df.order_date<='2019-05-01'))
# print(df1.count())
# df1.show(truncate=False)
df2=df1.groupBy("first_name","order_date").agg(sum("total_order_cost").alias("max_cost"))
df2 = df2.orderBy(desc("max_cost")).limit(1)
# df2.show(truncate=False)
df2.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# customers.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9915").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- customer with the highest total order cost
-- between 2019-02-01 and 2019-05-01 (feb and may)
-- first name, total cost of items (by date), and date (> 1 orders on certain day possible)

-- assumption:
-- customer has > 1 order
-- there may be 