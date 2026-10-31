# StrataScratch Question ID: 9909 - Highest Number Of Orders

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9909` |
| **Title** | **Highest Number Of Orders** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9909) |

---

## 1. Problem Description

Find the customer who has placed the highest number of orders. Output the id of the customer along with the corresponding number of orders.

---

## 2. Input Tables & Schema

```text
Table
orders
More about this question
Hints
Expected Output
orders
Preview
id	cust_id	order_date	order_details	total_order_cost
1	3	2019-03-04	Coat	100
2	3	2019-03-01	Shoes	80
3	3	2019-03-07	Skirt	30
4	7	2019-02-01	Coat	25
5	7	2019-03-10	Shoes	80
6	15	2019-02-01	Boats	100
7	15	2019-01-11	Shirts	60
8	15	2019-03-11	Slipper	20
9	15	2019-03-01	Jeans	80
10	15	2019-03-09	Shirts	50
11	5	2019-02-01	Shoes	80
12	12	2019-01-11	Shirts	60
13	12	2019-03-11	Slipper	20
14	4	2019-02-01	Shoes	80
15	4	2019-01-11	Shirts	60
16	3	2019-04-19	Shirts	50
17	7	2019-04-19	Suit	150
18	15	2019-04-19	Skirt	30
19	15	2019-04-20	Dresses	200
20	12	2019-01-11	Coat	125
21	7	2019-04-01	Suit	50
22	7	2019-04-02	Skirt	30
23	7	2019-04-03	Dresses	50
24	7	2019-04-04	Coat	25
25	7	2019-04-19	Coat	125
26	3	2019-04-20	Gloves	20
27	3	2019-04-21	Tie	25
28	3	2019-04-22	Cap	15
29	3	2019-04-23	Jacket	120
30	1	2019-04-19	Jacket	150
31	1	2019-04-19	Shoes 	125
id:
bigint
cust_id:
bigint
order_date:
date
order_details:
string
total_order_cost:
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
