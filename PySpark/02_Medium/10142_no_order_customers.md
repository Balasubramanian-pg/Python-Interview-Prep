# StrataScratch Question ID: 10142 - No Order Customers

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10142` |
| **Title** | **No Order Customers** |
| **Difficulty** | `Medium` |
| **Company Tag** | **City of Los Angeles** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10142) |

---

## 1. Problem Description

Include:


•    Customers who placed orders only outside this date range.
•    Customers who never placed any orders.


Output the customers' first names.

---

## 2. Input Tables & Schema

```text
Tables
customers
orders
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

first_name
Jack
Justin
Mark
Lili
Eva
customers
Preview
id	first_name	last_name	city	address	phone_number
8	John	Joseph	San Francisco		928-386-8164
7	Jill	Michael	Austin		813-297-0692
4	William	Daniel	Denver		813-368-1200
5	Henry	Jackson	Miami		808-601-7513
13	Emma	Isaac	Miami		808-690-5201
14	Liam	Samuel	Miami		808-555-5201
15	Mia	Owen	Miami		808-640-5201
1	Mark	Thomas	Arizona	4476 Parkway Drive	602-993-5916
12	Eva	Lucas	Arizona	4379 Skips Lane	301-509-8805
6	Jack	Aiden	Arizona	4833 Coplin Avenue	480-303-1527
2	Mona	Adrian	Los Angeles	1958 Peck Court	714-409-9432
10	Lili	Oliver	Los Angeles	3832 Euclid Avenue	530-695-1180
3	Farida	Joseph	San Francisco	3153 Rhapsody Street	813-368-1200
9	Justin	Alexander	Denver	4470 McKinley Avenue	970-433-7589
11	Frank	Jacob	Miami	1299 Randall Drive	808-590-5201
id:
bigint
first_name:
string
last_name:
string
city:
string
address:
string
phone_number:
string
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
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.