# StrataScratch Question ID: 2049 - Total Order Per Status Per Service

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2049` |
| **Title** | **Total Order Per Status Per Service** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Uber** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2049) |

---

## 1. Problem Description

Uber is interested in identifying gaps in their business. Calculate the count of orders for each status of each service. Your output should include the service name, status of the order, and the number of orders.

---

## 2. Input Tables & Schema

```text
<uber_orders>
order_date              datetime
number_of_orders        int
status_of_order         varchar
monetary_value          float
service_name            varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the p