# StrataScratch Question ID: 10073 - Favorite Host Nationality

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10073` |
| **Title** | **Favorite Host Nationality** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Airbnb** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10073) |

---

## 1. Problem Description

For each guest reviewer, find the nationality of the reviewer’s favorite host based on the guest’s highest review score given to a host. Output the user ID of the guest along with their favorite host’s nationality.

---

## 2. Input Tables & Schema

```text
<airbnb_reviews>
from_user               int
to_user                 int
from_type               varchar
to_type                 varchar
review_score            int

<airbnb_hosts>
host_id                 int
nationality             varchar
gender                  varchar
age                     int
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

``