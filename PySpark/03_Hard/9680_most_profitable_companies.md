# StrataScratch Question ID: 9680 - Most Profitable Companies

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9680` |
| **Title** | **Most Profitable Companies** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9680) |

---

## 1. Problem Description

Find the 3 most profitable companies in the entire world.
Output the result along with the corresponding company name.
Sort the result based on profits in descending order.

---

## 2. Input Tables & Schema

```text
forbes_global_2010_2014
company             varchar
sector              varchar
industry            varchar
continent           varchar
country             varchar
marketvalue         float
sales               float
profits             float
assets              float
rank                int
forbeswebpage       varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down t