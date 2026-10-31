# StrataScratch Question ID: 2018 - Inactive Free Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2018` |
| **Title** | **Inactive Free Users** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2018) |

---

## 1. Problem Description

Return a list of users with status free who didn’t make any calls in Apr 2020.

Table:
<rc_calls>
user_id         int
date            datetime
call_id         int

<rc_users>
user_id         int
status          varchar
company_id      int

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2018.
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
-- filter status = 'free'
-- filter list of users in who made call in Apr 2020
-- find all users and return users who have not made a call in 2020


SELECT user_id
FROM rc_users
WHERE status = 'free'
    -- free user should not have made a call in apr 2020
    AND user_id NOT IN (
        -- users who made call in apr 2020
        SELECT DISTINCT user_id
        FROM rc_calls
        WHERE DATE_PART('year', date) = '2020'
            AND DATE_PART('month', date) = '04'
    )
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql imp