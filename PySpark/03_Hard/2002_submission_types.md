# StrataScratch Question ID: 2002 - Submission Types

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2002` |
| **Title** | **Submission Types** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2002) |

---

## 1. Problem Description

Write a query that returns the user ID of all users that have created at least one ‘Refinance’ submission and at least one ‘InSchool’ submission.

---

## 2. Input Tables & Schema

```text
<loans>
id                  int
user_id             int
created_at          datetime
status              varchar
type                varchar
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
-- find user ID have both `Refinance` and `InSchool` submission

-- assumption:
-- not all user may have that

-- logic:
-- filter user WHERE type = 'refinance' and 'inschool'
-- self join refinance and inschool
-- distinct user_id as user may have submit more thna once for both types of submissions.

SELECT DISTINCT loans.user_id
FROM loans
JOIN (
    SELECT user_id
    FROM loans
    WHERE type = 'Refinance'
) refinance
    ON loans.user_id = refinance.user_id
JOIN (
    SELECT user_id
    FROM loans
    WHERE type = 'InSchool'
) inschool
     ON loans.user_id = inschool.user_id
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session