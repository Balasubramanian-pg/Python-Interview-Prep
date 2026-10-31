# StrataScratch Question ID: 2097 - Premium Accounts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2097` |
| **Title** | **Premium Accounts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2097) |

---

## 1. Problem Description

You have a dataset that records daily active users for each premium account. A premium account appears in the data every day as long as it remains premium. However, some premium accounts may be temporarily discounted, meaning they are not actively paying—this is indicated by a final_price of 0.


For each of the first 7 available dates in the dataset, count the number of premium accounts that were actively paying on that day. Then, track how many of those same accounts are still premium and actively paying exactly 7 days later, based solely on their status on that 7th day (i.e., both dates must exist in the dataset). Accounts are only counted if they appear in the data on both dates.


Output three columns:
•   The date of initial calculation.
•   The number of premium accounts that were actively paying on that day.
•   The number of those accounts that remain premium and are still paying after 7 days.

---

## 2. Input Tables & Schema

```text
Table
premium_accounts_by_day
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

entry_date	premium_paid_accounts	premium_paid_accounts_after_7d
2022-02-07	2	2
2022-02-08	3	2
2022-02-09	3	2
2022-02-10	4	3
2022-02-11	4	1
premium_accounts_by_day
Preview
account_id	entry_date	users_visited_7d	final_price	plan_size
A01	2022-02-07	1	100	10
A03	2022-02-07	30	400	50
A01	2022-02-08	3	100	10
A03	2022-02-08	39	400	50
A05	2022-02-08	14	400	50
A01	2022-02-09	12	100	10
A03	2022-02-09	44	400	50
A04	2022-02-09	25	0	70
A05	2022-02-09	32	400	50
A01	2022-02-10	17	100	10
A02	2022-02-10	82	800	100
A03	2022-02-10	60	400	50
A04	2022-02-10	72	0	70
A05	2022-02-10	45	400	50
A01	2022-02-11	26	100	10
A02	2022-02-11	102	800	100
A03	2022-02-11	76	400	50
A04	2022-02-11	115	0	70
A05	2022-02-11	50	400	50
A01	2022-02-12	28	100	10
A02	2022-02-12	181	800	100
A03	2022-02-12	104	400	50
A04	2022-02-12	140	20	70
A01	2022-02-13	29	100	10
A02	2022-02-13	235	800	100
A03	2022-02-13	113	400	50
A04	2022-02-13	154	20	70
A01	2022-02-14	34	100	10
A02	2022-02-14	305	800	100
A03	2022-02-14	117	400	50
A04	2022-02-14	195	20	70
A01	2022-02-15	38	100	10
A02	2022-02-15	389	800	100
A03	2022-02-15	127	400	50
A04	2022-02-15	253	20	70
A01	2022-02-16	35	100	10
A02	2022-02-16	412	800	100
A03	2022-02-16	143	0	50
A04	2022-02-16	276	20	70
A05	2022-02-16	31	250	20
A01	2022-02-17	38	100	10
A02	2022-02-17	400	800	100
A03	2022-02-17	172	0	50
A04	2022-02-17	276	20	70
A05	2022-02-17	26	250	20
A02	2022-02-18	310	800	100
A03	2022-02-18	186	0	50
A04	2022-02-18	239	20	70
A02	2022-02-19	142	800	100
A03	2022-02-19	189	0	50
A04	2022-02-19	228	20	70
A03	2022-02-20	191	0	50
A04	2022-02-20	264	20	70
A05	2022-02-20	25	350	30
account_id:
string
entry_date:
date
users_visited_7d:
bigint
final_price:
bigint
plan_size:
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
from pyspark.sql import *

spark = SparkSession.builder.appName("app").getOrCreate()
df=premium_accounts_by_day
df=df.orderBy(col("entry_date"),col("account_id"))
df2=df.filter(df.entry_d