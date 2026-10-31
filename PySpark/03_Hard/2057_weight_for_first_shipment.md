# StrataScratch Question ID: 2057 - Weight For First Shipment

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2057` |
| **Title** | **Weight For First Shipment** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Amazon** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2057) |

---

## 1. Problem Description

Write a query to find the weight for each shipment's earliest shipment date. Output the shipment id along with the weight.

---

## 2. Input Tables & Schema

```text
<amazon_shipment>
shipment_id             int
sub_id                  int
weight                  int
shipment_date           datetime
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or wind