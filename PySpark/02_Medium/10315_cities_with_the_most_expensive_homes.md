# StrataScratch Question ID: 10315 - Cities With The Most Expensive Homes

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10315` |
| **Title** | **Cities With The Most Expensive Homes** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10315) |

---

## 1. Problem Description

Write a query that identifies cities with higher than average home prices when compared to the national average. Output the city names.

---

## 2. Input Tables & Schema

```text
<zillow_transactions>
id                  int
state               varchar
city                varchar
street_address      varchar
mkt_price           int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `w