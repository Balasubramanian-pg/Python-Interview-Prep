# StrataScratch Question ID: 10026 - Aroma-based Winery Search.

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10026` |
| **Title** | **Aroma-based Winery Search.** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10026) |

---

## 1. Problem Description

Find all wineries which produce wines by possessing aromas of plum, cherry, rose, or hazelnut.
Output unique winery values only.

---

## 2. Input Tables & Schema

```text
<winemag_p1>
id                  int
country             varchar
description         varchar
designation         varchar
points              int
price               float
province            varchar
region_1            varchar
region_2            varchar
variety             varchar
winery              varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and g