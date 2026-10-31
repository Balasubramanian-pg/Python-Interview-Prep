# StrataScratch Question ID: 10172 - Best Selling Item

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10172` |
| **Title** | **Best Selling Item** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10172) |

---

## 1. Problem Description

Find the best selling item for each month (no need to separate months by year) where the biggest total invoice was paid. The best selling item is calculated using the formula (unitprice * quantity). Output the description of the item along with the amount paid.

---

## 2. Input Tables & Schema

```text
(online_retail)
invoiceno       varchar
stockcode       varchar
description     varchar
quantity        int
invoicedate     datetime
unitprice       float
customerid      float
country         varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFr