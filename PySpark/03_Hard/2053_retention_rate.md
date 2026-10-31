# StrataScratch Question ID: 2053 - Retention Rate

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2053` |
| **Title** | **Retention Rate** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Salesforce** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2053) |

---

## 1. Problem Description

You are given a dataset that tracks user activity. The dataset includes information about the date of user activity, the account_id associated with the activity, and the user_id of the user performing the activity. Each row in the dataset represents a user’s activity on a specific date for a particular account_id.


Your task is to calculate the monthly retention rate for users for each account_id for December 2020 and January 2021. The retention rate is defined as the percentage of users active in a given month who have activity in any future month.


For instance, a user is considered retained for December 2020 if they have activity in December 2020 and any subsequent month (e.g., January 2021 or later). Similarly, a user is retained for January 2021 if they have activity in January 2021 and any later month (e.g., February 2021 or later).


The final output should include the account_id and the ratio of the retention rate in January 2021 to the retention rate in December 2020 for each account_id. If there are no users retained in December 2020, the retention rate ratio should be set to 0.

---

## 2. Input Tables & Schema

```text
Table
sf_events
More about this question
Hints
Expected Output
sf_events
Preview
record_date	account_id	user_id
2021-01-01	A1	U1
2021-01-01	A1	U2
2021-01-06	A1	U3
2021-01-02	A1	U1
2020-12-24	A1	U2
2020-12-08	A1	U1
2020-12-09	A1	U1
2021-01-10	A2	U4
2021-01-11	A2	U4
2021-01-12	A2	U4
2021-01-15	A2	U5
2020-12-17	A2	U4
2020-12-25	A3	U6
2020-12-25	A3	U6
2020-12-25	A3	U6
2020-12-06	A3	U7
2020-12-06	A3	U6
2021-01-14	A3	U6
2021-02-07	A1	U1
2021-02-10	A1	U2
2021-02-01	A2	U4
2021-02-01	A2	U5
2020-12-05	A1	U8
record_date:
date
account_id:
string
user_id:
string
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
import datetime
import pandas as pd
import pyspark
from pyspark.sql.functions import *
from pyspark.sql.window import Window
from pyspark.sql import SparkSession
# Start writing code

sf_events1 = sf_events
df = sf_events.groupBy("user_id").agg(max("date").alias("maximum_date"))
df = df.withColumn("extract_date",date_format("maximum_date","yyyy-MM"))
# print(df)
# df.show(truncate=False)
# print(sf_events.count())
df = df.withColumnRenamed("user_id","usr_id")

df1 = sf_events.withColumn("date1",date_format("date","yyyy-MM"))
# df1.show(truncate=False)
# print(df1.count())

df1 = df1.filter(col("date").between(pd.to_datetime('2020-12-01'),pd.to_datetime('2021-12-31')))
# print("Filtered df1 count",df1.count())
# df1.show(truncate=False)

df2 = df1.select("account_id","user_id","date1").dropDuplicates()
# df2.show(truncate=False)
# print(df2.count())

df2 = df2.groupBy("account_id").agg(count("