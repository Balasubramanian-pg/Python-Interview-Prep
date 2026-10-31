# StrataScratch Question ID: 2004 - Number Of Comments Per User In Past 30 Days

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2004` |
| **Title** | **Number Of Comments Per User In Past 30 Days** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2004) |

---

## 1. Problem Description

Return the total number of comments received for each user in the last 30 days. Assume today is 2020-02-10.

---

## 2. Input Tables & Schema

```text
<fb_comments_count>
user_id             int
created_at          datetime
number_of_comments  int
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
-- count number of comments per user in the last 30 days 2020-02-10 - 30 days

SELECT user_id,
       SUM(number_of_comments)
FROM fb_comments_count
-- date conversion
WHERE created_at BETWEEN '2020-02-10'::date - 30 * INTERVAL '1 DAY' AND '2020-02-10'::date
GROUP BY 1
# ''').show()

```

---

## 5. Alternative Ap