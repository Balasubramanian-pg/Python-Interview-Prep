# StrataScratch Question ID: 10060 - Top Cool Votes

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10060` |
| **Title** | **Top Cool Votes** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Yelp** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10060) |

---

## 1. Problem Description

Find the review_text that received the highest number of  'cool' votes.
Output the business name along with the review text with the highest numbef of 'cool' votes.

---

## 2. Input Tables & Schema

```text
<yelp_reviews>
business_name       varchar
review_id           varchar
user_id             varchar
stars               varchar
review_date         datetime
review_text         varchar
funny               int
useful              int
cool                int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity requir