# StrataScratch Question ID: 2099 - Election Results

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2099` |
| **Title** | **Election Results** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2099) |

---

## 1. Problem Description

The election is conducted in a city and everyone can vote for one or more candidates, or choose not to vote at all. Each person has 1 vote so if they vote for multiple candidates, their vote gets equally split across these candidates. For example, if a person votes for 2 candidates, these candidates receive an equivalent of 0.5 vote each. Some voters have chosen not to vote, which explains the blank entries in the dataset.


Find out who got the most votes and won the election. Output the name of the candidate or multiple names in case of a tie.
To avoid issues with a floating-point error you can round the number of votes received by a candidate to 3 decimal places.

---

## 2. Input Tables & Schema

```text
Table
voting_results
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

candidate
Christine 
voting_results
Preview
voter	candidate
Kathy	
Charles	Ryan 
Charles	Christine 
Charles	Kathy 
Benjamin	Christine 
Anthony	Paul 
Anthony	Anthony 
Edward	Ryan 
Edward	Paul 
Edward	Kathy 
Terry	
Nancy	Ryan 
Nancy	Nicole 
Nancy	Paul 
Nancy	Christine 
Nancy	Kathy 
Evelyn	Anthony 
Evelyn	Christine 
Evelyn	Paul 
Evelyn	Nicole 
Shirley	Ryan 
Shirley	Nicole 
Shirley	Kathy 
Shirley	Anthony 
Victor	
Bobby	Ryan 
Bobby	Christine 
Helen	Ryan 
Helen	Christine 
Helen	Kathy 
Helen	Nicole 
Kevin	Ryan 
Kevin	Kathy 
Kevin	Paul 
Betty	
Andrew	Ryan 
Andrew	Christine 
Martha	Ryan 
Martha	Anthony 
Marie	Anthony 
Alan	Christine 
Matthew	Nicole 
Matthew	Christine 
Arthur	
Joyce	
Ryan	Ryan 
Nicole	Nicole 
Paul	
Christine	Christine 
Christine	Ryan 
Kathy	Kathy 
Kathy	Christine 
Kathy	Ryan 
Kathy	Nicole 
Anthony	Anthony 
Anthony	Ryan 
Anthony	Paul 
voter:
string
candidate:
string
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
# 