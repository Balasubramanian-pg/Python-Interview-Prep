# StrataScratch Question ID: 2003 - Recent Refinance Submissions

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2003` |
| **Title** | **Recent Refinance Submissions** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2003) |

---

## 1. Problem Description

Write a query that joins this submissions table to the loans table and returns the total loan balance on each user’s most recent ‘Refinance’ submission. Return all users and the balance for each of them.

---

## 2. Input Tables & Schema

```text
<loans>
id              int
user_id         int
created_at      datetime
status          varchar
type            varchar

<submissions>
id              int
balance         float
interest_rate   float
rate_type       varchar
loan_id         int
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
# -- objective:
-- 1. total loan balance on the most RECENT 'Refinance' submission
-- 2. Return all users and balance

-- assumption:
-- not all users have make the first payment for the 'Refinance submission'
-- status should be 'offer_accepted' -> means they start the loan already

-- logic:
-- need latest date on 'refinance' for each user
-- retrieve loan_id and user_id
-- join submission on loan_id and user_id

-- getting user_id and balance
SELECT latest_refinance.user_id,
       balance
FROM (
    -- for each loan submission, we want see the date vs the latest submission date for Refinance
    SELECT DISTINCT user_id,
           created_at,
           id,
           MAX(created_at) OVER(PARTITION BY user_id) AS latest_date
    FROM loans
    WHERE type = 'Refinance'
) latest_refinance
JOIN submissions s
    ON latest_refinance.id = s.loan_id
-- ensure that the latest refinance submission is observed
WHERE latest_refinance.created_at = latest_refinance.latest_date
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2003").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- 1. total loan balance on the most RECENT 'Refinance' submission
-- 2. Return all users and balance

-- assumption:
-- not all users have make the first payment for the 'Refinance submission'
-- status should be 'offer_accepted' -> means they start the loan already

-- logic:
-- need latest date on 'refinance' for each user
-- retrieve loan_id and user_id
-- join submission on loan_id and user_id

-- getting user_id and balance
SELECT latest_refinance.user_id,
       balance
FROM (
    -- for each loan submission, we want see the date vs the latest submission date for Refinance
    SELECT DISTINCT user_id,
           created_at,
           id,
           MAX(created_at) OVER(PARTITION BY user_id) AS latest_date
    FROM loans
    WHERE type = 'Refinance'
) latest_refinance
JOIN submissions s
    ON latest_refinance.id = s.loan_id
-- ensure that the latest refinance submission is observed
WHERE latest_refinance.created_at = latest_refinance.latest_date
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
