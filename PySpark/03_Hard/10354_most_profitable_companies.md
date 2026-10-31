# StrataScratch Question ID: 10354 - Most Profitable Companies

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10354` |
| **Title** | **Most Profitable Companies** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10354) |

---

## 1. Problem Description

Find the 3 most profitable companies in the entire world.
Output the result along with the corresponding company name.
Sort the result based on profits in descending order.

---

## 2. Input Tables & Schema

```text
(forbes_global_2010_2014)
company         varchar
sector          varchar
industry        varchar
continent       varchar
country         varchar
marketvalue     float
sales           float
profits         float
assets          float
rank            int
forbeswebpage   varchar
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
# SELECT company, profits
FROM (
    SELECT company, 
           profits, 
           RANK() OVER(ORDER BY profits DESC) AS profits_rank
    FROM forbes_global_2010_2014
) AS ra