# StrataScratch Question ID: 10077 - Income By Title And Gender

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10077` |
| **Title** | **Income By Title And Gender** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Salesforce** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10077) |

---

## 1. Problem Description

Find the average total compensation based on employee titles and gender. Total compensation is calculated by adding both the salary and bonus of each employee. However, not every employee receives a bonus so disregard employees without bonuses in your calculation. Employee can receive more than one bonus.
Output the employee title, gender (i.e., sex), along with the average total compensation.

---

## 2. Input Tables & Schema

```text
Tables
sf_employee
sf_bonus
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

employee_title	sex	avg_total_comp
Senior Sales	M	5350
Sales	M	4600
Manager	F	209500
Auditor	M	2200
sf_employee
Preview
id	first_name	last_name	age	sex	employee_title	department	salary	target	email	city	address	manager_id
5	Max	George	26	M	Sales	Sales	1300	200	Max@company.com	California	2638 Richards Avenue	1
13	Katty	Bond	56	F	Manager	Management	150000	0	Katty@company.com	Arizona		1
11	Richerd	Gear	57	M	Manager	Management	250000	0	Richerd@company.com	Alabama		1
10	Jennifer	Dion	34	F	Sales	Sales	1000	200	Jennifer@company.com	Alabama		13
19	George	Joe	50	M	Manager	Management	100000	0	George@company.com	Florida	1003 Wyatt Street	1
18	Laila	Mark	26	F	Sales	Sales	1000	200	Laila@company.com	Florida	3655 Spirit Drive	11
20	Sarrah	Bicky	31	F	Senior Sales	Sales	2000	200	Sarrah@company.com	Florida	1176 Tyler Avenue	19
21	Suzan	Lee	34	F	Sales	Sales	1300	200	Suzan@company.com	Florida	1275 Monroe Avenue	19
22	Mandy	John	31	F	Sales	Sales	1300	200	Mandy@company.com	Florida	2510 Maryland Avenue	19
23	Britney	Berry	45	F	Sales	Sales	1200	200	Britney@company.com	Florida	3946 Steve Hunt Road	19
25	Jack	Mick	29	M	Sales	Sales	1300	200	Jack@company.com	