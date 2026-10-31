# StrataScratch Question ID: 2019 - Top 2 Users With Most Calls

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2019` |
| **Title** | **Top 2 Users With Most Calls** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2019) |

---

## 1. Problem Description

Return the top 2 users in each company that called the most. Output the company_id, user_id, and the user's rank. If there are multiple users in the same rank, keep all of them.

---

## 2. Input Tables & Schema

```text
<rc_calls>
user_id     int
datedate    time
call_id     int

<rc_users>
user_id     int
status      varchar
company_id  int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define exp