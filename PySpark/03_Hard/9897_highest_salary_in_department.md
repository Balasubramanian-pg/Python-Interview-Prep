# StrataScratch Question ID: 9897 - Highest Salary In Department

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9897` |
| **Title** | **Highest Salary In Department** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9897) |

---

## 1. Problem Description

Find the employee with the highest salary per department.
Output the department name, employee's first name along with the corresponding salary.

---

## 2. Input Tables & Schema

```text
[employee]
id                      int
first_name              varchar
last_name               varchar
age                     int
sex                     varchar
employee_title          varchar
department              varchar
salary                  int
target                  int
bonus                   int
email                   varchar
city                    varchar
address                 varchar
manager_id              int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the