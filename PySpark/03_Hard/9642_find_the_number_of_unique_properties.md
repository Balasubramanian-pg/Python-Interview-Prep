# StrataScratch Question ID: 9642 - Find The Number Of Unique Properties

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9642` |
| **Title** | **Find The Number Of Unique Properties** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9642) |

---

## 1. Problem Description

Solve the 'Find The Number Of Unique Properties' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
<airbnb_searches>
ds                      datetime
id_user                 varchar
ds_checkin              datetime
ds_checkout             datetime
n_searches              int
n_nights                float
n_guests_min            int
n_guests_max            int
origin_country          varchar
filter_price_min        float
filter_price_max        float
filter_room_types       varchar
filter_neighborhoods    datetime
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
-- find number of different property types

SELECT DISTINCT room_types
FROM (
    SELECT UNNEST(STRING_TO_ARRAY(filter_room_types, ',')) room_types
    FROM airbnb_searches
) unique_room_types
WHERE room_types != ''
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9642").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find number of different property types

SELECT DISTINCT room_types
FROM (
    SELECT UNNEST(STRING_TO_ARRAY(filter_room_types, ',')) room_types
    FROM airbnb_searches
) unique_room_types
WHERE room_types != ''
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
