# StrataScratch Question ID: 10315 - Cities With The Most Expensive Homes

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10315` |
| **Title** | **Cities With The Most Expensive Homes** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10315) |

---

## 1. Problem Description

Write a query that identifies cities with higher than average home prices when compared to the national average. Output the city names.

---

## 2. Input Tables & Schema

```text
<zillow_transactions>
id                  int
state               varchar
city                varchar
street_address      varchar
mkt_price           int
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
# -- logic: we need to find the national average of houses
-- we need to find the average home prices by city for comparison
-- filter for cities that > national average
-- return city names `city`

-- subquery
-- we only need the city name
SELECT city
FROM zillow_transactions
GROUP BY 1
-- agg avg func > the avg nation wide
HAVING AVG(mkt_price) > (
    SELECT AVG(mkt_price)
    FROM zillow_transactions
)
-- just returning back the city in desc order of avg cost
ORDER BY AVG(mkt_price) DESC;
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql