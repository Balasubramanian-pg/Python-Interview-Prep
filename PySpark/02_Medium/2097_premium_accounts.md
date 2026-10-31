# StrataScratch Question ID: 2097 - Premium Accounts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2097` |
| **Title** | **Premium Accounts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2097) |

---

## 1. Problem Description

You have a dataset that records daily active users for each premium account. A premium account appears in the data every day as long as it remains premium. However, some premium accounts may be temporarily discounted, meaning they are not actively paying—this is indicated by a final_price of 0.


For each of the first 7 available dates in the dataset, count the number of premium accounts that were actively paying on that day. Then, track how many of those same accounts are still premium and actively paying exactly 7 days later, based solely on their status on that 7th day (i.e., both dates must exist in the dataset). Accounts are only counted if they appear in the data on both dates.


Output three columns:
•   The date of initial calculation.
•   The number of premium accounts that were actively paying on that day.
•   The number of those accounts that remain premium and are still paying after 7 days.

---

## 2. Input Tables & Schema

```text
Table
premium_accounts_by_day
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

entry_date	premium_paid_accounts	premium_paid_accounts_after_7d
2022-02-07	2	2
2022-02-08	3	2
2022-02-09	3	2
2022-02-10	4	3
2022-02-11	4	1
premium_accounts_by_day
Preview
account_id	entry_date	users_visited_7d	final_price	plan_size
A01	2022-02-07	1	100	10
A03	2022-02-07	30	400	50
A01	2022-02-08	3	100	10
A03	2022-02-08	39	400	50
A05	2022-02-08	14	400	50
A01	2022-02-09	12	100	10
A03	2022-02-09	44	400	50
A04	2022-02-09	25	0	70
A05	2022-02-09	32	400	50
A01	2022-02-10	17	100	10
A02	2022-02-10	82	800	100
A03	2022-02-10	60	400	50
A04	2022-02-10	72	0	70
A05	2022-02-10	45	400	50
A01	2022-02-11	26	100	1