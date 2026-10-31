# StrataScratch Question ID: 9614 - Find The Average Difference Between Booking And Check-in Dates

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9614` |
| **Title** | **Find The Average Difference Between Booking And Check-in Dates** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9614) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the average difference between booking and check-in dates.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9614.
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

# we filter data on the basis of our requirement.
refined_df = airbnb_contacts.filter(F.col("ts_booking_at").isNotNull())

# modify one column schema and calculate different .
day_gap_df = refined_df.withColumn("booking_date",F.to_date(F.col("ts_booking_at"))).withColumn("day_diff",F.datediff(F.col("ds_checkin"),F.col("booking_date")))

# here we select the data which required for business
final_df = day_gap_df.groupBy("id_host").agg(F.avg('day_diff').alias("avg_days_between