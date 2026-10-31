# StrataScratch Question ID: 10172 - Best Selling Item

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10172` |
| **Title** | **Best Selling Item** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10172) |

---

## 1. Problem Description

Find the best selling item for each month (no need to separate months by year) where the biggest total invoice was paid. The best selling item is calculated using the formula (unitprice * quantity). Output the description of the item along with the amount paid.

---

## 2. Input Tables & Schema

```text
(online_retail)
invoiceno       varchar
stockcode       varchar
description     varchar
quantity        int
invoicedate     datetime
unitprice       float
customerid      float
country         varchar
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

# Start writing code
df=online_retail
df=df.withColumn("month",month(to_date(col("invoicedate"))))
df=df.withColumn("total_paid",round(col("unitprice")*col("quantity"),2))
df=df.groupby("month","description").agg(sum("total_paid").alias("total_paid"))
df1=df.groupby("month").agg(max("total_paid").alias("max_value"))
df1=df1.withColumnRenamed("month","month1")
# df.show(truncate=False)
# df1.show(truncate=False)
result=df.join(df1,(df.month==df1.month1) & (df.total_paid==df1.max_value)).select("month","description","total_paid")
result=result.orderBy("month")
# result.show(truncate=False)
result.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# online_retail.toPandas()
```

---

#