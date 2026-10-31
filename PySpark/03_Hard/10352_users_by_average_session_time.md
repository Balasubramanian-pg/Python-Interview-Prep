# StrataScratch Question ID: 10352 - Users By Average Session Time

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10352` |
| **Title** | **Users By Average Session Time** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10352) |

---

## 1. Problem Description

Calculate each user's average session time. A session is defined as the time difference between a page_load and page_exit. For simplicity, assume an user has only 1 session per day and if there are multiple of the same events in that day, consider only the latest page_load and earliest page_exit. Output the user_id and their average session time.

---

## 2. Input Tables & Schema

```text
<facebook_web_log>
user_id                 int
timestamp               datetime
action                  varchar
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
# Not able to solve getting wrong answer
# Import your libraries
import pyspark
from pyspark.sql.window import Window
from pyspar