# StrataScratch Question ID: 9818 - File Contents Shuffle

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9818` |
| **Title** | **File Contents Shuffle** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9818) |

---

## 1. Problem Description

Sort the words alphabetically in 'final.txt' and make a new file named 'wacky.txt'. Output the file contents in one column and the filename 'wacky.txt' in another column.

* If coding in python, the file contents should be contained in a list.

---

## 2. Input Tables & Schema

```text
<google_file_store>
filename            varchar
contents            varchar
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
# -- logic:
-- 1. filter filename for 'final.txt'
-- 2. turn content into individual words within an array
-- 3. unnest the array
-- 4. sort rows by alphabetical order
-- 5. merge rows back into 1 file content

SELECT 'wacky.txt' AS filename, STRING_AGG(words, ' ') AS contents
FROM (
    -- turn content into individual words in array
    SELECT UNNEST(STRING_TO_ARRAY(LOWER(contents), ' ')) AS words
    FROM google_file_store
    -- filter for filename = 'final.txt'
    WHERE filename = 'final.txt'
    ORDER BY words ASC
) AS order_words
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSess