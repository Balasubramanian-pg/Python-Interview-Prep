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
- Can be executed entirely in parallel on each worker node in me