# StrataScratch Question ID: 10183 - Total Cost Of Orders

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10183` |
| **Title** | **Total Cost Of Orders** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10183) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Total Cost Of Orders.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10183.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query executio