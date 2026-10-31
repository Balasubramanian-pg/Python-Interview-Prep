# StrataScratch Question ID: 2126 - Account Registrations

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2126` |
| **Title** | **Account Registrations** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2126) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Account Registrations.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2126.
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

# add new column for (YYYY-MM) .
noom_signups = noom_signups.withColumn('month_year', F.date_format(F.col('started_at'),'yyyy-MM'))

noom_signups = noom_signups.groupBy('month_year').agg(F.count('signup_id').alias('registration_count'))
# To validate your solution, convert your final pySpark df to a pandas df
noom_signups.toPandas()

# We needed to count how many new accounts were r