# StrataScratch Question ID: 2000 - Variable Vs Fixed Rates

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2000` |
| **Title** | **Variable Vs Fixed Rates** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2000) |

---

## 1. Problem Description

Write a query that returns binary description of rate type per loan_id. The results should have one row per loan_id and two columns: for fixed and variable type.

Table:
<submissions>
id                  int
balance             float
interest_rate       float
rate_type           varchar
loan_id             int

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2000.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `fil