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
str