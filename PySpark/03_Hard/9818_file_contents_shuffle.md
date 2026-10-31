# StrataScratch Question ID: 9818 - File Contents Shuffle

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9818` |
| **Title** | **File Contents Shuffle** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Google** |
| **Category** | `Data Transformation & Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9818) |

---

## 1. Problem Description

Sort the words alphabetically in 'final.txt' and make a new file named 'wacky.txt'. Output the file contents in one column and the filename 'wacky.txt' in another column.

* If coding in python, the file contents should be contained in a list.

---

## 2. Input Tables & Schema

```text
<google_file_store>
filename            varchar
contents            varchar
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific conditional flags or date ranges are specified.
2. **PySpark Optimization Strategy**:
   - Utilize native DataFrame API transformations (`select`, `filter`, `groupBy`, `withColumn`) to allow the Catalyst Op