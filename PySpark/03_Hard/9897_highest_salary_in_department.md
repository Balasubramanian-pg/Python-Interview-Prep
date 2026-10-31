# StrataScratch Question ID: 9897 - Highest Salary In Department

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9897` |
| **Title** | **Highest Salary In Department** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9897) |

---

## 1. Problem Description

Find the employee with the highest salary per department.
Output the department name, employee's first name along with the corresponding salary.

---

## 2. Input Tables & Schema

```text
[employee]
id                      int
first_name              varchar
last_name               varchar
age                     int
sex                     varchar
employee_title          varchar
department              varchar
salary                  int
target                  int
bonus                   int
email                   varchar
city                    varchar
address                 varchar
manager_id              int
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
from pyspark.sql import *
from pyspark.sql.functions import *

# Start writing code
df=employee
df1=df.groupBy(col("department")).agg(max(col("salary")).alias("salary"))
df1=df1.withColumnRenamed("department","dpt").withColumnRenamed("salary","sal")
# df1.show(truncate=False)
df=df1.join(df,df1.sal==df.salary,"left")
# df.show(truncate=False)
df=df.drop("department","salary")
df=df.withColumnRenamed("dpt","department").withColumnRenamed("sal","salary")
df=df.select("department","first_name","salary")
# df.show(truncate=False)
# To validate your solutio