# StrataScratch Question ID: 2005 - Share Of Active Users

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2005` |
| **Title** | **Share Of Active Users** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2005) |

---

## 1. Problem Description

Return the share of monthly active users in the United States (US). Active users are the ones with an "open" status in the table.

---

## 2. Input Tables & Schema

```text
<fb_active_users>
user_id             int
name                varchar
status              varchar
country             varchar
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
df = fb_active_users
df.filter(df.country=='USA')
cnt= df.count()
# print(cnt)
df1=df.filter(df.status=='open')
cnt1=df1.count()
# print(cnt1)
# print(cnt1/cnt)
df=df.withColumn("active_users_share",round(lit(cnt1/cnt),1))
df=df.select("active_users_share")
# To validate your solution, convert your final pySpark df to a pandas df
# fb_active_users.toPandas()
df.toPandas().head(1)
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.