# StrataScratch Question ID: 10164 - Total Adwords Earnings

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10164` |
| **Title** | **Total Adwords Earnings** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10164) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Total AdWords Earnings.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10164.
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
google_adwords_earnings = google_adwords_earnings.groupBy('business_type').agg(F.sum('adwords_earnings').alias('total earnings'))
 
# To validate your solution, convert your final pySpark df to a pandas df
google_adwords_earni