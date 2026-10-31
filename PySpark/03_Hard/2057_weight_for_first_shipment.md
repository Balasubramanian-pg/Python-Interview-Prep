# StrataScratch Question ID: 2057 - Weight For First Shipment

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2057` |
| **Title** | **Weight For First Shipment** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Amazon** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2057) |

---

## 1. Problem Description

Write a query to find the weight for each shipment's earliest shipment date. Output the shipment id along with the weight.

---

## 2. Input Tables & Schema

```text
<amazon_shipment>
shipment_id             int
sub_id                  int
weight                  int
shipment_date           datetime
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
-- find weight for each shipment's earliest shipment date

-- assumption:
-- there may be more than 1 sub_id per shipment_id for earliest date

-- logic:
-- min(shipment_date) for shipment_id
-- where shipment = min(shipment_date)

SELECT s.shipment_id,
       SUM(s.weight)
FROM amazon_shipment s
JOIN (
    SELECT shipment_id,
           MIN(shipment_date) AS earliest_date
    FROM amazon_shipment
    GROUP BY 1
) earliest_shipment
    ON s.shipment_id = earliest_shipment.shipment_id
    AND s.shipment_date = earliest_shipment.earliest_date
GROUP BY 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_2057").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find weight for each shipment's earliest shipment date

-- assumption:
-- there may be more than 1 sub_id per shipment_id for earliest date

-- logic:
-- min(shipment_date) for shipment_id
-- where shipment = min(shipment_date)

SELECT s.shipment_id,
       SUM(s.weight)
FROM amazon_shipment s
JOIN (
    SELECT shipment_id,
           MIN(shipment_date) AS earliest_date
    FROM amazon_shipment
    GROUP BY 1
) earliest_shipment
    ON s.shipment_id = earliest_shipment.shipment_id
    AND s.shipment_date = earliest_shipment.earliest_date
GROUP BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
