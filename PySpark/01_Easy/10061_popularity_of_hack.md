# StrataScratch Question ID: 10061 - Popularity Of Hack

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10061` |
| **Title** | **Popularity Of Hack** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10061) |

---

## 1. Problem Description

Facebook has developed a new programing language called Hack.To measure the popularity of Hack they ran a survey with their employees. The survey included data on previous programing familiarity as well as the number of years of experience, age, gender and most importantly satisfaction with Hack. Due to an error location data was not collected, but your supervisor demands a report showing average popularity of Hack by office location. Luckily the user IDs of employees completing the surveys were stored.
Based on the above, find the average popularity of the Hack per office location.
Output the location along with the average popularity.

---

## 2. Input Tables & Schema

```text
<facebook_employees>
id                  int
location            varchar
age                 int
gender              varchar
is_senior           bool

facebook_hack_survey
employee_id         int
age                 int
gender              varchar
popularity          int
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
from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Execute solution using Spark SQL or DataFrame API:
# spark.sql('''
# -- objective:
-- average popularity per office

-- logic:
-- join employee and survey by id = employee_id
-- avg(popularity) by location

SELECT location,
       AVG(popularity)
FROM facebook_employees e
JOIN facebook_hack_survey h
    ON e.id = h.employee_id
GROUP BY 1
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10061").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- objective:
-- average popularity per office

-- logic:
-- join employee and survey by id = employee_id
-- avg(popularity) by location

SELECT location,
       AVG(popularity)
FROM facebook_employees e
JOIN facebook_hack_survey h
    ON e.id = h.employee_id
GROUP BY 1
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
