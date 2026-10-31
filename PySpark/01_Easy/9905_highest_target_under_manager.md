# StrataScratch Question ID: 9905 - Highest Target Under Manager

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9905` |
| **Title** | **Highest Target Under Manager** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Salesforce** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9905) |

---

## 1. Problem Description

Solve the 'Highest Target Under Manager' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
Table
salesforce_employees
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

first_name	target
Nicky	400
Steve	400
David	400
salesforce_employees
Preview
id	first_name	last_name	age	sex	employee_title	department	salary	target	bonus	email	city	address	manager_id
1	Allen	Wang	55	F	Manager	Management	200000	600	300	Allen@company.com	California	1069 Ventura Drive	1
20	Sarrah	Bicky	31	F	Senior Sales	Sales	2000	500	150	Sarrah@company.com	Florida	1176 Tyler Avenue	19
7	Nicky	Bat	33	F	Sales	Sales	1400	400	100	Molly@company.com	Arizona	3461 Preston Street	13
31	Steve	Smith	39	M	Sales	Sales	1500	400	125	steve@company.com	Texas		13
32	David	Warner	38	M	Sales	Sales	1200	400	150	david@company.com	Florida		13
17	Mick	Berry	44	M	Senior Sales	Sales	2200	400	150	Mick@company.com	Florida		11
24	Adam	Morris	30	M	Sales	Sales	1300	400	100	Adam@company.com	Alabama	4541 Ferry Street	19
2	Joe	Jack	32	M	Sales	Sales	1000	200	150	Joe@company.com	California	995 Jim Rosa Lane	1
3	Henry	Ted	31	M	Senior Sales	Sales	2000	200	150	Henry@company.com	California	1609 Ford Street	1
5	Max	George	26	M	Sales	Sales	1300	200	150	Max@company.com	California	2638 Richards Avenue	1
9	Monika	William	33	F	Sales	Sales	1000	200	100	Molly@company.com	Alabama		13
10	Jennifer	Dion	34	F	Sales	Sales	1000	200	150	Jennifer@company.com	Alabama		13
12	Shandler	Bing	23	M	Auditor	Audit	1100	200	150	Shandler@company.com	Arizona		11
14	Jason	Tom	23	M	Auditor	Audit	1000	200	150	Jason@company.com	Arizona		11
16	Celine	Anston	27	F	Auditor	Audit	1000	200	150	Celine@company.com	Colorado		11
18	Laila	Mark	26	F	Sales	Sales	1000	200	150	Laila@company.com	Florida	3655 Spirit Drive	11
21	Suzan	Lee	34	F	Sales	Sales	1300	200	150	Suzan@company.com	Florida	1275 Monroe Avenue	19
22	Mandy	John	31	F	Sales	Sales	1300	200	150	Mandy@company.com	Florida	2510 Maryland Avenue	19
23	Britney	Berry	45	F	Sales	Sales	1200	200	100	Britney@company.com	Florida	3946 Steve Hunt Road	19
25	Jack	Mick	29	M	Sales	Sales	1300	200	100	Jack@company.com	Hawaii	3762 Stratford Drive	19
27	Tom	Fridy	32	M	Sales	Sales	1200	200	150	Tom@company.com	Hawaii	801 Stratford Drive	1
28	Morgan	Matt	25	M	Sales	Sales	1200	200	150	Morgan@company.com	Hawaii	2641 Randall Drive	1
30	Mark	Jon	28	M	Sales	Sales	1200	200	150	Mark@company.com	Alabama	2522 George Avenue	1
29	Antoney	Adam	34	M	Sales	Sales	1300	180	150	Antoney@company.com	Hawaii	3533 Randall Drive	1
15	Michale	Jackson	44	F	Auditor	Audit	700	150	150	Michale@company.com	Colorado		11
26	Ben	Ten	43	M	Sales	Sales	1300	150	100	Ben@company.com	Hawaii	3055 Indiana Avenue	19
8	John	Ford	26	M	Senior Sales	Sales	1500	140	100	Molly@company.com	Alabama	4832 New Creek Road	13
4	Sam	Mark	25	M	Sales	Sales	1000	120	150	Sam@company.com	California	4869 Libby Street	1
6	Molly	Sam	28	F	Sales	Sales	1400	100	150	Molly@company.com	Arizona	3632 Polk Street	13
11	Richerd	Gear	57	M	Manager	Management	250000	0	300	Richerd@company.com	Alabama		1
13	Katty	Bond	56	F	Manager	Management	150000	0	300	Katty@company.com	Arizona		1
19	George	Joe	50	M	Manager	Management	100000	0	300	George@company.com	Florida	1003 Wyatt Street	1
id:
bigint
first_name:
string
last_name:
string
age:
bigint
sex:
string
employee_title:
string
department:
string
salary:
bigint
target:
bigint
bonus:
bigint
email:
string
city:
string
address:
string
manager_id:
bigint
```

---
