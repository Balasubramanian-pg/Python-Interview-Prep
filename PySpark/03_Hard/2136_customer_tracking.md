# StrataScratch Question ID: 2136 - Customer Tracking

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2136` |
| **Title** | **Customer Tracking** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Amazon** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2136) |

---

## 1. Problem Description

Shopify
Amazon


Data Engineer
Data Scientist
BI Analyst
Data Analyst
ML Engineer
Given the users' sessions logs on a particular day, calculate how many hours each user was active that day.


Note: The session starts when state=1 and ends when state=0.

---

## 2. Input Tables & Schema

```text
Table: cust_tracking
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

cust_id	sum(time_diff)
c001	5
c002	4.5
c003	1.5
c004	2
c005	7.5
cust_tracking
Preview
cust_id	state	timestamp
c001	1	2024-11-26 07:00:00
c001	0	2024-11-26 09:30:00
c001	1	2024-11-26 12:00:00
c001	0	2024-11-26 14:30:00
c002	1	2024-11-26 08:00:00
c002	0	2024-11-26 09:30:00
c002	1	2024-11-26 11:00:00
c002	0	2024-11-26 12:30:00
c002	1	2024-11-26 15:00:00
c002	0	2024-11-26 16:30:00
c003	1	2024-11-26 09:00:00
c003	0	2024-11-26 10:30:00
