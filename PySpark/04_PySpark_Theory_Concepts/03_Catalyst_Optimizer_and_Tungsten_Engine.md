# The Catalyst Optimizer & Project Tungsten in Spark 3.x

## 1. What is the Catalyst Optimizer?

The **Catalyst Optimizer** is the query optimization engine behind PySpark DataFrames, Datasets, and Spark SQL. It translates declarative Python DataFrame operations into highly optimized JVM bytecode.

```
+--------------------+
|  SQL / DataFrame   |
+--------------------+
          |
          v
   [ 1. ANALYSIS ]  --> Resolves column names & data types against Catalog
          |
          v
[ 2. LOGICAL OPTIMIZATION ] --> Rule-based optimizations (Predicate Pushdown, Projection Pruning)
          |
          v
[ 3. PHYSICAL PLANNING ]   --> Generates physical plans (e.g., BroadcastHashJoin vs SortMergeJoin)
          |
          v
[ 4. CODE GENERATION ]     --> Compiles plan into optimized Java bytecode (Whole-Stage CodeGen)
```

---

## 2. The Four Optimization Phases

### Phase 1: Analysis
- Validates relations, table names, and column identifiers against the metastore **Catalog**.
- Converts an **Unresolved Logical Plan** into a **Resolved L