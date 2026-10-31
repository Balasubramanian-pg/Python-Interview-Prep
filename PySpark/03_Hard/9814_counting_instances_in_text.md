# StrataScratch Question ID: 9814 - Counting Instances In Text

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9814` |
| **Title** | **Counting Instances In Text** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9814) |

---

## 1. Problem Description

Find the number of times the exact words bull and bear appear in the contents column.


Count all occurrences, even if they appear multiple times within the same row. Matches should be case-insensitive and only count exact words, that is, exclude substrings like bullish or bearing.


Output the word (bull or bear) and the corresponding number of occurrences.

---

## 2. Input Tables & Schema

```text
Table
google_file_store
More about this question
Hints
Expected Output
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
import pyspark
from pyspark.sql.functions import *
# Start writing code
x=google_file_store.select(split("contents","\\s+").alias('w_contents'))
# print(x)
y=x.selec