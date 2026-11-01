# Transformations vs. Actions & Lazy Evaluation in PySpark

## 1. The Core Paradigm: Lazy Evaluation

In Apache Spark, computation is **strictly lazy**. When you invoke operations on a DataFrame, Spark does not execute the computation immediately. Instead, it builds a metadata blueprint called a **Lineage Graph** (or DAG - Directed Acyclic Graph).

### Why Lazy Evaluation?
1. **Global Query Optimization**: Spark inspects the entire chain of transformations before executing, enabling the **Catalyst Optimizer** to reorder operations, combine filters, and eliminate unused columns.
2. **Pipelining**: Multiple narrow operations (e.g., `filter()` followed by `select()`) are fused into a single iterator loop over data rows without writing intermediate results to memory or disk.
3. **Fault Tolerance**: If an executor crashes mid-computation, Spark reconstructs only the lost partition by replaying its lineage instructions from the source.

---

## 2. Transformations: Narrow vs. Wide

Transformations produce a new DataFrame from an existing one without modifying the original (immutability).

### 2.1 Narrow Transformations (No Shuffle)
- Each input partition contributes to **at most one** output partition.
- Can be executed entirely in parallel on each worker node in memory without network communication.
- **Common Examples**:
  - `df.select("colA", "colB")`
  - `df.filter(F.col("age") > 25)`
  - `df.withColumn("new_col", F.col("x") * 2)`
  - `df.drop("temp_col")`
  - `df.union(df2)` (when schemas and partitioning align)

### 2.2 Wide Transformations (Requires Shuffle)
- Each input partition can contribute to **multiple** output partitions.
- Requires redistributing data across physical cluster nodes over the network, known as a **Shuffle**.
- Defines the boundary between **Stages** in a Spark Job.
- **Common Examples**:
  - `df.groupBy("department").agg(F.avg("salary"))`
  - `df1.join(df2, on="id", how="inner")`
  - `df.distinct()` / `df.dropDuplicates()`
  - `df.orderBy("created_at")` / `df.sort()`
  - `df.repartition(100)`

```
Narrow Transformation (Pipelineable):
Partition 1 [Row 1, Row 2] ---> Task 1 (filter + select) ---> Partition 1 [Row 2]
Partition 2 [Row 3, Row 4] ---> Task 2 (filter + select) ---> Partition 2 [Row 4]

Wide Transformation (Shuffle Barrier):
Partition 1 [Dept A, Dept B] --\  /--> Shuffle Exchange --> Node 1 [Dept A, Dept A]
Partition 2 [Dept A, Dept B] ---X---> Shuffle Exchange --> Node 2 [Dept B, Dept B]
```

---

## 3. Actions: Triggering Execution

Actions are operations that instruct Spark to compute the DAG and produce non-DataFrame results (e.g., write to storage, return data to Driver, or output to console).

| Action | Return Type | Description / Interview Caution |
| :--- | :--- | :--- |
| `df.count()` | `int` | Counts total records across distributed partitions. |
| `df.show(n)` | `None` (Stdout) | Fetches the top `n` rows and prints a formatted text table. |
| `df.first()` / `df.head(n)` | `Row` / `list[Row]` | Returns first row(s) to Driver. |
| `df.collect()` | `list[Row]` | **Caution**: Downloads entire dataset to Driver JVM. Causes OOM on large datasets! |
| `df.toPandas()` | `pandas.DataFrame` | **Caution**: Converts entire distributed DataFrame to single-node Pandas DataFrame. |
| `df.write.parquet(path)` | `None` | Writes distributed partitions directly to persistent distributed storage. |
| `df.take(n)` | `list[Row]` | Returns an array of the first `n` elements. |

---

## 4. Lineage Graph & Fault Recovery

You can inspect the lineage of any DataFrame using `.explain()` or `.rdd.toDebugString()`:

```python
df1 = spark.read.csv("sales.csv", header=True)
df2 = df1.filter(F.col("amount") > 100)
df3 = df2.groupBy("customer_id").agg(F.sum("amount").alias("total_spent"))

# Inspect Execution Plan
df3.explain(True)
```
