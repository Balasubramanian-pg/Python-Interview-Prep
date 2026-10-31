# StrataScratch Question ID: 9781 - Processed Ticket Rate By Type

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9781` |
| **Title** | **Processed Ticket Rate By Type** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9781) |

---

## 1. Problem Description

Find the processed rate of tickets for each type. The processed rate is defined as the number of processed tickets divided by the total number of tickets for that type. Round this result to two decimal places.

---

## 2. Input Tables & Schema

```text
Table
facebook_complaints
More about this question
Hints
Expected Output
facebook_complaints
Preview
complaint_id	type	processed
0	0	TRUE
1	0	TRUE
2	0	FALSE
3	1	TRUE
4	1	TRUE
5	1	FALSE
complaint_id:
bigint
type:
bigint
processed:
boolean
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional f