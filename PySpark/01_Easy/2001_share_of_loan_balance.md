# StrataScratch Question ID: 2001 - Share Of Loan Balance

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2001` |
| **Title** | **Share Of Loan Balance** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2001) |

---

## 1. Problem Description

Write a query that returns the rate_type, loan_id and balance of each loan type, and a column that shows what percentage of the submission’s total balance each loan constitutes.

---

## 2. Input Tables & Schema

```text
<submissions>
id                      int
balance                 float
interest_rate           float
rate_type               varchar
loan_id                 int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculat