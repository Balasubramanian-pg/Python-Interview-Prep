# StrataScratch Question ID: 2063 - Change Of Currency Exchange Rates

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2063` |
| **Title** | **Change Of Currency Exchange Rates** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Salesforce** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2063) |

---

## 1. Problem Description

You are given a list of exchange rates from various currencies to US Dollars (USD) in different months. Show how the exchange rate of all the currencies changed in the first half of 2020. Output the currency code and the difference between values of the exchange rate between July 1, 2020 and January 1, 2020.

---

## 2. Input Tables & Schema

```text
<sf_exchange_rate>
source_currency         varchar
target_currency         varchar
exchange_rate           float
date                    datetime
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API trans