# StrataScratch Question ID: 10087 - Find All Posts Which Were Reacted To With A Heart

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10087` |
| **Title** | **Find All Posts Which Were Reacted To With A Heart** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10087) |

---

## 1. Problem Description

Find all posts which were reacted to with a heart.

---

## 2. Input Tables & Schema

```text
<facebook_reactions>
poster                  int
friend                  int
reaction                varchar
date_day                int
post_id                 int

<facebook_posts>
post_id                 int
poster                  int
post_text               varchar
post_keywords           varchar
post_date               datetime
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataF