# StrataScratch Question ID: 2001 - Share Of Loan Balance

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2001` |
| **Title** | **Share Of Loan Balance** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2001) |

---

## 1. Problem Description

Write a query that returns the rate_type, loan_id and balance of each loan type, and a column that shows what percentage of the submission’s total balance each loan constitutes.

---

## 2. Input Tables & Schema

```text
<submissions>
id                      int
balance                 float
interest_rate           float
rate_type               varchar
loan_id                 int
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
from pyspark.sql import functions as F
from pyspark.sql.window  import Window 

# We partition by rate_type to get totals per group (Fixed vs Variable)
window_spec = Window.partitionBy('rate_type')

# Calculate the Percentage
# Formula: (Individual Balance / Total Group Balance) * 100
df_with_share = (
    submissions
    .withColumn('total_balance_per_rate_type',F.sum('balance').over(window_spec))
    .withColumn('balance_shares', F.col('balance')/F.col('total_balance_per_rate_type') * 100 )
    )
    
#final output DF
final_df = df_with_share.select("rate_type","loan_id","balance","balance_shares").orderBy("rate_type","loan_id")


# To validate your solution, convert your final pySpark df to a pandas df
final_df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2001").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find the % of each loan on the basis of the overall rate_type's balance

-- assumption:
-- "balance of each loan type" = "balance of each loan(rate_type)"

-- logic:
-- sum(balance) for each rate_type AS total_balance
-- join total_balance on each loan's balance ON rate_type

-- output:
-- rate_type, loan_id, balance, % of the total balance for the specific rate_type
SELECT s.rate_type,
       s.loan_id,
       s.balance,
       -- computing % of balance / total_balance
       (s.balance / rate_balances.total_balance)::float AS pct_total_balance
FROM submissions s
JOIN (
    -- summing balance for each rate_type
    SELECT rate_type,
           SUM(balance) AS total_balance
    FROM submissions
    GROUP BY 1
) rate_balances
    ON s.rate_type = rate_balances.rate_type
ORDER BY 1,3
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
