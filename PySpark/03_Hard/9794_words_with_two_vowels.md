# StrataScratch Question ID: 9794 - Words With Two Vowels

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9794` |
| **Title** | **Words With Two Vowels** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9794) |

---

## 1. Problem Description

Find all words which contain exactly two vowels in any list in the table.

Table:
<google_word_lists>
words1              varchar
words2              varchar

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9794.
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
-- find words that contains 'two vowels'

-- logic:
-- turn each row into array
-- unnest each array into individual rows (so 1 word 1 row)
-- count vowel with regex_replace()


SELECT word
FROM (
    -- unnest each array into individual word
    SELECT DISTINCT UNNEST(STRING_TO_ARRAY(word, ',')) AS word
    FROM (
        -- combining two columns into rows
        SELECT words1 AS word
        FROM google_word_lists
        UNION
        SELECT words2 AS word
        FROM google_word_lists
    ) union_words
) unnest_word_arrays
-- filter words with >= 3 vowels
WHERE NOT word ~ '([aeiou].*){3}'
    -- and only keep words with 2 vowels
    AND word ~ '([aeiou].*){2}'
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScrat