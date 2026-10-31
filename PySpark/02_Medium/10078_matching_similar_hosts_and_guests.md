# StrataScratch Question ID: 10078 - Matching Similar Hosts And Guests

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10078` |
| **Title** | **Matching Similar Hosts And Guests** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Airbnb** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10078) |

---

## 1. Problem Description

Find matching hosts and guests pairs in a way that they are both of the same gender and nationality.
Output the host id and the guest id of matched pair.

---

## 2. Input Tables & Schema

```text
Tables
airbnb_hosts
airbnb_guests
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

host_id	guest_id
11	11
4	0
0	9
10	6
8	3
airbnb_hosts
Preview
host_id	nationality	gender	age
0	USA	M	28
1	USA	F	29
2	China	F	31
3	China	M	24
4	Mali	M	30
5	Mali	F	30
6	Luxembourg	M	25
7	Luxembourg	F	25
8	Australia	F	33
9	Australia	M	35
10	Brazil	M	39
11	Brazil	F	42
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
2	China	F	31
3	China	M	24
4	Mali	M	30
5	Mali	F	30
6	Luxembourg	M	25
7	Luxembourg	F	25
8	Australia	F	33
9	Australia	M	35
10	Brazil	M	39
11	Brazil	F	42
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
2	China	F	31
3	China	M	24
4	Mali	M	30
5	Mali	F	30
6	Luxembourg	M	25
7	Luxembourg	F	25
8	Australia	F	33
9	Australia	M	35
10	Brazil	M	39
11	Brazil	F	42
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
2	China	F	31
3	China	M	24
4	Mali	M	30
5	Mali	F	30
6	Luxembourg	M	25
7	Luxembourg	F	25
8	Australia	F	33
9	Australia	M	35
10	Brazil	M	39
11	Brazil	F	42
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
1	USA	F	29
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
0	USA	M	28
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
6	Luxembourg	M	25
7	Luxembourg	F	25
host_id:
bigint
nationality:
string
gender:
string
age:
bigint
airbnb_guests
Preview
guest_id	nationality	gender	age
0	Mali	M	21
1	China	F	23
2	Mali	F	27
3	Australia	F	24
4	Luxembourg	M	19
5	USA	F	33
6	Brazil	M	32
7	China	M	27
8	Australia	M	37
9	USA	M	29
10	Luxembourg	F	28
11	Brazil	F	24
guest_id:
bigint
nationality:
string
gender:
string
age:
bigint
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations until final aggregations.

---

## 4. PySpark DataFrame API Solution

```python
# Import your libraries
import pyspark

# Start writing code
df=airbnb_hosts
df1=airbnb_guests

df2 = df.join(df1,(df.nationality == df1.nationality) & (df.gender == df1.gender), "left")
df2 = df2.select("host_id","guest_id").distinct()
# df2.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
# airbnb_hosts.toPandas()
df2.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10078").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10078\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
