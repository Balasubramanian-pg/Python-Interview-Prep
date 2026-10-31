# StrataScratch Question ID: 2033 - Find The Most Profitable Location

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2033` |
| **Title** | **Find The Most Profitable Location** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2033) |

---

## 1. Problem Description

Find the most profitable location. Write a query that calculates the average signup duration and average revenue for each location, and then compare these two measures together by taking the ratio of the average revenue and average duration for each location.

Your output should include the location, average duration, average revenue, and ratio. Sort your results from highest ratio to lowest.

---

## 2. Input Tables & Schema

```text
<signups>
signup_id               int
signup_start_date       datetime
signup_stop_date        datetime
plan_id                 int
location                varchar

<transactions>
transaction_id          int
signup_id               int
transaction_start_date  datetime
amt                     float
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimiz