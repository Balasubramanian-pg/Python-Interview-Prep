# StrataScratch Question ID: 2002 - Submission Types

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2002` |
| **Title** | **Submission Types** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2002) |

---

## 1. Problem Description

Write a query that returns the user ID of all users that have created at least one ‘Refinance’ submission and at least one ‘InSchool’ submission.

---

## 2. Input Tables & Schema

```text
<loans>
id                  int
user_id             int
created_at          datetime
status              varchar
type                varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or wi