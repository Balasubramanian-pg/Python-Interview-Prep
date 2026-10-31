# Window Functions and Complex Aggregations in PySpark

## 1. What are Window Functions?

Window functions compute values over a defined group of rows (called a **Frame**) related to the current row, **without collapsing rows** like standard `groupBy()` aggregations do.

In PySpark, all window operations require:
1. `from pyspark.sql.window import Window`
2. `from pyspark.sql import functions as F`

```python
from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Basic Specification
windowSpec = Window.partitionBy("department").orderBy(F.col("salary").desc())
```

---

## 2. Ranking Functions Comparison

A high-frequency interview question: Explain the exact behavioral differences between `row_number()`, `rank()`, and `dense_rank()`:

| Value | `row_number()` | `rank()` | `dense_rank()` |
| :---: | :---: | :---: | :---: |
| 1000 | 1 | 1 | 1 |
| 900  | 2 | 2 | 2 |
| 900  | 3 | 2 | 2 |
| 850  | 4 | 4 (skips 3) | 3 (no skip) |
| 800  | 5 | 5 | 4 |

```python
windowSpec = Window.partitionBy("dept_id").orderBy(F.col("salary").desc())

df = df.withColumn("row_num", F.row_number().over(windowSpec)) \
       .withColumn("rank", F.rank().over(windowSpec)) \
       .withColumn("dense_rank", F.dense_rank().over(windowSpec))
```

---

## 3. Lead & Lag Analytic Functions

Used to access prior or subsequent records without performing self-joins (e.g., month-over-month growth, consecutive active days):

```python
windowSpec = Window.partitionBy("user_id").orderBy("event_date")

df = df.withColumn("prev_date", F.lag("event_date", 1).over(windowSpec)) \
       .withColumn("next_date", F.lead("event_date", 1).over(windowSpec)) \
       .withColumn("days_since_last", F.datediff(F.col("event_date"), F.col("prev_date")))
```

---

## 4. Window Framing: `rowsBetween()` vs. `rangeBetween()`

Defines which subset of rows within the partition are included in the calculation:

```python
# Cumulative Running Total (From start of partition up to current row)
cum_window = Window.partitionBy("account_id").orderBy("tx_date") \
                   .rowsBetween(Window.unboundedPrec