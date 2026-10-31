# StrataScratch Question ID: 2005 - Share Of Active Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2005` |
| **Title** | **Share Of Active Users** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2005) |

---

## 1. Problem Description

Return the share of monthly active users in the United States (US). Active users are the ones with an "open" status in the table.

---

## 2. Input Tables & Schema

```text
<fb_active_users>
user_id             int
name                varchar
status              varchar
country             varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transforma