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
                   .rowsBetween(Window.unboundedPreceding, Window.currentRow)

df = df.withColumn("running_total", F.sum("amount").over(cum_window))

# 7-Day Moving Average
# rowsBetween uses PHYSICAL row offsets (-3 to +3 rows)
moving_avg_rows = Window.partitionBy("ticker").orderBy("trade_date") \
                        .rowsBetween(-3, 3)

# rangeBetween uses LOGICAL value offsets (e.g., within 7 days in seconds)
# Requires unix_timestamp for date ranges
days_window = Window.partitionBy("ticker").orderBy(F.col("date_seconds")) \
                    .rangeBetween(-7 * 86400, 0)
```

---

## 5. Performance Tips for Window Functions

1. **Always provide a `partitionBy`**: A window without `partitionBy` moves **all cluster data onto a single partition on one executor**, causing severe bottlenecking and OOM.
2. **Prune unnecessary columns**: Window operations spill to disk if records have wide schemas. Select only required columns prior to applying window definitions.
3. **Filter after ranking**: When finding top-N records per group, filter immediately after assigning `row_number()` or `dense_rank()`.
