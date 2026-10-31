# StrataScratch Question ID: 10300 - Premium Vs Freemium

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10300` |
| **Title** | **Premium Vs Freemium** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Microsoft** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10300) |

---

## 1. Problem Description

Find the total number of downloads for paying and non-paying users by date. Include only records where non-paying customers have more downloads than paying customers. The output should be sorted by earliest date first and contain 3 columns date, non-paying downloads, paying downloads.

---

## 2. Input Tables & Schema

```text
<ms_user_dimension>
user_id             int
acc_id              int

ms_acc_dimension
acc_id              int
paying_customer     varchar

ms_download_facts
2021-10-13          datetime
user_id             int
downloads           int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys 