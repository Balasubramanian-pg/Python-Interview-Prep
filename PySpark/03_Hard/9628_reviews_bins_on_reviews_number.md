# StrataScratch Question ID: 9628 - Reviews Bins On Reviews Number

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9628` |
| **Title** | **Reviews Bins On Reviews Number** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Airbnb** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9628) |

---

## 1. Problem Description

To better understand the effect of the review count on the price, categorize the number of reviews into the following groups along with the price.
    0 reviews: NO
    1 to 5 reviews: FEW
    6 to 15 reviews: SOME
    16 to 40 reviews: MANY
    more than 40 reviews: A LOT

Table:
<airbnb_search_details>
id                          int
price                       float
property_type               varchar
room_type                   varchar
amenities                   varchar
accommodates                int
bathrooms                   int
bed_type                    varchar
cancellation_policy         varchar
cleaning_fee                bool
city                        varchar
host_identity_verified      varchar
host_response_rate          varchar
host_since                  datetime
neighbourhood               varchar
number_of_reviews           int
review_scores_rating        float
zipcode                     in