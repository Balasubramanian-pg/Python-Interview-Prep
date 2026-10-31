# StrataScratch Question ID: 9924 - Email Preference Missing

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9924` |
| **Title** | **Email Preference Missing** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9924) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Email Preference Missing.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9924.
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

# Start writing code
library_usage = library_usage.filter((F.col('circulation_active_year') == 2016) & ( F.col("provided_email_address") == False) & ( F.col("notice_preference_definition") == 'email'))

library_usage = library_usage.select(F.col('home_library_code'))
# To validate your solution, convert your final pySpark df to a pandas df
library_usage.toPandas()

# here we use filter instead g