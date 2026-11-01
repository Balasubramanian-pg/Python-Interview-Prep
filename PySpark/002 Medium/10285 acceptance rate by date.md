# StrataScratch Question ID: 10285 - Acceptance Rate By Date

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10285` |
| **Title** | **Acceptance Rate By Date** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10285) |

---

## 1. Problem Description

Calculate the friend acceptance rate for each date when friend requests were sent. A request is sent if action = sent and accepted if action = accepted. If a request is not accepted, there is no record of it being accepted in the

---

## 2. Input Tables & Schema

```text
table. The output will only include dates where requests were sent and at least one of them was accepted, as the acceptance rate can only be calculated for those dates. Show the results ordered from the earliest to the latest date.

Table
fb_friend_requests
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

request_date	percentage_acceptance
2020-01-04	0.75
2020-01-06	0.67
fb_friend_requests
Preview
user_id_sender	user_id_receiver	date	action
ad4943sdz	948ksx123d	2020-01-04	sent
ad4943sdz	948ksx123d	2020-01-06	accepted
dfdfxf9483	9djjjd9283	2020-01-04	sent
dfdfxf9483	9djjjd9283	2020-01-15	accepted
ffdfff4234234	lpjzjdi4949	2020-01-06	sent
fffkfld9499	993lsldidif	2020-01-06	sent
fffkfld9499	993lsldidif	2020-01-10	accepted
fg503kdsdd	ofp049dkd	2020-01-04	sent
fg503kdsdd	ofp049dkd	2020-01-10	accepted
hh643dfert	847jfkf203	2020-01-04	sent
r4gfgf2344	234ddr4545	2020-01-06	sent
r4gfgf2344	234ddr4545	2020-01-11	accepted
user_id_sender:
string
user_id_receiver:
string
date:
date
action:
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
import pyspark
from pyspark.sql.functions import *
from pyspark.sql import *
# Start writing code
df=fb_friend_requests
df_sent=df.filter(col("action")=="sent")
df_accepted=df.filter(col("action")=="accepted")
df_accepted=df_accepted.withColumnRenamed("date","date1").withColumnRenamed("user_id_sender","user_id_sender1").withColumnRenamed("user_id_receiver","user_id_receiver1")
# df_sent.show(truncate=False)
# df_accepted.show(truncate=False)
df_sent_cnt=df_sent.groupBy(col("date")).agg(count(col("user_id_sender")).alias("cnt"))
# df_sent_cnt.show(truncate=False)
df_sent_accepted = df_sent.join(df_accepted,df_sent.user_id_sender==df_accepted.user_id_sender1,"right")
df_sent_accepted=df_sent_accepted.groupBy(col("date")).agg(count(col("user_id_sender")).alias("cnt1"))
df_sent_accepted=df_sent_accepted.withColumnRenamed("date","date2")
# df_sent_accepted.show(truncate=False)
df_sent_accepted=df_sent_accepted.join(df_sent_cnt,df_sent_accepted.date2==df_sent_cnt.date,"left").select("date","cnt","cnt1")
df_sent_accepted=df_sent_accepted.withColumn("percentage_acceptance",round(col("cnt1")/col("cnt"),2)).withColumnRenamed("date","request_date")
df_sent_accepted=df_sent_accepted.select("request_date","percentage_acceptance")
# df_sent_accepted.show(truncate=False)
df_sent_accepted.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# fb_friend_requests.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10285").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10285\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
