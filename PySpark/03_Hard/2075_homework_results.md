# StrataScratch Question ID: 2075 - Homework Results

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2075` |
| **Title** | **Homework Results** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2075) |

---

## 1. Problem Description

Given the homework results of a group of students, calculate the average grade and the completion rate of each student. A homework is considered not completed if no grade has been assigned.
Output first name of a student, their average grade, and completion rate in percentages. Note that it's possible for several students to have the same first name but their results should still be shown separately.

---

## 2. Input Tables & Schema

```text
<allstate_homework>
student_id              int
homework_id             int
grade                   float

<allstate_students>
student_id              int
student_firstname       varchar
student_lastname        varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans.
   - If ranking or windowed calculations are needed, define explicit partition keys and order expressions using `pyspark.sql.window.Window`.
   - Avoid collecting large DataFrames to the driver node; utilize distributed operations until final aggregations.

---

## 4. PySpark DataFrame API Solution

```python
# Import y