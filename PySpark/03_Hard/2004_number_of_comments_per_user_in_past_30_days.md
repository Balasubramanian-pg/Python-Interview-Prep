# StrataScratch Question ID: 2004 - Number Of Comments Per User In Past 30 Days

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2004` |
| **Title** | **Number Of Comments Per User In Past 30 Days** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2004) |

---

## 1. Problem Description

Return the total number of comments received for each user in the last 30 days. Assume today is 2020-02-10.

---

## 2. Input Tables & Schema

```text
<fb_comments_count>
user_id             int
created_at          datetime
number_of_comments  int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization