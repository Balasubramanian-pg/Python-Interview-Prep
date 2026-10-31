# StrataScratch Question ID: 10324 - Distances Traveled

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10324` |
| **Title** | **Distances Traveled** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Lyft** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10324) |

---

## 1. Problem Description

Find the top 10 users that have traveled the greatest distance. Output their id, name and a total distance traveled.

---

## 2. Input Tables & Schema

```text
<lyft_rides_log>
id              int
user_id         int
distance        int

<lyft_users>
id              int
name            varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames 