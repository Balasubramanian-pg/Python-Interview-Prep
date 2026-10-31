# StrataScratch Question ID: 10301 - Expensive Projects

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10301` |
| **Title** | **Expensive Projects** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Microsoft** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10301) |

---

## 1. Problem Description

Given a list of projects and employees mapped to each project, calculate by the amount of project budget allocated to each employee . The output should include the project title and the project budget per employee as an integer. Order your list by projects with the highest budget per employee first.

---

## 2. Input Tables & Schema

```text
<ms_projects>
id                  int
title               varchar
budget              int

<ms_emp_projects>
emp_id              int
project_id          int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculation