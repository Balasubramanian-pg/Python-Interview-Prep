# StrataScratch Question ID: 10308 - Salaries Differences

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10308` |
| **Title** | **Salaries Differences** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10308) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Salaries Differences.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10308.
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
import pyspark.sql.functions as f

# 1. Standard Join

joined_df = db_employee.join(db_dept, db_employee.department_id == db_dept.id)

# 2. Conditional Aggregation (Faster & cleaner than Pivot)
# We find the max salary for each dept on the same row

result_df = joined_df.agg(
    f.max(f.when(f.col("department") == 'marketing', f.col("salary"))).alias("mkt_max"),
    f.max(f.when(f.col("department") == 'engineering', f.col("salary"))).alias("eng_max")
)

# 3. Final Calculation
# Column name must be EXACTLY 'salary_difference'

final_res = result_df.select(
    f.abs(f.col("mkt_max") - f.col("eng_max")).alias("salary_difference")
)

# StrataScratch Trick: Convert to Pandas for the platform grader
return final_res.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10308").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10308\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
