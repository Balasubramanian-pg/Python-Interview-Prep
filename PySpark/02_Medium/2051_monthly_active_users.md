# StrataScratch Question ID: 2051 - Monthly Active Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2051` |
| **Title** | **Monthly Active Users** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2051) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Monthly Active Users.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2051.
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

# 1st we filter data and take required (january 2021) data only
sf_events = sf_events.filter((F.col('record_date')>='2021-01-01') & (F.col('record_date')<='2021-01-31'))
 
# We count the unique users found within that account's January data.
monthly_count = sf_events.groupBy('account_id').agg(F.countDistinct('user_id')).alias("CountDatewise")

# To validate your soluti