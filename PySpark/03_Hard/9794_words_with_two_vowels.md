# StrataScratch Question ID: 9794 - Words With Two Vowels

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9794` |
| **Title** | **Words With Two Vowels** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9794) |

---

## 1. Problem Description

Find all words which contain exactly two vowels in any list in the table.

Table:
<google_word_lists>
words1              varchar
words2              varchar

---

## 2. Input Tables & Schema

```text
Dataset provided by StrataScratch environment for Question ID 9794.
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sq