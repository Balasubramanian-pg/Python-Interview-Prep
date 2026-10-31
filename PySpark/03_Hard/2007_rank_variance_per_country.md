# StrataScratch Question ID: 2007 - Rank Variance Per Country

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2007` |
| **Title** | **Rank Variance Per Country** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2007) |

---

## 1. Problem Description

Which countries have risen in the rankings based on the number of comments between Dec 2019 vs Jan 2020? Hint: Avoid gaps between ranks when ranking countries.

---

## 2. Input Tables & Schema

```text
<fb_comments_count>
user_id                 int
created_at              datetime
number_of_comments      int

<fb_active_users>
user_id                 int
name                    varchar
status                  varchar
country                 varchar
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
from pyspark.sql impo