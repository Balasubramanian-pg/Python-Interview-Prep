# StrataScratch Question ID: 2003 - Recent Refinance Submissions

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2003` |
| **Title** | **Recent Refinance Submissions** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2003) |

---

## 1. Problem Description

Write a query that joins this submissions table to the loans table and returns the total loan balance on each user’s most recent ‘Refinance’ submission. Return all users and the balance for each of them.

---

## 2. Input Tables & Schema

```text
<loans>
id              int
user_id         int
created_at      datetime
status          varchar
type            varchar

<submissions>
id              int
balance         float
interest_rate   float
rate_type       varchar
loan_id         int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid co