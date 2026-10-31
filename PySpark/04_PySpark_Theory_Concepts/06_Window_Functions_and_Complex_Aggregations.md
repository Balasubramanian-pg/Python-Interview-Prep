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
windowSpec = Window.partitionBy("dept_id").orderBy(F.col("