# Shuffling, Partitioning, and Memory Management

## 1. The Anatomy of a Spark Shuffle

A **Shuffle** is the process of redistributing data across physical partitions and worker nodes so that rows with identical keys reside in the same physical partition.

### Why Shuffling is Expensive:
1. **Disk I/O**: Executors write shuffle map outputs to local disk files.
2. **Network I/O**: Reduce tasks fetch shuffle blocks across cluster network links.
3. **Serialization/Deserialization**: Objects must be serialized to bytes and deserialized on the receiver.
4. **Garbage Collection**: Massive churn in buffer allocation triggers JVM GC overhead.

---

## 2. Partitioning Strategies: `repartition()` vs. `coalesce()`

One of the most essential interview questions:

| Feature | `repartition(n)` | `coalesce(n)` |
| :--- | :--- | :--- |
| **Shuffle Occurs?** | **Yes** (Full network shuffle). | **No** (Combines local partitions). |
| **Increase Partitions?** | **Yes** (Can increase from 10 to 100). | **No** (Only decreases partition count). |
| **Data Distribution** | Uniformly distributed across new partitions. | May result in uneven / skewed partitions. |
| **Primary Use Case** | Balance skewed data, increase parallelism. | Efficiently reduce file count before writing to disk. |

```python
# BAD: triggers an expensive full shuffle just to reduce files
df.filter(F.col("status") == "active").repartition(1).write.parquet("output/")

# GOOD: merges existing local partitions with ZERO shuffle
df.filter(F.col("status") == "active").coalesce(1).write.parquet("output/")
```

---

## 3. Data Skew & Mitigation Techniques

**Data Skew** occurs when a disproportionate amount of data is associated with a single key (e.g., 90% of web traffic comes from `user_id = NULL` or `country = 'US'`).
- **Symptom**: One task runs for hours at 99% progress while all other tasks finished in seconds.

### Solutions:
1. **Salting the Key**:
   Append a random integer (e.g., 0 to 9) to the skewed key before grouping/joining, perform the aggregation, and then aggregate a second time on the original key:
   ```python
   # Add salt
   df_salted = df.withColumn("salted_key", F.concat(F.col("skewed_key"), F.lit("_"), (F.rand() * 10).cast("int")))
   ```
2. **Adaptive Query Execution (AQE)** in Spark 3.x:
   Enable automatic skew handling:
   ```python
   spark.conf.set("spark.sql.adaptive.enabled", "true")
   spark.conf.set("spark.sql.adaptive.skewJoin.enabled", "true")
   ```
3. **Filter Nulls Before Joining**:
   If null keys are not needed in the result, filter them out prior to joins.

---

## 4. Spark Unified Memory Architecture

Spark allocates executor JVM heap into two primary regions:

```
+---------------------------------------------------------------+
|                    Executor JVM Total Memory                  |
|  +---------------------------------------------------------+  |
|  | Reserved Memory (300 MB, Spark internal system overhead)|  |
|  +---------------------------------------------------------+  |
|  | User Memory (40%: custom data structures, UDF objects)  |  |
|  +---------------------------------------------------------+  |
|  | Spark Memory Pool (60%):                                |  |
|  |   +-----------------------+-----------------------+     |  |
|  |   |    Storage Memory     |   Execution Memory    |     |  |
|  |   | (Cached data, .cache)| (Shuffle, Join, Sort) |     |  |
|  |   +-----------------------+-----------------------+     |  |
|  |   <------- Dynamic Borrowing Boundary ----------->      |  |
|  +---------------------------------------------------------+  |
+---------------------------------------------------------------+
```

- **Execution Memory**: Used for computation in shuffles, joins, sorts, and aggregations.
- **Storage Memory**: Used for caching DataFrames (`.cache()`, `.persist()`) and broadcast variables.
- **Dynamic Occupancy**: If no cached data exists, Execution memory can borrow 100% of Storage space. If Execution needs memory, it can evict Storage cached blocks to disk.
