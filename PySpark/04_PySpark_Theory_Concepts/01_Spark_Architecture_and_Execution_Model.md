# Apache Spark & PySpark Architecture and Execution Model

## 1. High-Level Architecture Overview

Apache Spark operates as a distributed computing system following a **master-worker architecture**. In PySpark, Python code interfaces with Spark's underlying JVM (Java Virtual Machine) core via the **Py4J** bridge.

```
+-------------------------------------------------------------+
|                        Driver Program                       |
|  +---------------------+        +-------------------------+ |
|  | PySpark Application | <----> | SparkSession / Context  | |
|  +---------------------+ (Py4J) +-------------------------+ |
|                                              |              |
+----------------------------------------------|--------------+
                                               |
                                     +-------------------+
                                     |  Cluster Manager  |
                                     | (K8s/YARN/St.aln) |
                                     +-------------------+
                                       /               \
                                      /                 \
          +--------------------------+                   +--------------------------+
          |      Worker Node 1       |                   |      Worker Node 2       |
          |  +--------------------+  |                   |  +--------------------+  |
          |  |  Executor Process  |  |                   |  |  Executor Process  |  |
          |  |  [Task] [Task]     |  |                   |  |  [Task] [Task]     |  |
          |  |  BlockManager (RAM)|  |                   |  |  BlockManager (RAM)|  |
          |  +--------------------+  |                   |  +--------------------+  |
          +--------------------------+                   +--------------------------+