# StrataScratch Question ID: 2104 - User With Most Approved Flags

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2104` |
| **Title** | **User With Most Approved Flags** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2104) |

---

## 1. Problem Description

Which user flagged the most distinct videos that ended up approved by YouTube? Output, in one column, their full name or names in case of a tie. In the user's full name, include a space between the first and the last name.

---

## 2. Input Tables & Schema

```text
Tables
user_flags
flag_review
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

username
Richard Hasson
Mark May
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
flag_review
Preview
flag_id	reviewed_by_yt	reviewed_date	reviewed_outcome
0cazx3	FALSE		
1cn76u	TRUE	2022-03-15	REMOVED
1i43zk	TRUE	2022-03-15	REMOVED
1n0vef	TRUE	2022-03-15	REMOVED
1sv6ib	TRUE	2022-03-15	APPROVED
20xekb	TRUE	2022-03-17	REMOVED
4cvwuv	TRUE	2022-03-15	APPROVED
4l1tk7	FALSE		
4sd6dv	TRUE	2022-03-14	REMOVED
6jjkvn	TRUE	2022-03-16	APPROVED
7ks264	TRUE	2022-03-15	APPROVED
8946nx	FALSE		
8wwg0l	FALSE		
arydfd	TRUE	2022-03-15	APPROVED
bl40qw	TRUE	2022-03-16	REMOVED
ehn1pt	TRUE	2022-03-18	APPROVED
hucyzx	FALSE		
i2l3oo	TRUE	2022-03-17	REMOVED
i6336w	FALSE		
iey5vi	FALSE		
kc41jd	TRUE	2022-03-14	REMOVED
kktiwe	TRUE	2022-03-14	APPROVED
nkjgku	FALSE		
ov5gd8	TRUE	2022-03-17	APPROVED
qa16ua	FALSE		
xciyse	TRUE	2022-03-16	APPROVED
xvhk6d	TRUE	2022-03-17	APPROVED
flag_id:
string
reviewed_by_yt:
boolean
reviewed_date:
date
reviewed_outcome:
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
from pyspark.sql import *
from pyspark.sql.functions import *
# Start writing code
df=user_flags.na.drop(how="any")
# df.show(50,truncate=False)
df1=flag_review.filter(col("reviewed_outcome")=="APPROVED")
df1=df1.withColumnRenamed("flag_id","flag_id1")
# df1.show(50,truncate=False)
df2=df.join(df1,df.flag_id==df1.flag_id1,"left_outer")
df2=df2.na.drop(how="any").select("user_firstname","user_lastname","video_id","flag_id")
df2=df2.withColumn("username",concat(df2.user_firstname,lit(" "),df2.user_lastname)).select("username","video_id").distinct()
df2=df2.groupBy("username").agg(count("video_id")).orderBy(col("count(video_id)").desc())
df2=df2.withColumnRenamed("count(video_id)","cnt")
max1=df2.select(max(col("cnt"))).limit(1).collect()[0][0]
# print(max1)
df2=df2.filter(col("cnt")==max1).select("username")
# df2.show(truncate=False)
df2.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# user_flags.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2104").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2104\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
