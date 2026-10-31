# StrataScratch Question ID: 9762 - Find The Day Of The Week That Most People Check In

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9762` |
| **Title** | **Find The Day Of The Week That Most People Check In** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9762) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the day of the week that most people check in.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9762.
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
import pyspark
from pyspark.sql import functions as F

# here we find out particular day as per date.
day_list_df = airbnb_contacts.withColumn(
    "week_days",
    F.date_format(F.col("ds_checkin"), 'UUUU')
)


# final output
final_count_df = (
    day_list_df
    .groupBy("week_days")
    .agg(F.count('*') .alias ("check-in count"))
    .orderBy(F.desc('check-in count'))
)
