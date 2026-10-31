# StrataScratch Question ID: 2006 - Users Activity Per Month Day

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2006` |
| **Title** | **Users Activity Per Month Day** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2006) |

---

## 1. Problem Description

Return a distribution of users activity per day of the month

Table:
<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2006.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst O