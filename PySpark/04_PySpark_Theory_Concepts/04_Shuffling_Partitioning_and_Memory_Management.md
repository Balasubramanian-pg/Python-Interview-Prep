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
# BAD: triggers an expensive full shuffle just to reduce f