# StrataScratch Question ID: 10284 - Popularity Percentage

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10284` |
| **Title** | **Popularity Percentage** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10284) |

---

## 1. Problem Description

Find the popularity percentage for each user on Meta/Facebook. The dataset contains two columns, user1 and user2, which represent pairs of friends. Each row indicates a mutual friendship between user1 and user2, meaning both users are friends with each other. A user's popularity percentage is calculated as the total number of friends they have (counting connections from both user1 and user2 columns) divided by the total number of unique users on the platform. Multiply this value by 100 to express it as a percentage.


Output each user along with their calculated popularity percentage. The results should be ordered by user ID in ascending order.

---

## 2. Input Tables & Schema

```text
Table
facebook_friends
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

user1	popularity
1	55.56
2	33.33
3	33.33
4	11.11
5	11.11
facebook_friends
Preview
user1	user2
2	1
1	3
4	1
1	5
1	6
2	6
7	2
8	3
3	9
user1:
bigint
user2:
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
from pyspark.sql.functions import *
# Start writing code

facebook_friends1 = facebook_friends.select("user1").union(facebook_friends.select("user2"))
cnt=facebook_friends1.distinct().count()
# print(cnt)
facebook_friends1=facebook_friends1.distinct().orderBy("user1")
# facebook_friends1.show(truncate=False)
facebook_friends=facebook_friends.unionAll(facebook_friends.select("