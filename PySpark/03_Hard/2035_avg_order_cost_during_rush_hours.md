# StrataScratch Question ID: 2035 - Avg Order Cost During Rush Hours

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2035` |
| **Title** | **Avg Order Cost During Rush Hours** |
| **Difficulty** | `Hard` |
| **Company Tag** | **DoorDash** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2035) |

---

## 1. Problem Description

Write a query that returns the average order cost per hour during hours 3 PM -6 PM (15-18) in San Jose. For calculating time period use 'Customer placed order datetime' field. Earnings value is 'Order total' field. Order output by hour.

---

## 2. Input Tables & Schema

```text
<doordash_delivery>
customer_placed_order_datetime          datetime
placed_order_with_restaurant_datetime   datetime
driver_at_restaurant_datetime           datetime
delivered_to_consumer_datetime          datetime
driver_id                               int
restaurant_id                           int
consumer_id                             int
is_new                                  bool
delivery_region                         varchar
is_asap                                 bool
order_total                             float
discount_amount                         float
tip_amount                              float
refunded_amount                