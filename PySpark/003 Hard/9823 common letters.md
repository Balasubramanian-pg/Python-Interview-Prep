# StrataScratch Question ID: 9823 - Common Letters

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9823` |
| **Title** | **Common Letters** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9823) |

---

## 1. Problem Description

Find the top 3 most common letters across all the words from both the tables. Output the letter along with the number of occurrences and order records in descending order based on the number of occurrences.

---

## 2. Input Tables & Schema

```text
<google_file_store>
filename            varchar
contents            varchar

<google_word_lists>
words1              varchar
words2              varchar
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
-- for all letter that appears, we want to count their occurences
-- and find the top 3

-- asssumption:
-- only look at contents, words1, words2


-- logic:
-- string_to_array and unnest() to get words in each row individually
-- union all words1, words2, words3, DO NOT REMOVE DUPLICATES
-- regext_split_string_to_array() to extract letters
-- unnest() to get letters to each row individually
-- groupby() letters and count(*)
-- order by count(*) DESC

-- groupby each letters and count(*)
SELECT letters,
      COUNT(*)
FROM (
    -- extracting letters and unnest to individual letters
    SELECT words,
           UNNEST(REGEXP_SPLIT_TO_ARRAY(words, E'\\W*')) AS letters
    FROM (
        -- extracting words and unnest to individual rows
        SELECT UNNEST(STRING_TO_ARRAY(LOWER(contents), ' ')) AS words
        FROM google_file_store
        -- union all ensures all duplicates remains
        UNION ALL
        SELECT UNNEST(STRING_TO_ARRAY(words1, ',')) AS words
        FROM google_word_lists
        UNION ALL
        SELECT UNNEST(STRING_TO_ARRAY(words2, ',')) AS words
        FROM google_word_lists
    ) AS all_words
) all_letters
-- there is an issue with extracting totally excluding punctuations
WHERE letters <> ''
GROUP BY 1
ORDER BY 2 DESC
LIMIT 3
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9823").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- for all letter that appears, we want to count their occurences
-- and find the top 3

-- asssumption:
-- only look at contents, words1, words2


-- logic:
-- string_to_array and unnest() to get words in each row individually
-- union all words1, words2, words3, DO NOT REMOVE DUPLICATES
-- regext_split_string_to_array() to extract letters
-- unnest() to get letters to each row individually
-- groupby() letters and count(*)
-- order by count(*) DESC

-- groupby each letters and count(*)
SELECT letters,
      COUNT(*)
FROM (
    -- extracting letters and unnest to individual letters
    SELECT words,
           UNNEST(REGEXP_SPLIT_TO_ARRAY(words, E'\\W*')) AS letters
    FROM (
        -- extracting words and unnest to individual rows
        SELECT UNNEST(STRING_TO_ARRAY(LOWER(contents), ' ')) AS words
        FROM google_file_store
        -- union all ensures all duplicates remains
        UNION ALL
        SELECT UNNEST(STRING_TO_ARRAY(words1, ',')) AS words
        FROM google_word_lists
        UNION ALL
        SELECT UNNEST(STRING_TO_ARRAY(words2, ',')) AS words
        FROM google_word_lists
    ) AS all_words
) all_letters
-- there is an issue with extracting totally excluding punctuations
WHERE letters <> ''
GROUP BY 1
ORDER BY 2 DESC
LIMIT 3
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
