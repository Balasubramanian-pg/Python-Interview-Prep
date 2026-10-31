# StrataScratch Question ID: 10134 - Spam Posts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10134` |
| **Title** | **Spam Posts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10134) |

---

## 1. Problem Description

Calculate the percentage of spam posts in all viewed posts by day. Note that the facebook_posts table stores all posts posted by users. The facebook_post_views table is an action table denoting if a user has viewed a post.

---

## 2. Input Tables & Schema

```text
<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime

<facebook_post_views>
post_id                 int
viewer_id               int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting lar