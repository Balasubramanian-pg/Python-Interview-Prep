# StrataScratch Question ID: 10297 - Comments Distribution

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10297` |
| **Title** | **Comments Distribution** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10297) |

---

## 1. Problem Description

Write a query to calculate the distribution of comments by the count of users that joined Facebook between 2018 and 2020, for the month of January 2020.

The output should contain a count of comments and the corresponding number of users that made that number of comments in Jan-2020. For example, you'll be counting how many users made 1 comment, 2 comments, 3 comments, 4 comments, etc in Jan-2020. Your left column in the output will be the number of comments while your right column in the output will be the number of users. Sort the output from the least number of comments to highest.

To add some complexity, there might be a bug where an user post is dated before the user join date. You'll want to remove these posts from the result.

---

## 2. Input Tables & Schema

```text
<fb_users>
id                  int
name                varchar
joined_at           datetime
city_id             int
device              int

<fb_comments>
user_id             int
body                varchar
created_at          datetime
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Optimizer to optimize query execution plans