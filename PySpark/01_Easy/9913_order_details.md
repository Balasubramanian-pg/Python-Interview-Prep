# StrataScratch Question ID: 9913 - Order Details

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9913` |
| **Title** | **Order Details** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9913) |

---

## 1. Problem Description

Find order details made by Jill and Eva.
Consider the Jill and Eva as first names of customers.
Output the order date, details and cost along with the first name.
Order records based on the customer id in ascending order.

---

## 2. Input Tables & Schema

```text
<customers>
id                          int
first_name                  varchar
last_name                   varchar
city                        varchar
address                     varchar
phone_number                varchar

<orders>
id                          int
cust_id                     int
order_date                  datetime
order_details               varchar
total_order_cost            int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - 