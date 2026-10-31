# StrataScratch Question ID: 2062 - Questions In Second Quarter

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2062` |
| **Title** | **Questions In Second Quarter** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2062) |

---

## 1. Problem Description

How many searches were there in the second quarter of 2021?

---

## 2. Input Tables & Schema

```text
<fb_searches>
date            datetime
search_id       int
user_id         int
age_group       varchar
search_query    varchar
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
# -- logic: find quarter for date and ensure we are looking into year 2021, simple group by count thereafter

-- we only want the result
SELECT result
FROM (
    -- getting the quarter and group by
    SELECT EXTRACT(QUARTER FROM date), COUNT(*) AS result
    FROM fb_searches
    -- ensure that we are only finding 2nd quarter and year 2021
    WHERE EXTRACT(QUARTER FROM date) = 2 AND EXTRACT(YEAR FROM date) = '2021'
    GROUP BY 1
) count_by_quarter
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession
