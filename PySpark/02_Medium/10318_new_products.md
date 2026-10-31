# StrataScratch Question ID: 10318 - New Products

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10318` |
| **Title** | **New Products** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10318) |

---

## 1. Problem Description

Calculate the net change in the number of products launched by companies in 2020 compared to 2019. Your output should include the company names and the net difference.
(Net difference = Number of products launched in 2020 - The number launched in 2019.)

---

## 2. Input Tables & Schema

```text
[car_launches]
year                    int
company_name            varchar
product_name            varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optim