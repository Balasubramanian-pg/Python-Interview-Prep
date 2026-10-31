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
# # print(lst_contents)
for i in lst_contents:
    if i not in dict1:
        dict1[i] = 1
    else:
        dict1[i]+=1
# print(dict1)
# lst_key = list(dict1.keys())
# lst_val = list(dict1.values())
# data = list(zip(lst_key,lst_val))
# print(data)
# google_file_store = spark.createDataFrame(data, ["word","occurrences"])
# google_file_store.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
# google_file_store.toPandas()
dict2={'word':[],'occurrences':[]}
for i,j in dict1.items():
    dict2['word'].append(i)
    dict2['occurrences'].append(j)
# print(dict2)

df=pd.DataFrame(dict2)
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_9817").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 9817\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
