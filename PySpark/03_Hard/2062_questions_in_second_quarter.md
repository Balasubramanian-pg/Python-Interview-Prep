# StrataScratch Question ID: 2062 - Questions In Second Quarter

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2062` |
| **Title** | **Questions In Second Quarter** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2062) |

---

## 1. Problem Description

How many searches were there in the second quarter of 2021?

---

## 2. Input Tables & Schema

```text
<fb_searches>
date            datetime
search_id       int
user_id         int
age_group       varchar
search_query    varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to o