# StrataScratch Question ID: 2063 - Change Of Currency Exchange Rates

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2063` |
| **Title** | **Change Of Currency Exchange Rates** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Salesforce** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2063) |

---

## 1. Problem Description

You are given a list of exchange rates from various currencies to US Dollars (USD) in different months. Show how the exchange rate of all the currencies changed in the first half of 2020. Output the currency code and the difference between values of the exchange rate between July 1, 2020 and January 1, 2020.

---

## 2. Input Tables & Schema

```text
<sf_exchange_rate>
source_currency         varchar
target_currency         varchar
exchange_rate           float
date                    datetime
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
# -- logic: self-join to get the columns side by side for diff operations, need to join on two keys to have 1:1 match
-- logic: we will also need to find exchange to USD ONLY

-- ensure that we are minus from the latest date
SELECT t1.source_currency, t2.exchange_rate - t1.exchange_rate AS difference
FROM sf_exchange_rate t1
JOIN sf_exchange_rate t2
    ON t1.source_currency = t2.source_currency
    AND t2.target_currency = t2.target_currency
-- set the date for differencing
WHERE t1.date = '2020-01-01'
      AND t2.date = '2020-07-01'
      AND t1.target_currency = 'USD'
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```p