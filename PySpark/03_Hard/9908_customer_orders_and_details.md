# StrataScratch Question ID: 9908 - Customer Orders And Details

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9908` |
| **Title** | **Customer Orders And Details** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9908) |

---

## 1. Problem Description

Find the number of orders, the number of customers, and the total cost of orders for each city. Only include cities that have made at least 5 orders and count all customers in each city even if they did not place an order.

Output each calculation along with the corresponding city name.

---

## 2. Input Tables & Schema

```text
<customers>
id                  int
first_name          varchar
last_name           varchar
city                varchar
address             varchar
phone_number        varchar

orders
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
   - Utilize native DataFrame API transformations (`select`,