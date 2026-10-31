# StrataScratch Question ID: 9817 - Count Occurrences Of Words In Drafts

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9817` |
| **Title** | **Count Occurrences Of Words In Drafts** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Google** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9817) |

---

## 1. Problem Description

Find the number of times each word appears in the contents column across all rows in the google_file_store dataset. Output two columns: word and occurrences.

---

## 2. Input Tables & Schema

```text
Table
google_file_store
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

word	occurrences
market	6
a	5
investors	4
the	4
and	4
google_file_store
Preview
filename	contents
draft1.txt	The stock exchange predicts a bull market which would make many investors happy.
draft2.txt	The stock exchange predicts a bull market which would make many investors happy, but analysts warn of possibility of too much optimism and that in fact we are awaiting a bear market.
final.txt	The stock exchange predicts a bull market which would make many investors happy, but analysts warn of possibility of too much optimism and that in fact we are awaiting a bear market. As always predicting the future market is an uncertain game and all investors should follow their instincts and best practices.
filename:
string
contents:
string
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
import pandas as pd
import pyspark
from pyspark.sql.functions import *
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("app").getOrCreate()
dict1={}
# Start writing code
# google_file_store.show(truncate=False)
google_file_store1 = google_file_store.filter(col("filename").contains("draft"))
# google_file_store1.show(truncate=False)
contents=list(google_file_store1.select("contents").toPandas()["contents"])
# # print(contents,type(contents))
lst_contents=[]
for i in contents:
    i=i.replace('.','')
    i=i.replace(',','')
#     # print(i.split())
    lst_contents.extend(i.split())
# #