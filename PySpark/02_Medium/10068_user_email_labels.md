# StrataScratch Question ID: 10068 - User Email Labels

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10068` |
| **Title** | **User Email Labels** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10068) |

---

## 1. Problem Description

Find the number of emails received by each user under each built-in email label. The email labels are: 'Promotion', 'Social', and 'Shopping'. Output the user along with the number of promotion, social, and shopping mails count,.

---

## 2. Input Tables & Schema

```text
(google_gmail_emails)
id                      int
from_user               varchar
to_user                 varchar
day                     int
(google_gmail_labels)
email_id                int
label                   varchar
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
# -- we need count for each user, 'promotion', 'social' and 'shopping' tags
-- users are the user that RECEVIED

SELECT to_user,
       SUM(CASE WHEN label = 'Promotion' THEN 1
           ELSE 0
           END) AS promo_cnt,
       SUM(CASE WHEN label = 'Social' THEN 1
           ELSE 0
           END) AS soc_cnt,
       SUM(CASE WHEN label = 'Shopping' THEN 1
           ELSE 0
           END) AS shop_cnt
FROM google_gmail_emails e
JOIN google_gmail_labels l
    ON e.id = l.email_id
GROUP BY 1
ORDER BY 1
# ''').show()

```

---

## 5. Alternative Approach: PySpa