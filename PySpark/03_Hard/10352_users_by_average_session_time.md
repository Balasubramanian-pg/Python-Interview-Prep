# StrataScratch Question ID: 10352 - Users By Average Session Time

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10352` |
| **Title** | **Users By Average Session Time** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10352) |

---

## 1. Problem Description

Calculate each user's average session time. A session is defined as the time difference between a page_load and page_exit. For simplicity, assume an user has only 1 session per day and if there are multiple of the same events in that day, consider only the latest page_load and earliest page_exit. Output the user_id and their average session time.

---

## 2. Input Tables & Schema

```text
<facebook_web_log>
user_id                 int
timestamp               datetime
action                  varchar
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
# Not able to solve getting wrong answer
# Import your libraries
import pyspark
from pyspark.sql.window import Window
from pyspark.sql.functions import *
from pyspark.sql import SparkSession
from pyspark.sql.types import *
# Start writing code
# facebook_web_log
df=facebook_web_log
# print(df.count())
df=df.filter((df.action == "page_load") |  (df.action == "page_exit") )
# print(df.count())
df=df.withColumn("timestamp1",df["timestamp"].cast(DateType()))
# df.show(truncate=False)
window = Window.partitionBy("user_id","action","timestamp1").orderBy("user_id","timestamp1")
df1=df.withColumn("rnk",row_number().over(window))
# df1.show(50,truncate=False)
df2=df1.filter(df1.action == "page_load")
df3=df1.filter(df1.action == "page_exit")
# df2.show(truncate=False)
# df3.show(truncate=False)
df2=df2.withColumn("max_rnk",max("rnk").over(window))
df3=df3.withColumn("min_rnk",min("rnk").over(window))
# df2.show(truncate=False)
# df3.show(truncate=False)
# df2=df2.filter(df2.rnk == df2.max_rnk)
# df3=df3.filter(df3.rnk == df3.min_rnk)
df3=df3.withColumnRenamed("action","action1")
df3=df3.withColumnRenamed("timestamp","timestamp2")
df2_alias = df2.alias("df2")
df3_alias = df3.alias("df3")
# df2.show(truncate=False)
# df3.show(truncate=False)
# df4=df2.join(df3,(df2.user_id==df3.user_id) ,"left").filter(df3.timestamp2<df2.timestamp)
df4=df2_alias.join(df3_alias,(df2_alias.user_id == df3_alias.user_id),"left").filter(df2_alias.timestamp<df3_alias.timestamp2)
# df4.show(truncate=False)
df4=df4.groupBy("df2.user_id","df2.timestamp1").agg({"timestamp":"max","timestamp2":"min"})
df4=df4.withColumn("duration",col("min(timestamp2)").cast("long")-col("max(timestamp)").cast("long"))
df4=df4.groupBy("user_id").agg(mean("duration")).withColumnRenamed("avg(duration)","avg_session_duration")
# df4.show(truncate=False)
df4.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = 