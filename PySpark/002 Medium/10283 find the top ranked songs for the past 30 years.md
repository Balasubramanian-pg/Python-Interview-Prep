# StrataScratch Question ID: 10283 - Find The Top-ranked Songs For The Past 30 Years.

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10283` |
| **Title** | **Find The Top-ranked Songs For The Past 30 Years.** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10283) |

---

## 1. Problem Description

Find all the songs that were top-ranked (at first position) at least once in the past 30 years

---

## 2. Input Tables & Schema

```text
<billboard_top_100_year_end>
year                                int
year_rank                           int
group_name                          varchar
artist                              varchar
song_name                           varchar
id                                  int
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
-- find song that at least ranked first one time in any year
-- within the last 30 years

-- assumption:
-- the song has to be rank 1 at least once
-- song can be rank 1 for many times
-- we use song_name as the primary key

-- logic:
-- filter songs in the last 30 years
-- count the number of rank 1 in the same period
-- return all details about the song

-- select song name
SELECT DISTINCT song_name
FROM billboard_top_100_year_end
-- within the last 30 years from today's year
WHERE DATE_PART('year', CURRENT_DATE) - year <= 30
    AND year_rank = 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10283").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find song that at least ranked first one time in any year
-- within the last 30 years

-- assumption:
-- the song has to be rank 1 at least once
-- song can be rank 1 for many times
-- we use song_name as the primary key

-- logic:
-- filter songs in the last 30 years
-- count the number of rank 1 in the same period
-- return all details about the song

-- select song name
SELECT DISTINCT song_name
FROM billboard_top_100_year_end
-- within the last 30 years from today's year
WHERE DATE_PART('year', CURRENT_DATE) - year <= 30
    AND year_rank = 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
