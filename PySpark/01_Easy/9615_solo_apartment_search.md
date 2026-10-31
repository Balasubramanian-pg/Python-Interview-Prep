# StrataScratch Question ID: 9615 - Solo Apartment Search

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9615` |
| **Title** | **Solo Apartment Search** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9615) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Solo Apartment Search.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9615.
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
airbnb_search_details = airbnb_search_details.filter(
    (F.col('property_type') == 'Apartment' ) & 
    (F.col('accommodates') == 1 )
)


airbnb_search_details.toPandas()

# We used .filter() instead of .groupBy() because the goal was 'Details'.
# Filtering keeps the original