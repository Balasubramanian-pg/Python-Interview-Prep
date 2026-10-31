# StrataScratch Question ID: 10167 - Total Number Of Housing Units

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10167` |
| **Title** | **Total Number Of Housing Units** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10167) |

---

## 1. Problem Description

Find the total number of housing units completed for each year. Output the year along with the total number of housings. Order the result by year in ascending order.

Table:
<housing_units_completed_us>
year            int
month           int
south           float
west            float
midwest         float
northeast       float

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10167.
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
from pyspark.sql.window import Window

# Execute solution using Spark SQL or DataFrame API:
# spark.sql('''
# -- logic:
-- group by year, SUM south west midwest northeast
-- order by year ASC

SELECT year,
       SUM(south + west + midwest + northeast)
FROM housing_units_completed_us