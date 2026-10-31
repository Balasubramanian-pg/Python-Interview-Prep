# StrataScratch Question ID: 2032 - Signups By Billing Cycle

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2032` |
| **Title** | **Signups By Billing Cycle** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2032) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Signups By Billing Cycle.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2032.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy