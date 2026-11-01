# StrataScratch Question ID: 2102 - Flags Per Video

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2102` |
| **Title** | **Flags Per Video** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2102) |

---

## 1. Problem Description

For each video, find how many unique users flagged it. A unique user can be identified using the combination of their first name and last name. Do not consider rows in which there is no flag ID.

---

## 2. Input Tables & Schema

```text
Table
user_flags
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

video_id	num_unique_users
y6120QOlsfU	5
5qap5aO4i9A	2
Ct6BUPvE2sM	2
dQw4w9WgXcQ	5
jNQXAC9IVRw	3
user_flags
Preview
user_firstname	user_lastname	video_id	flag_id
Richard	Hasson	y6120QOlsfU	0cazx3
Mark	May	Ct6BUPvE2sM	1cn76u
Gina	Korman	dQw4w9WgXcQ	1i43zk
Mark	May	Ct6BUPvE2sM	1n0vef
Mark	May	jNQXAC9IVRw	1sv6ib
Gina	Korman	dQw4w9WgXcQ	20xekb
Mark	May	5qap5aO4i9A	4cvwuv
Daniel	Bell	5qap5aO4i9A	4sd6dv
Richard	Hasson	y6120QOlsfU	6jjkvn
Pauline	Wilks	jNQXAC9IVRw	7ks264
Courtney		dQw4w9WgXcQ	
Helen	Hearn	dQw4w9WgXcQ	8946nx
Mark	Johnson	y6120QOlsfU	8wwg0l
Richard	Hasson	dQw4w9WgXcQ	arydfd
Gina	Korman		
Mark	Johnson	y6120QOlsfU	bl40qw
Richard	Hasson	dQw4w9WgXcQ	ehn1pt
Lopez	dQw4w9WgXcQ	hucyzx
Greg		5qap5aO4i9A	
Pauline	Wilks	jNQXAC9IVRw	i2l3oo
Richard	Hasson	jNQXAC9IVRw	i6336w
Johnson	y6120QOlsfU	iey5vi
William 	Kwan	y6120QOlsfU	kktiwe
Ct6BUPvE2sM	
Loretta	Crutcher	y6120QOlsfU	nkjgku
Pauline	Wilks	jNQXAC9IVRw	ov5gd8
Mary	Thompson	Ct6BUPvE2sM	qa16ua
Daniel	Bell	5qap5aO4i9A	xciyse
Evelyn	Johnson	dQw4w9WgXcQ	xvhk6d
user_firstname:
string
user_lastname:
string
video_id:
string
flag_id:
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

# Start writing code
df = user_flags
# df.show(100,truncate=False)
df1=df.withColumn("name",concat(col("user_firstname"),lit(" "),col("user_lastname")))
df1=df1.filter(col("flag_id").isNotNull())
df_distinct = df1.dropDuplicates(["name","video_id"])
# print(df_distinct.count())
df=df_distinct.groupBy(col("video_id")).agg(count("*").alias("num_unique_users"))
# df.show(truncate=False)

df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2102").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2102\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
