# StrataScratch Question ID: 2058 - Total Shipment Weight

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2058` |
| **Title** | **Total Shipment Weight** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2058) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Total Shipment Weight.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 2058.
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

#using window functions we separate by shipment_id
shimpent_window =  Window.partitionBy('shipment_id')


# Start writing code
amazon_shipment = amazon_shipment.withColumn('total weight', F.sum('weight').over(shimpent_window))

# To validate your solution, convert your final pyS