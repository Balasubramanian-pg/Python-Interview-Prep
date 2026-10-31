# StrataScratch Question ID: 9636 - Cheapest Neighborhoods With Real Beds And Internet

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9636` |
| **Title** | **Cheapest Neighborhoods With Real Beds And Internet** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Filtering & Conditional Logic` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9636) |

---

## 1. Problem Description

Find neighborhoods where you can sleep on a real bed in a villa with internet while paying the lowest price possible.

---

## 2. Input Tables & Schema

```text
<airbnb_search_details>
id                      int
price                   float
property_type           varchar
room_type               varchar
amenities               varchar
accommodates            int
bathrooms               int
bed_type                varchar
cancellation_policy     varchar
cleaning_fee            bool
city                    varchar
host_identity_verified  varchar
host_response_rate      varchar
host_since              datetime
neighbourhood           varchar
number_of_reviews       int
review_scores_rating    float
zipcode                 int
bedrooms                int
beds                    int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis*