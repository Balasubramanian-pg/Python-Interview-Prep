# StrataScratch Question ID: 10353 - Workers With The Highest Salaries

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10353` |
| **Title** | **Workers With The Highest Salaries** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10353) |

---

## 1. Problem Description

Find the titles of workers that earn the highest salary. Output the highest-paid title or multiple titles that share the highest salary.

---

## 2. Input Tables & Schema

```text
<worker>
worker_id               int
first_name              varchar
last_name               varchar
salary                  int
joining_date            datetime
department              varchar

title
worker_ref_id           int
worker_title            varchar
affected_from           datetime
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformation