# StrataScratch Question ID: 2018 - Inactive Free Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2018` |
| **Title** | **Inactive Free Users** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2018) |

---

## 1. Problem Description

Return a list of users with status free who didn’t make any calls in Apr 2020.

Table:
<rc_calls>
user_id         int
date            datetime
call_id         int

<rc_users>
user_id         int
status          varchar
company_id      int

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2018.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`