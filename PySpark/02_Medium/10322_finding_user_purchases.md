# StrataScratch Question ID: 10322 - Finding User Purchases

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10322` |
| **Title** | **Finding User Purchases** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Amazon** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10322) |

---

## 1. Problem Description

Write a query that'll identify returning active users. 
A returning active user is a user that has made a second purchase within 7 days of any other of their purchases. Output a list of user_ids of these returning active users.

---

## 2. Input Tables & Schema

```text
<amazon_transactions>
id                      int
user_id                 int
item                    varchar
created_at              datetime
revenue                 int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.