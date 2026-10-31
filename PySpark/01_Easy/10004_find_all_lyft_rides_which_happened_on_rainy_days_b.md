# StrataScratch Question ID: 10004 - Find All Lyft Rides Which Happened On Rainy Days Before Noon

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10004` |
| **Title** | **Find All Lyft Rides Which Happened On Rainy Days Before Noon** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Lyft** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10004) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find all Lyft rides which happened on rainy days before noon.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10004.
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

# we need to only filter out data as per bussiness requirements . that why we use filter only
lyft_rides = lyft_rides.filter((F.lower(F.col('weather')) == 'rainy') & (F.col('hour') < 12))

# To validate your solution, convert you