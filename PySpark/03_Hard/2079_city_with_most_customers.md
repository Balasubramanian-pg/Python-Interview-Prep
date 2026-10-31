# StrataScratch Question ID: 2079 - City With Most Customers

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2079` |
| **Title** | **City With Most Customers** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Lyft** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2079) |

---

## 1. Problem Description

For each city, find the number of rides in August 2021 that were not paid for using promotional codes. 
Output the city or cities where this number was the highest.

---

## 2. Input Tables & Schema

```text
(lyft_orders)
order_id                int
customer_id             varchar
driver_id               varchar
country                 varchar
city                    varchar

(lyft_payments)
order_id                int
order_date              datetime
promo_code              bool
order_fare              float
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed