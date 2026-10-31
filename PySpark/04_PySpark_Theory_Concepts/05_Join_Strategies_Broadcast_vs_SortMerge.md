# Join Strategies in PySpark: Broadcast Hash Join vs. Sort-Merge Join

## 1. Overview of Join Implementations in Spark

Selecting the appropriate join strategy is a critical performance differentiator in data engineering interviews.

```
                          [ Join Evaluation ]
                                   |
                   Is one table smaller than threshold?
                                (<= 10 MB)
                               /          \
                             YES           NO
                             /              \
             [ Broadcast Hash Join ]    Are join keys sortable?
                                        /                   \
                                      YES                    NO
                                      /                       \
                            [ Sort-Merge Join ]       [ Shuffle Hash Join ]
```

---

## 2. Broadcast Hash Join (BHJ) / Map-Side Join

### Mechanism:
1. The Driver collects the smaller DataFrame into memory.
2. The Driver broadcasts the entire small DataFrame to all executor nodes via efficient BitTorrent-like peer-to-peer protocols.
3. Each executor builds a hash table in memory.
4. The large DataFrame is streamed partition-by-partition and probed against the local in-memory hash table.
5. **ZERO Shuffle occurs for the large table!**

```python
from pyspark.sql import functions as F

# Explicit Broadcast Join Hint
large_df.join(F.broadcast(small_df), on="customer_id", how="inner")
```

- **Default Threshold**: Controlled by `spark.sql.autoBroadcastJoinThreshold` (default: 10 MB, can be increased to 100 MB+ depending on Driver RAM).
- **Interview Caution**: Never broadcast a table that does not fit comfortably in Driver RAM and Executor RAM, as it will trigger an immediate `Driver OutOfMemoryError`.

---

## 3. Sort-Merge Join (SMJ)

### Mechanism:
The default join strategy in Spark 3.x for two large DataFrames:
1. **Shuffle Phase**: Both DataFrames are shuffled across the cluster using hash partitioning on the join key, ensuring rows with identical keys end up on the exact same executor.
2. **Sort Phase**: Each executor sorts its local partition by join key.
3. **Merge Phase**: The executor iterates sequentially through both sorted streams, outputting matched records with minimal memory overhead.

- **Pros**: Highly scalable, immune to OOM errors because sorted streams are merged sequentially.
- **Cons**: High network shuffle and disk sort I/O overhead.

---

## 4. Shuffle Hash Join (SHJ)

- Shuffles both datasets on join keys, then builds an in-memory hash table for each partition of the smaller dataset.
- Useful when one table is moderately sized (too large to broadcast, but its individual partitions fit easily into executor RAM) and join keys are not easily sortable.

---

## 5. Join Comparison Matrix

| Join Type | Shuffle? | Memory Footprint | Best Used When... |
| :--- | :--- | :--- | :--- |
| **Broadcast Hash Join (BHJ)** | **None** | High on Driver; Moderate on Worker | One dataset < 100 MB. |
| **Sort-Merge Join (SMJ)** | **Yes** | Very Low (Streamed from disk) | Both datasets are large. |
| **Shuffle Hash Join (SHJ)** | **Yes** | Moderate (Hash table per partition)| One dataset partitions fit in RAM. |
| **Broadcast Nested Loop (BNLJ)**| **None** | High | Non-equi joins (`df1.id > df2.id`) on small tables. |
| **Cartesian Join** | **Yes** | Massive | Cross joins without join keys (`O(N * M)`). |
