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
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimi