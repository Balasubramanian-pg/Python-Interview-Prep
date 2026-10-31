# StrataScratch Question ID: 9782 - Customer Revenue In March

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9782` |
| **Title** | **Customer Revenue In March** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9782) |

---

## 1. Problem Description

Calculate the total revenue from each customer in March 2019.

Output the revenue along with the customer id and sort the results based on the revenue in descending order.

---

## 2. Input Tables & Schema

```text
<orders>
id                  int
cust_id             int
order_date          datetime
order_details       varchar
total_order_cost    int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `wit