# StrataScratch Question ID: 10351 - Activity Rank

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10351` |
| **Title** | **Activity Rank** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Google** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10351) |

---

## 1. Problem Description

Find the email activity rank for each user. Email activity rank is defined by the total number of emails sent. The user with the highest number of emails sent will have a rank of 1, and so on. Output the user, total emails, and their activity rank. Order records by the total emails in descending order. Sort users with the same number of emails in alphabetical order.
In your rankings, return a unique value (i.e., a unique rank) even if multiple users have the same number of emails.

---

## 2. Input Tables & Schema

```text
<google_gmail_emails>
id                      int
from_user               varchar
to_user                 varchar
day                     int
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
from pyspark.sql import Window
# Start writing code
google_gmail_emails1 = google_gmail_emails

google_gmail_emails1 = google_gmail_emails1.groupBy(["from_user"]).count()
google_gmail_emails1 = google_gmail_emails1.withColumnRenamed("count","total_emails").orderBy(desc("total_emails"))
# google_gmail_emails1.show(200,truncate=False)
w = Window.orderBy(google_gmail_emails1.total_emails.desc())
google_gmail_emails1 = google_gmail_emails1.sort(asc("from_user"),desc("count")).withColumn("rank",row_number().over(w))
# google_gmail_emails1.show(truncate=False)

# To validate your solution, convert your final pySpark df to a pandas df
google_gmail_emails1.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10351").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- assumption:
-- clean data
-- all ranks must be unique

-- logic:
-- count total emails sent by each user
-- rank users by the total emails sent
-- break rank by ordering total emails desc, then user_id asc

SELECT from_user,
       COUNT(*) total_emails,
       -- rank by total emails desc, user_id asc
       RANK() OVER(ORDER BY COUNT(*) DESC, from_user ASC) AS activity_rank
FROM google_gmail_emails
GROUP BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
