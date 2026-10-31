# StrataScratch Question ID: 10006 - Find The Averag Distance Traveled In Each Hour

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10006` |
| **Title** | **Find The Averag Distance Traveled In Each Hour** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10006) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the averag distance traveled in each hour.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10006.
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
lyft_rides = lyft_rides.groupBy('hour').agg(F.avg('travel_distance').alias('average')).orderBy(F.col('hour').asc())


lyft_rides = lyft_rides.select('hour','average')

# To validate your solution, convert your final py