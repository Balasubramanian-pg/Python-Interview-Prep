# StrataScratch Question ID: 10353 - Workers With The Highest Salaries

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10353` |
| **Title** | **Workers With The Highest Salaries** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10353) |

---

## 1. Problem Description

Find the titles of workers that earn the highest salary. Output the highest-paid title or multiple titles that share the highest salary.

---

## 2. Input Tables & Schema

```text
<worker>
worker_id               int
first_name              varchar
last_name               varchar
salary                  int
joining_date            datetime
department              varchar

title
worker_ref_id           int
worker_title            varchar
affected_from           datetime
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
# worker.show(truncate=False)
# title.show(truncate=False)
df = worker.join(title, worker.worker_id == title.worker_ref_id,"right")
df1 = df.sort(col("salary").desc(), col("worker_title").asc()).select("salary").limit(1)
# df1.show(truncate=False)
df=df.sort(col("salary").desc(), col("worker_title").asc())
# df.show(truncate=False)
df1_lst = [data[0] for data in df1.select('salary').collect()]
# print(df1_lst)
df = df.where(col("salary")== df1_lst[0]).select("worker_title")
df=df.withColumnRenamed("worker_title","best_paid_title")
# df.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession
