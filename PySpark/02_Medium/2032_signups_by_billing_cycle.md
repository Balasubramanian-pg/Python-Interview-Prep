# StrataScratch Question ID: 2032 - Signups By Billing Cycle

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2032` |
| **Title** | **Signups By Billing Cycle** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2032) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Signups By Billing Cycle.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2032.
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

# here we will join both tables.
joined_df = signups.join(
    plans,
    signups['plan_id'] == plans['id'],
    "inner"
    ).select(
        "signup_start_date",
        "billing_cycle"
    )
    
    
# here we assign number to week days.
weekday_df = joined_df.withColumn("number_of_day", F.dayofweek(F.col('signup_start_date'))-1)

# now we use pivot . and finsl output as bussiness requirements
pivot_df  = weekday_df.groupBy('number_of_day').pivot('billing_cycle',["monthly","quarterly","annual"]).agg(F.count("billing_c