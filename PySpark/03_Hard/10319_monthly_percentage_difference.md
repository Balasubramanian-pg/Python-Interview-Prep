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
31