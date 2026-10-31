# StrataScratch Question ID: 10310 - Class Performance

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10310` |
| **Title** | **Class Performance** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10310) |

---

## 1. Problem Description

You are given a table containing assignment scores of students in a class. Write a query that identifies the largest difference in total score  of all assignments.
Output just the difference in total score (sum of all 3 assignments) between a student with the highest score and a student with the lowest score.

---

## 2. Input Tables & Schema

```text
(box_scores)
id          int
student     varchar
assignment1 int
assignment2 int
assignment3 int
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
# WITH total_scores AS (
    SELECT student, SUM(score) AS total_score
    FROM (
        SELECT student, assignment1 AS score
        FROM box_scores
        UNION
        SELECT student, assignment2 AS score
        FROM box_scores
        UNION
        SELECT student, assignment3 AS score
        FROM box_scores
    ) AS total_scores
    GROUP BY 1
)

SELECT MAX(total_score) - MIN(total_score) AS difference_in_score
FROM total_scores
# ''').show()

```

---

## 5. Alternative Approa