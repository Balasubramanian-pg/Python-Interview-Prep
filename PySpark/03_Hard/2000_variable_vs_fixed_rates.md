# StrataScratch Question ID: 2000 - Variable Vs Fixed Rates

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2000` |
| **Title** | **Variable Vs Fixed Rates** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2000) |

---

## 1. Problem Description

Write a query that returns binary description of rate type per loan_id. The results should have one row per loan_id and two columns: for fixed and variable type.

Table:
<submissions>
id                  int
balance             float
interest_rate       float
rate_type           varchar
loan_id             int

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2000.
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
-- true/false for variable and fixed per load_id

-- assumption:
-- binary description = 0/1

-- logic:
-- self join on loan_id to get two columns of rate_type
-- case when to insert 0/1 for both variable and fixed columns

SELECT a.loan_id,
       CASE
           WHEN a.rate_type = 'variable'
           THEN 1
           ELSE 0 END AS variable,
       CASE
           WHEN b.rate_type = 'fixed'
           THEN 1
           ELSE 0 END as fixed
FROM submissions a
JOIN submissions b
    ON a.loan_id = b.loan_id
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2000").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- true/false for variable and fixed per load_id

-- assumption:
-- binary description = 0/1

-- logic:
-- self join on loan_id to get two columns of rate_type
-- case when to insert 0/1 for both variable and fixed columns

SELECT a.loan_id,
       CASE
           WHEN a.rate_type = 'variable'
           THEN 1
           ELSE 0 END AS variable,
       CASE
           WHEN b.rate_type = 'fixed'
           THEN 1
           ELSE 0 END as fixed
FROM submissions a
JOIN submissions b
    ON a.loan_id = b.loan_id
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
