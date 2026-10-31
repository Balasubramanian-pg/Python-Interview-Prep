# StrataScratch Question ID: 2125 - Process A Refund

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2125` |
| **Title** | **Process A Refund** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2125) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Process a Refund.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2125.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Wi