# StrataScratch Question ID: 2029 - Most Popular Client For Calls

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2029` |
| **Title** | **Most Popular Client For Calls** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2029) |

---

## 1. Problem Description

Select the most popular client_id based on the number of users who individually have at least 50% of their events from the following list: 'video call received', 'video call sent', 'voice call received', 'voice call sent'.

---

## 2. Input Tables & Schema

```text
Table
fact_events
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

CLIENT_ID
desktop
fact_events
Preview
id	time_id	user_id	customer_id	client_id	event_type	event_id
1	2020-02-28	3668-QPYBK	Sendit	desktop	message sent	3
2	2020-02-28	7892-POOKP	Connectix	mobile	file received	2
3	2020-04-03	9763-GRSKD	Zoomit	desktop	video call received	7
4	2020-04-02	9763-GRSKD	Connectix	desktop	video call received	7
5	2020-02-06	9237-HQITU	Sendit	desktop	video call received	7
6	2020-02-27	8191-XWSZG	Connectix	desktop	file received	2
7	2020-04-03	9237-HQITU	Connectix	desktop	video call received	7
8	2020-03-01	9237-HQITU	Connectix	mobile	message received	4
9	2020-04-02	4190-MFLUW	Connectix	mobile	video call received	7
10	2020-04-21	9763-GRSKD	Sendit	desktop	file received	2
11	2020-02-28	5129-JLPIS	Electric Gravity	mobile	video call started	6
12	2020-03-31	6713-OKOMC	Connectix	desktop	file received	2
13	2020-03-21	6388-TABGU	Connectix	desktop	message sent	3
14	2020-03-03	7469-LKBCI	Connectix	mobile	video call received	7
15	2020-02-11	9237-HQITU	Connectix	desktop	video call received	7
16	2020-03-01	5575-GNVDE	Zoomit	desktop	file received	2
17	2020-03-02	6388-TABGU	Connectix	desktop	message sent	3
18	2020-04-06	9305-CDSKC	Connectix	desktop	message received	4
19	2020-02-13	3668-QPYBK	Connectix	mobile	file sent	1
20	2020-04-03	9959-WOFKT	Connectix	desktop	file received	2
21	2020-03-15	9305-CDSKC	Zoomit	mobile	message received	4
22	2020-04-01	7892-POOKP	eShop	mobile	voice call started	8
23	2020-04-09	8191-XWSZG	Connectix	mobile	file received	2
24	2020-04-08	3668-QPYBK	eShop	desktop	message sent	3
25	2020-03-05	8191-XWSZG	Zoomit	mobile	file received	2
26	2020-02-24	3668-QPYBK	Connectix	mobile	api message received	5
27	2020-03-26	6388-TABGU	Zoomit	desktop	message received	4
28	2020-02-03	7795-CFOCW	Connectix	mobile	api message received	5
29	2020-03-19	7892-POOKP	Connectix	desktop	message received	4
30	2020-04-07	9763-GRSKD	Connectix	mobile	message sent	3
31	2020-04-06	9959-WOFKT	Connectix	desktop	message received	4
32	2020-02-15	9237-HQITU	Connectix	mobile	message sent	3
33	2020-04-06	4183-MYFRB	Sendit	desktop	file received	2
34	2020-03-13	9305-CDSKC	Connectix	desktop	video call received	7
35	2020-04-05	9959-WOFKT	Connectix	mobile	message received	4
36	2020-03-28	6388-TABGU	Connectix	desktop	message sent	3
37	2020-04-03	4183-MYFRB	Connectix	desktop	message received	4
38	2020-03-15	5575-GNVDE	Electric Gravity	desktop	video call started	6
39	2020-03-06	8091-TTVAX	Zoomit	desktop	file received	2
40	2020-03-25	4190-MFLUW	Connectix	mobile	file received	2
41	2020-04-13	9959-WOFKT	Zoomit	mobile	video call received	7
42	2020-02-20	7590-VHVEG	Sendit	desktop	file received	2
43	2020-03-13	9305-CDSKC	Connectix	mobile	voice call received	9
44	2020-02-22	1452-KIOVK	Zoomit	mobile	voice call started	8
45	2020-04-18	9959-WOFKT	Connectix	desktop	file received	2
46	2020-02-04	9305-CDSKC	Connectix	desktop	message sent	3
47	2020-04-06	4190-MFLUW	Connectix	mobile	file sent	1
48	2020-03-22	1452-KIOVK	Connectix	mobile	file sent	1
49	2020-04-06	5129-JLPIS	Sendit	desktop	message sent	3
50	2020-04-04	7469-LKBCI	Sendit	mobile	message received	4
51	2020-02-14	3668-QPYBK	Connectix	desktop	message received	4
52	2020-03-28	5575-GNVDE	Sendit	desktop	file received	2
53	2020-04-05	8091-TTVAX	Connectix	desktop	message sent	3
54	2020-03-01	7469-LKBCI	Connectix	desktop	video call started	6
55	2020-02-20	5129-JLPIS	Connectix	desktop	voice call received	9
56	2020-03-13	7590-VHVEG	Zoomit	mobile	message received	4
57	2020-04-09	8091-TTVAX	Sendit	desktop	video call received	7
58	2020-02-27	9237-HQITU	eShop	desktop	video call received	7
59	2020-03-24	8191-XWSZG	Connectix	mobile	video call received	7
60	2020-03-19	7469-LKBCI	Sendit	desktop	video call received	7
61	2020-03-29	7892-POOKP	Connectix	desktop	message received	4
62	2020-03-14	5129-JLPIS	Connectix	mobile	message sent	3
63	2020-03-07	4190-MFLUW	Electric Gravity	desktop	message sent	3
64	2020-03-05	4190-MFLUW	Connectix	desktop	file sent	1
65	2020-02-06	3668-QPYBK	Sendit	desktop	video call received	7
66	2020-02-08	6713-OKOMC	Connectix	desktop	voice call started	8
67	2020-02-24	6713-OKOMC	Connectix	mobile	file sent	1
68	2020-03-25	7469-LKBCI	Connectix	mobile	message received	4
69	2020-02-12	1452-KIOVK	Connectix	desktop	message sent	3
70	2020-02-08	7795-CFOCW	Connectix	desktop	voice call received	9
71	2020-03-10	7469-LKBCI	Connectix	mobile	video call received	7
72	2020-03-09	9237-HQITU	Sendit	desktop	video call received	7
73	2020-03-13	5575-GNVDE	Sendit	mobile	voice call received	9
74	2020-03-17	7469-LKBCI	Electric Gravity	desktop	message received	4
75	2020-03-02	4190-MFLUW	Sendit	mobile	message sent	3
76	2020-04-09	7892-POOKP	Sendit	desktop	file sent	1
77	2020-03-18	7590-VHVEG	Sendit	mobile	message received	4
78	2020-02-27	3655-SNQYZ	Sendit	desktop	file received	2
79	2020-02-03	7469-LKBCI	Zoomit	desktop	file received	2
80	2020-02-03	0280-XJGEX	eShop	desktop	message sent	3
81	2020-02-25	6713-OKOMC	Connectix	desktop	message received	4
82	2020-02-19	6713-OKOMC	Connectix	mobile	file sent	1
83	2020-03-26	7590-VHVEG	Electric Gravity	desktop	video call received	7
84	2020-03-19	8091-TTVAX	eShop	desktop	message received	4
85	2020-02-17	9237-HQITU	Connectix	desktop	file sent	1
86	2020-03-14	3668-QPYBK	Sendit	mobile	file sent	1
87	2020-02-17	8191-XWSZG	Connectix	mobile	video call started	6
88	2020-02-13	3668-QPYBK	Sendit	desktop	voice call started	8
89	2020-04-01	9959-WOFKT	Connectix	mobile	video call started	6
90	2020-03-26	7795-CFOCW	Sendit	desktop	file received	2
91	2020-04-08	7795-CFOCW	Zoomit	mobile	message received	4
92	2020-03-28	9305-CDSKC	Connectix	desktop	file sent	1
93	2020-03-06	6713-OKOMC	Connectix	desktop	file received	2
94	2020-02-23	9305-CDSKC	Sendit	desktop	message sent	3
95	2020-03-19	5575-GNVDE	Sendit	desktop	voice call received	9
96	2020-03-28	3668-QPYBK	eShop	desktop	message received	4
97	2020-03-22	8091-TTVAX	Connectix	mobile	voice call received	9
98	2020-02-09	3655-SNQYZ	Connectix	desktop	file received	2
99	2020-03-18	6388-TABGU	Sendit	desktop	message received	4
100	2020-03-31	3668-QPYBK	Sendit	mobile	file sent	1
101	2020-03-02	5129-JLPIS	Sendit	desktop	message sent	3
102	2020-03-02	9237-HQITU	Connectix	desktop	voice call received	9
103	2020-03-01	9305-CDSKC	Connectix	desktop	message received	4
104	2020-04-07	5575-GNVDE	Connectix	mobile	message received	4
105	2020-02-17	8191-XWSZG	Zoomit	mobile	message received	4
106	2020-03-02	0280-XJGEX	Electric Gravity	mobile	video call started	6
107	2020-02-07	7590-VHVEG	eShop	mobile	video call received	7
108	2020-03-06	7892-POOKP	Connectix	mobile	message sent	3
109	2020-02-03	9237-HQITU	Sendit	mobile	video call started	6
110	2020-03-02	1452-KIOVK	eShop	mobile	file received	2
111	2020-02-04	7892-POOKP	Connectix	desktop	message received	4
112	2020-03-02	8191-XWSZG	Connectix	desktop	message received	4
113	2020-03-25	4183-MYFRB	Sendit	desktop	video call received	7
114	2020-02-23	6713-OKOMC	Connectix	desktop	message sent	3
115	2020-03-02	9305-CDSKC	Sendit	desktop	voice call started	8
116	2020-03-11	7590-VHVEG	Sendit	desktop	api message received	5
117	2020-04-08	8091-TTVAX	Zoomit	mobile	file sent	1
118	2020-02-01	6713-OKOMC	Electric Gravity	mobile	file received	2
119	2020-03-24	8091-TTVAX	Electric Gravity	desktop	message sent	3
120	2020-03-06	8091-TTVAX	Electric Gravity	mobile	file sent	1
121	2020-03-09	5575-GNVDE	Connectix	mobile	file sent	1
122	2020-03-22	8091-TTVAX	Connectix	mobile	video call received	7
123	2020-03-02	7469-LKBCI	Connectix	mobile	video call started	6
124	2020-03-23	5575-GNVDE	Connectix	mobile	voice call received	9
125	2020-03-30	9305-CDSKC	eShop	desktop	message sent	3
126	2020-03-25	4190-MFLUW	Connectix	desktop	video call started	6
127	2020-03-09	7590-VHVEG	Connectix	mobile	api message received	5
128	2020-03-14	7795-CFOCW	Sendit	desktop	file received	2
129	2020-04-04	9959-WOFKT	Connectix	mobile	message received	4
130	2020-03-31	5129-JLPIS	Connectix	desktop	video call received	7
131	2020-03-27	4183-MYFRB	Connectix	desktop	voice call received	9
132	2020-04-03	5129-JLPIS	Connectix	desktop	file received	2
133	2020-03-01	0280-XJGEX	Connectix	desktop	video call started	6
134	2020-04-16	9763-GRSKD	Connectix	desktop	message sent	3
135	2020-03-07	6388-TABGU	Connectix	desktop	api message received	5
136	2020-03-20	9305-CDSKC	Zoomit	mobile	message sent	3
137	2020-03-10	8091-TTVAX	Sendit	desktop	video call started	6
138	2020-03-20	0280-XJGEX	Zoomit	mobile	message sent	3
139	2020-02-23	5129-JLPIS	Connectix	mobile	file received	2
140	2020-02-18	7590-VHVEG	Connectix	mobile	file sent	1
141	2020-02-18	1452-KIOVK	Connectix	mobile	file received	2
142	2020-02-08	3668-QPYBK	Sendit	desktop	message received	4
143	2020-04-13	7469-LKBCI	Sendit	desktop	video call received	7
144	2020-03-22	6388-TABGU	eShop	mobile	file sent	1
145	2020-03-13	0280-XJGEX	Sendit	desktop	message sent	3
146	2020-03-07	6388-TABGU	Connectix	desktop	voice call received	9
147	2020-03-21	8091-TTVAX	Connectix	mobile	message sent	3
148	2020-04-03	8191-XWSZG	Connectix	desktop	file received	2
149	2020-02-22	7795-CFOCW	Connectix	desktop	message received	4
150	2020-02-14	7590-VHVEG	Connectix	desktop	message received	4
id:
bigint
time_id:
date
user_id:
string
customer_id:
string
client_id:
string
event_type:
string
event_id:
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


# Start writing code
fact_events_filt = fact_events.filter((fact_events.event_type).isin(['video call received','video call sent','voice call received','voice call sent']))
fact_events_filt = fact_events_filt.groupBy("client_id","event_type").count()
fact_events_filt = fact_events_filt.groupBy("client_id").sum("count")
fact_events_filt1 = fact_events_filt.agg(max("sum(count)"))
fact_events_filt1 = fact_events_filt1.withColumnRenamed("max(sum(count))","cnt")
fact_events_filt = fact_events_filt.withColumnRenamed("sum(count)","cnt")
df = fact_events_filt1.join(fact_events_filt,fact_events_filt1.cnt == fact_events_filt.cnt,"inner")
df = df.select("client_id")
# df.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2029").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 2029\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
