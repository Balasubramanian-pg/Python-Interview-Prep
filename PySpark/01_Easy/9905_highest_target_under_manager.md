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
10	Jennifer	Dion	34	F	Sales	Sales	1000	200	150	Jennifer@company.com	