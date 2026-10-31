# StrataScratch Question ID: 10065 - Find Whether The Number Of Seniors Works At Meta Facebook

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10065` |
| **Title** | **Find Whether The Number Of Seniors Works At Meta Facebook** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10065) |

---

## 1. Problem Description

StrataScratch PySpark Interview Challenge: Find whether the number of seniors works at Meta Facebook.

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 10065.
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
from pyspark.sql import SparkSession
from pyspark.sql import functions as F

#Initialize the Spark Session
spark = SparkSession.builder.appName("EmployeeAnalysis").getOrCreate()
# Start writing code
counts = facebook_employees.select(F.count (F.when(F.col('is_senior') == 'TRUE',1 )).alias('senior_count'),F.count(F.when(F.col('location') == 'USA',1)).alias('USA_count')).collect()[0]

# separate that count as per category
senior_count = counts['senior_count']
usa_count = counts['USA_count']

# now comapre count 
if senior_count > usa_count:
    result = "More seniors"
else :