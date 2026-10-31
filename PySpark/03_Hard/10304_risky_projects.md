# StrataScratch Question ID: 10304 - Risky Projects

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10304` |
| **Title** | **Risky Projects** |
| **Difficulty** | `Hard` |
| **Company Tag** | **LinkedIn** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10304) |

---

## 1. Problem Description

Solve the 'Risky Projects' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
<linkedin_projects>
id              int
title           varchar
budget          int
start_date      datetime
end_date        datetime

<linkedin_emp_projects>
emp_id          int
project_id      int

<linkedin_employees>
id              int
first_name      varchar
last_name       varchar
salary          int
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
from pyspark.sql import function