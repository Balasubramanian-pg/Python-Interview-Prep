# StrataScratch Question ID: 10148 - Find The Top 5 Cities With The Most 5 Star Businesses

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10148` |
| **Title** | **Find The Top 5 Cities With The Most 5 Star Businesses** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10148) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the top 5 cities with the most 5 star businesses.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10148.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations until final aggregations.

---

## 4. PySpark DataFrame API Solution

```python
# Import your libraries
from pyspark.sql import functions as F
from pyspark.sql.window import Window

# we filter out only required data and make partition of it.and count it city wise.
stars_filter_df = (
    yelp_business.filter(F.col("stars") == 5)
    .groupBy('city')
    .agg(F.count("business_id").alias("n_counts"))
)

# using window we arrange above count as descending form
window_rank_df = Window.orderBy(F.desc("n_counts"))

# as per position we provide rank them 
yelp_business_df = (
    stars_filter_df
    .withColumn('rank', F.rank().over