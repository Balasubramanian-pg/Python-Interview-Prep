# StrataScratch Question ID: 10351 - Activity Rank

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10351` |
| **Title** | **Activity Rank** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Google** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10351) |

---

## 1. Problem Description

Find the email activity rank for each user. Email activity rank is defined by the total number of emails sent. The user with the highest number of emails sent will have a rank of 1, and so on. Output the user, total emails, and their activity rank. Order records by the total emails in descending order. Sort users with the same number of emails in alphabetical order.
In your rankings, return a unique value (i.e., a unique rank) even if multiple users have the same number of emails.

---

## 2. Input Tables & Schema

```text
<google_gmail_emails>
id                      int
from_user               varchar
to_user                 varchar
day                     int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter dow