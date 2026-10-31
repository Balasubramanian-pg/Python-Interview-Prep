# StrataScratch Question ID: 10296 - Meta/facebook Accounts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10296` |
| **Title** | **Meta/facebook Accounts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10296) |

---

## 1. Problem Description

Calculate the ratio of accounts closed on January 10th, 2020 using the fb_account_status

---

## 2. Input Tables & Schema

```text
table.

Table
fb_account_status
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

CLOSED_RATIO
0.45
fb_account_status
Preview
acc_id	status_date	status
3	2019-12-23	closed
4	2020-01-03	open
4	2020-01-07	open
4	2020-01-10	open
6	2019-12-26	closed
6	2020-01-05	closed
6	2020-01-11	closed
7	2019-12-28	closed
10	2020-01-15	open
13	2020-01-13	closed
18	2020-01-10	open
19	2019-12-16	open
21	2020-01-11	closed
22	2019-12-22	open
22	2019-12-29	closed
22	2020-01-04	closed
23	2019-12-30	closed
23	2020-01-10	closed
25	2020-01-13	closed
27	2019-12-15	open
27	2020-01-08	open
28	2019-12-18	closed
31	2020-01-08	open
32	2019-12-17	closed
33	2019-12-26	open
33	2020-01-10	closed
33	2020-01-14	closed
34	2019-12-22	open
34	2020-01-10	open
34	2020-01-14	closed
36	2019-12-20	closed
36	2020-01-03	closed
36	2020-01-09	open
37	2019-12-29	closed
37	2020-01-11	open
38	2019-12-27	open
39	2019-12-31	open
42	2019-12-17	closed
42	2019-12-27	open
43	2020-01-11	open
47	2019-12-16	open
47	2019-12-19	closed
47	2019-12-27	open
48	2019-12-17	open
49	2019-12-28	open
49	2020-01-04	closed
50	2020-01-03	closed
51	2019-12-27	closed
52	2020-01-10	open
54	2019-12-17	closed
55	2019-12-22	closed
56	2020-01-06	open
56	2020-01-12	closed
59	2020-01-11	open
59	2020-01-15	open
64	2020-01-07	open
65	2020-01-09	open
66	2019-12-30	open
66	2020-01-01	open
68	2019-12-18	closed
68	2020-01-11	open
69	2019-12-26	open
69	2019-12-28	closed
71	2020-01-13	closed
72	2019-12-16	open
72	2020-01-08	closed
72	2020-01-12	open
73	2020-01-03	open
74	2019-12-16	open
75	2020-01-10	closed
78	2019-12-25	open
79	2020-01-03	closed
80	2019-12-24	open
80	2020-01-15	closed
81	2019-12-17	closed
81	2020-01-01	open
82	2019-12-15	open
82	2019-12-22	closed
82	2020-01-07	open
84	2020-01-12	open
85	2019-12-15	open
85	2019-12-25	closed
86	2019-12-31	open
86	2020-01-05	closed
87	2020-01-03	closed
88	2019-12-15	open
88	2019-12-28	open
88	2020-01-10	closed
88	2020-01-15	open
89	2019-12-27	closed
90	2019-12-30	open
90	2020-01-06	closed
90	2020-01-10	closed
91	2019-12-20	closed
93	2019-12-30	closed
94	2020-01-03	open
94	2020-01-10	open
96	2020-01-10	open
98	2019-12-19	closed
acc_id:
bigint
status_date:
date
status:
string
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations ar