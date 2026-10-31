# StrataScratch Question ID: 10068 - User Email Labels

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10068` |
| **Title** | **User Email Labels** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10068) |

---

## 1. Problem Description

Find the number of emails received by each user under each built-in email label. The email labels are: 'Promotion', 'Social', and 'Shopping'. Output the user along with the number of promotion, social, and shopping mails count,.

---

## 2. Input Tables & Schema

```text
(google_gmail_emails)
id                      int
from_user               varchar
to_user                 varchar
day                     int
(google_gmail_labels)
email_id                int
label                   varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utiliz