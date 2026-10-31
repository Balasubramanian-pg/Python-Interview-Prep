# StrataScratch Question ID: 2055 - Average Customers Per City

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2055` |
| **Title** | **Average Customers Per City** |
| **Difficulty** | `Hard` |
| **Company Tag** | **LinkedIn** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2055) |

---

## 1. Problem Description

Write a query that will return all cities with more customers than the average number of  customers of all cities. For each such city, return the country name,  the city name, and the number of customers

---

## 2. Input Tables & Schema

```text
<linkedin_customers>
id                  int
business_name       varchar
city_id             int

<linkedin_city>
id                  int
city_name           varchar
country_id          int

<linkedin_country>
id                  int
country_name        varchar
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
# -- logic: need find avg number of customers across all cities, find cities who have more than the global average

-- count total customers per city
WITH avg_cust_cities AS (
    SELECT city_id, COUNT(*) AS total_customers
    FROM linkedin_customers
    GROUP BY 1
)

-- selecting the country and city name, alongside total customers
SELECT lco.country_name, lci.city_name, total_customers
FROM avg_cust_cities acc
-- joins to retrieve the detail name
JOIN linkedin_city lci
    ON acc.city_id = lci.id
JOIN linkedin_country lco
    ON lci.country_id = lco.id
-- filter for city's total customers > avg across all cities
WHERE total_customers > (
    SELECT AVG(total_customers)
    FROM avg_cust_cities
);
# ''').show()

```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSessio