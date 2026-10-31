# StrataScratch Question ID: 2036 - Lowest Revenue Generated Restaurants

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2036` |
| **Title** | **Lowest Revenue Generated Restaurants** |
| **Difficulty** | `Hard` |
| **Company Tag** | **DoorDash** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2036) |

---

## 1. Problem Description

Write a query that returns a list of the bottom 2% revenue generating restaurants. Return a list of restaurant IDs and their total revenue from when customers placed orders in May 2020.

You can calculate the total revenue by summing the order_total column. And you should calculate the bottom 2% by partitioning the total revenue into evenly distributed buckets.

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
refunded_amount                         float