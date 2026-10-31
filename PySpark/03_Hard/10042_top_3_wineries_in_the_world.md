# StrataScratch Question ID: 10042 - Top 3 Wineries In The World

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10042` |
| **Title** | **Top 3 Wineries In The World** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `String & Text Processing` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10042) |

---

## 1. Problem Description

Find the top 3 wineries in each country based on the average points earned. In case there is a tie, order the wineries by winery name in ascending order. Output the country along with the best, second best, and third best wineries. If there is no second winery (NULL value) output 'No second winery' and if there is no third winery output 'No third winery'. For outputting wineries format them like this: "winery (avg_points)"

---

## 2. Input Tables & Schema

```text
(winemag_p1)
id              int
country         varchar
description     varchar
designation     varchar
points          int
price           float
province        varchar
region_1        varchar
region_2        varchar
variety         varchar
winery          varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations 