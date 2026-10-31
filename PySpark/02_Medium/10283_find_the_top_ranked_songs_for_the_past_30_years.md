# StrataScratch Question ID: 10283 - Find The Top-ranked Songs For The Past 30 Years.

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10283` |
| **Title** | **Find The Top-ranked Songs For The Past 30 Years.** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10283) |

---

## 1. Problem Description

Find all the songs that were top-ranked (at first position) at least once in the past 30 years

---

## 2. Input Tables & Schema

```text
<billboard_top_100_year_end>
year                                int
year_rank                           int
group_name                          varchar
artist                              varchar
song_name                           varchar
id                                  int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filt