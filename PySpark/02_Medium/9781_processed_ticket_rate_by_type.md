# StrataScratch Question ID: 9781 - Processed Ticket Rate By Type

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9781` |
| **Title** | **Processed Ticket Rate By Type** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9781) |

---

## 1. Problem Description

Find the processed rate of tickets for each type. The processed rate is defined as the number of processed tickets divided by the total number of tickets for that type. Round this result to two decimal places.

---

## 2. Input Tables & Schema

```text
Table
facebook_complaints
More about this question
Hints
Expected Output
facebook_complaints
Preview
complaint_id	type	processed
0	0	TRUE
1	0	TRUE
2	0	FALSE
3	1	TRUE
4	1	TRUE
5	1	FALSE
complaint_id:
bigint
type:
bigint
processed:
boolean
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
df = facebook_complaints
df_total = df.groupBy(col("type")).count()
df_total = df_total.withColumnRenamed("count","cnt_total")
# df_total.show(truncate=False)
df_processed = df.filter(df.processed==True)
df_processed = df_processed.groupBy(col("type")).count()
df_processed = df_processed.withColumnRenamed("count","cnt_processed")
df_processed = df_processed.withColumnRenamed("type","type1")
# df_processed.show(truncate=False)
df_ans = df_total.join(df_processed, df_total.type == df_processed.type1, "outer")
df_ans = df_ans.s