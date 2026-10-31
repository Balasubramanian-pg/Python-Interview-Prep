# StrataScratch Question ID: 2012 - Viewers Turned Streamers

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2012` |
| **Title** | **Viewers Turned Streamers** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2012) |

---

## 1. Problem Description

From users who had their first session as a viewer, how many streamer sessions have they had? Return the user id and number of sessions in descending order. In case there are users with the same number of sessions, order them by ascending user id.

---

## 2. Input Tables & Schema

```text
<twitch_sessions<
user_id                     int
session_start               datetime
session_end                 datetime
session_id                  int
session_type                varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations until final aggregation