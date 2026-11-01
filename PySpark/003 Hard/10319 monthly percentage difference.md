# StrataScratch Question ID: 10319 - Monthly Percentage Difference

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10319` |
| **Title** | **Monthly Percentage Difference** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Salesforce** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10319) |

---

## 1. Problem Description

Solve the 'Monthly Percentage Difference' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
table of purchases by date, calculate the month-over-month percentage change in revenue. The output should include the year-month date (YYYY-MM) and percentage change, rounded to the 2nd decimal point, and sorted from the beginning of the year to the end of the year.
The percentage change column will be populated from the 2nd month forward and can be calculated as ((this month's revenue - last month's revenue) / last month's revenue)*100.

Table
sf_transactions
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

year_month	revenue_diff_pct
2019-01	
2019-02	-28.56
2019-03	23.35
2019-04	-13.84
2019-05	13.49
sf_transactions
Preview
id	created_at	value	purchase_id
1	2019-01-01	172692	43
2	2019-01-05	177194	36
3	2019-01-09	109513	30
4	2019-01-13	164911	30
5	2019-01-17	198872	39
6	2019-01-21	184853	31
7	2019-01-25	186817	26
8	2019-01-29	137784	22
9	2019-02-02	140032	25
10	2019-02-06	116948	43
11	2019-02-10	162515	25
12	2019-02-14	114256	12
13	2019-02-18	197465	48
14	2019-02-22	120741	20
15	2019-02-26	100074	49
16	2019-03-02	157548	19
17	2019-03-06	105506	16
18	2019-03-10	189351	46
19	2019-03-14	191231	29
20	2019-03-18	120575	44
21	2019-03-22	151688	47
22	2019-03-26	102327	18
23	2019-03-30	156147	25
24	2019-04-03	192530	36
25	2019-04-07	154765	42
26	2019-04-11	113336	12
27	2019-04-15	129073	50
28	2019-04-19	123477	21
29	2019-04-23	182142	31
30	2019-04-27	116546	39
31	2019-05-01	174748	26
32	2019-05-05	155693	42
33	2019-05-09	103012	25
34	2019-05-13	187960	33
35	2019-05-17	101202	18
36	2019-05-21	112522	10
37	2019-05-25	195969	37
38	2019-05-29	117284	40
39	2019-06-02	112956	36
40	2019-06-06	174157	29
41	2019-06-10	125975	45
42	2019-06-14	110340	29
43	2019-06-18	143066	31
44	2019-06-22	153270	11
45	2019-06-26	139635	29
46	2019-06-30	157071	35
47	2019-07-04	166552	18
48	2019-07-08	197587	34
49	2019-07-12	103958	37
50	2019-07-16	111305	28
51	2019-07-20	190266	39
52	2019-07-24	116060	44
53	2019-07-28	163802	48
54	2019-08-01	188558	21
55	2019-08-05	166528	49
56	2019-08-09	141463	28
57	2019-08-13	120110	34
58	2019-08-17	159368	12
59	2019-08-21	184900	46
60	2019-08-25	190372	38
61	2019-08-29	195877	15
62	2019-09-02	143221	21
63	2019-09-06	160413	41
64	2019-09-10	183919	43
65	2019-09-14	134535	34
66	2019-09-18	188646	31
67	2019-09-22	122706	27
68	2019-09-26	160016	21
69	2019-09-30	186777	21
70	2019-10-04	165442	50
71	2019-10-08	172445	43
72	2019-10-12	167910	21
73	2019-10-16	116646	35
74	2019-10-20	163287	15
75	2019-10-24	187293	43
76	2019-10-28	144823	11
77	2019-11-01	118317	10
78	2019-11-05	166105	38
79	2019-11-09	121128	11
80	2019-11-13	177355	38
81	2019-11-17	176442	50
82	2019-11-21	129837	10
83	2019-11-25	122363	38
84	2019-11-29	125469	10
85	2019-12-03	109657	20
86	2019-12-07	108782	35
87	2019-12-11	149235	18
88	2019-12-15	187243	36
89	2019-12-19	152538	20
90	2019-12-23	178861	34
91	2019-12-27	122675	30
92	2019-12-31	104037	18
id:
bigint
created_at:
date
value:
bigint
purchase_id:
bigint
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
from pyspark.sql import Window
# Start writing code
sf_transactions
df = sf_transactions.withColumn("new_date",date_format('created_at','yyyy-MM'))
df = df.withColumn("new_date_sum",sum("value").over(Window.partitionBy("new_date")))
df1 = df.select("new_date","new_date_sum")
df1 = df1.distinct()
# df1.show(truncate=False)
# df2 = df1.withColumn("row_number", row_number().over(Window.partitionBy("new_date").orderBy( "new_date")))
# df2.show(truncate=False)
wind = Window.partitionBy().orderBy(date_format("new_date","MM").cast('int'))
df2 = df1.withColumn("prev_new_date_sum",lag(df1.new_date_sum).over(wind))
# df2.show(truncate=False)
df2 = df2.withColumn("revenue_diff_pct",round(((df2.new_date_sum-df2.prev_new_date_sum)/df2.prev_new_date_sum)*100,2))
df3=df2.drop("new_date_sum","prev_new_date_sum")
df3 = df3.withColumnRenamed("new_date","year_month")
# df3.show(truncate=False)
#To validate your solution, convert your final pySpark df to a pandas df
df3.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10319").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10319\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
