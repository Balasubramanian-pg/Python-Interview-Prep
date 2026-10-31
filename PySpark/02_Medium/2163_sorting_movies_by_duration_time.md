# StrataScratch Question ID: 2163 - Sorting Movies By Duration Time

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2163` |
| **Title** | **Sorting Movies By Duration Time** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Netflix** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2163) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Sorting Movies By Duration Time.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2163.
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
from pyspark.sql.types import IntegerType

# Start writing code
movie_catalogue = movie_catalogue.withColumn("time",F.split(F.col("duration")," ").getItem(0).cast(IntegerType())).orderBy(F.col("time").desc()).drop(F.col("time"))


# To validate your solution, convert your final pySpark df to a pandas df
movie_catalogue.toPandas()



# here we need to rearrange table as per dura