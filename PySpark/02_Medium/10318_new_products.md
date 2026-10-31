# StrataScratch Question ID: 10318 - New Products

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10318` |
| **Title** | **New Products** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10318) |

---

## 1. Problem Description

Calculate the net change in the number of products launched by companies in 2020 compared to 2019. Your output should include the company names and the net difference.
(Net difference = Number of products launched in 2020 - The number launched in 2019.)

---

## 2. Input Tables & Schema

```text
[car_launches]
year                    int
company_name            varchar
product_name            varchar
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
from pyspark.sql.functions import *

# Start writing code
car_launches_2020 = car_launches.filter(car_launches.year == 2020).groupBy("company_name").agg(count("*").alias("cnt1"))
car_launches_2019 = car_launches.filter(car_launches.year == 2019).groupBy("company_name").agg(count("*").alias("cnt2"))
car_launches_df1 = car_launches_2020.join(car_launches_2019, car_launches_2020['company_name'] == car_launches_2019['company_name'],"full").drop(car_launches_2019.company_name)
car_launches_df1 = car_launches_df1.withColumn("net_products",car_launches_df1["cnt1"]-car_launches_df1["cnt2"]).drop("cnt1","cnt2").drop()
# car_launches_df1.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
car_launches_df1.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10318").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
/*

1. figure the net dfifference (no. comp in 2020 vs 2019)
2. if company does not exist in 2019, all launched in 2020 is NEW

Potential edge case:
1. exist in 2019 but not in 2020

*/

SELECT company_name,
       SUM(product_2020) - SUM(product_2019) AS net_difference
FROM (
    SELECT company_name,
           (CASE 
                WHEN year = 2019 THEN 1
                ELSE 0
            END) AS product_2019, 
            (CASE 
                WHEN year = 2020 THEN 1
                ELSE 0
            END) AS product_2020
    FROM car_launches
    ) AS product_counts
GROUP BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
