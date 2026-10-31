# StrataScratch Question ID: 10026 - Aroma-based Winery Search.

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10026` |
| **Title** | **Aroma-based Winery Search.** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10026) |

---

## 1. Problem Description

Find all wineries which produce wines by possessing aromas of plum, cherry, rose, or hazelnut.
Output unique winery values only.

---

## 2. Input Tables & Schema

```text
<winemag_p1>
id                  int
country             varchar
description         varchar
designation         varchar
points              int
price               float
province            varchar
region_1            varchar
region_2            varchar
variety             varchar
winery              varchar
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
from pyspark.sql import *
# Start writing code
df=winemag_p1
# print(df.count())
df=df.filter(lower("description").rlike(r'\b(plum|cherry|rose|hazelnut)\b')).dropDuplicates()
 # print(df.count())
'''
df1=df.filter(~df.description.like("cherries"))
print(df1.count())
'''
# df.show(truncate=False)
df=df.select("winery").dropDuplicates()
df.toPandas()
# To validate your solution, convert your final pySpark df to a pandas df
# winemag_p1.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10026").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
SELECT DISTINCT winery
FROM winemag_p1
WHERE description ILIKE '%plum%' OR  description ILIKE '%cherry%' OR description ILIKE '%rose%' OR  description ILIKE '%hazelnut%'
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
