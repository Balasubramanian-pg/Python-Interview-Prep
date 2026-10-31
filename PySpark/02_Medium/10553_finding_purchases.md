# StrataScratch Question ID: 10553 - Finding Purchases

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10553` |
| **Title** | **Finding Purchases** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Amazon** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10553) |

---

## 1. Problem Description

Solve the 'Finding Purchases' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
Table
amazon_transactions
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

user_id
100
103
105
109
110
amazon_transactions
Preview
id	user_id	item	created_at	revenue
1	109	milk	2020-03-03	123
2	139	biscuit	2020-03-18	421
3	120	milk	2020-03-18	176
4	108	banana	2020-03-18	862
5	130	milk	2020-03-28	333
6	103	bread	2020-03-29	862
7	122	banana	2020-03-07	952
8	125	bread	2020-03-13	317
9	139	bread	2020-03-30	929
10	141	banana	2020-03-17	812
11	116	bread	2020-03-31	226
12	128	bread	2020-03-04	112
13	146	biscuit	2020-03-04	362
14	119	banana	2020-03-28	127
15	142	bread	2020-03-09	503
16	122	bread	2020-03-06	593
17	128	biscuit	2020-03-24	160
18	112	banana	2020-03-24	262
19	149	banana	2020-03-29	382
20	100	banana	2020-03-18	599
21	130	milk	2020-03-16	604
22	103	milk	2020-03-31	290
23	112	banana	2020-03-23	523
24	102	bread	2020-03-25	325
25	120	biscuit	2020-03-21	858
26	109	bread	2020-03-22	432
27	101	milk	2020-03-01	449
28	138	milk	2020-03-19	961
29	100	milk	2020-03-29	410
30	129	milk	2020-03-02	771
31	123	milk	2020-03-31	434
32	104	biscuit	2020-03-31	957
33	110	bread	2020-03-13	210
34	143	bread	2020-03-27	870
35	130	milk	2020-03-12	176
36	128	milk	2020-03-28	498
37	133	banana	2020-03-21	837
38	150	banana	2020-03-20	927
39	120	milk	2020-03-27	793
40	109	bread	2020