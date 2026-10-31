# StrataScratch Question ID: 9613 - Find The Date With The Highest Opening Stock Price

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9613` |
| **Title** | **Find The Date With The Highest Opening Stock Price** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9613) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find the date with the highest opening stock price.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9613.
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

# here we collect max values at node levels. and collect that rows.
max_val = aapl_historical_stock_price.select(F.max('open')).collect()[0][0]

aapl_historical_stock_price = aapl_historical_stock_price.filter(F.col('open') == max_val ).select ('date')


aapl_historical_stock_price.toPandas()

# if we do sort using desc and limit -> spark do total shuffle over network(moving single