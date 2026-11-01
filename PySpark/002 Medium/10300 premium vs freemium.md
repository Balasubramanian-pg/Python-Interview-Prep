# StrataScratch Question ID: 10300 - Premium Vs Freemium

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10300` |
| **Title** | **Premium Vs Freemium** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Microsoft** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10300) |

---

## 1. Problem Description

Find the total number of downloads for paying and non-paying users by date. Include only records where non-paying customers have more downloads than paying customers. The output should be sorted by earliest date first and contain 3 columns date, non-paying downloads, paying downloads.

---

## 2. Input Tables & Schema

```text
<ms_user_dimension>
user_id             int
acc_id              int

ms_acc_dimension
acc_id              int
paying_customer     varchar

ms_download_facts
2021-10-13          datetime
user_id             int
downloads           int
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
# Start writing code

ms_user_dimension = ms_user_dimension.join(ms_acc_dimension,ms_user_dimension.acc_id == ms_acc_dimension.acc_id, "inner")
ms_user_dimension = ms_user_dimension.join(ms_download_facts, ms_user_dimension.user_id == ms_download_facts.user_id, "inner")
# ms_user_dimension.show(truncate=False)
df_no =  ms_user_dimension.filter(ms_user_dimension.paying_customer == "no")
df_no = df_no.groupBy("date").sum("downloads")
df_no = df_no.withColumnRenamed("sum(downloads)","no")
df_yes = ms_user_dimension.filter(ms_user_dimension.paying_customer == "yes")
df_yes = df_yes.groupBy("date").sum("downloads")
df_yes = df_yes.withColumnRenamed("sum(downloads)","yes")
df_yes_no = df_yes.join(df_no, df_yes.date == df_no.date, "inner").drop(df_no.date)
df = df_yes_no.filter(df_yes_no.no > df_yes_no.yes).sort(col("date"))
df = df.select(["date","no","yes"])
# To validate your solution, convert your final pySpark df to a pandas df
df.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10300").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- find downloads by paying and non-paying users
-- on a date basis
-- records should be non-paying downloads > paying downloads

-- assumption:
-- downloads varies on dates can possibly be 0 on certain dates

-- logic:
-- find downloads per user
-- filter paying and non-paying customers
-- self join on date
-- filter non-paying download > paying downlaods
-- order by earliest date

WITH downloads_by_date AS (
    SELECT d.date,
           paying_customer,
           SUM(d.downloads) AS downloads
    FROM ms_user_dimension ud
    JOIN ms_acc_dimension ad
        ON ud.acc_id = ad.acc_id
    JOIN ms_download_facts d
        ON ud.user_id = d.user_id
    GROUP BY 1,2
)

SELECT p.date,
       np.downloads AS non_paying_downloads,
       p.downloads AS paying_downloads
FROM downloads_by_date p
JOIN (
    SELECT date,
           downloads
    FROM downloads_by_date
    WHERE paying_customer = 'no'
) np
    ON p.date = np.date
WHERE p.paying_customer = 'yes'
    AND np.downloads > p.downloads
ORDER BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
