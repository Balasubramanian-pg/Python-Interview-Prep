# StrataScratch Question ID: 10310 - Class Performance

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10310` |
| **Title** | **Class Performance** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10310) |

---

## 1. Problem Description

You are given a table containing assignment scores of students in a class. Write a query that identifies the largest difference in total score  of all assignments.
Output just the difference in total score (sum of all 3 assignments) between a student with the highest score and a student with the lowest score.

---

## 2. Input Tables & Schema

```text
(box_scores)
id          int
student     varchar
assignment1 int
assignment2 int
assignment3 int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strat