# StrataScratch Question ID: 2136 - Customer Tracking

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2136` |
| **Title** | **Customer Tracking** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Amazon** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2136) |

---

## 1. Problem Description

Shopify
Amazon


Data Engineer
Data Scientist
BI Analyst
Data Analyst
ML Engineer
Given the users' sessions logs on a particular day, calculate how many hours each user was active that day.


Note: The session starts when state=1 and ends when state=0.

---

## 2. Input Tables & Schema

```text
Table: cust_tracking
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

cust_id	sum(time_diff)
c001	5
c002	4.5
c003	1.5
c004	2
c005	7.5
cust_tracking
Preview
cust_id	state	timestamp
c001	1	2024-11-26 07:00:00
c001	0	2024-11-26 09:30:00
c001	1	2024-11-26 12:00:00
c001	0	2024-11-26 14:30:00
c002	1	2024-11-26 08:00:00
c002	0	2024-11-26 09:30:00
c002	1	2024-11-26 11:00:00
c002	0	2024-11-26 12:30:00
c002	1	2024-11-26 15:00:00
c002	0	2024-11-26 16:30:00
c003	1	2024-11-26 09:00:00
c003	0	2024-11-26 10:30:00
c004	1	2024-11-26 10:00:00
c004	0	2024-11-26 10:30:00
c004	1	2024-11-26 14:00:00
c004	0	2024-11-26 15:30:00
c005	1	2024-11-26 10:00:00
c005	0	2024-11-26 14:30:00
c005	1	2024-11-26 15:30:00
c005	0	2024-11-26 18:30:00
cust_id:
string
state:
bigint
timestamp:
timestamp
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
from pyspark.sql.window import *
# Start writing code
df=cust_tracking
window_spec = Window.orderBy("cust_id","timestamp")

df=df.withColumn("next",lead("timestamp",1).over