# StrataScratch Question ID: 10176 - Bikes Last Used

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10176` |
| **Title** | **Bikes Last Used** |
| **Difficulty** | `Easy` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10176) |

---

## 1. Problem Description

Find the last time each bike was in use. Output both the bike number and the date-timestamp of the bike's last use (i.e., the date-time the bike was returned). Order the results by bikes that were most recently used.

---

## 2. Input Tables & Schema

```text
<dc_bikeshare_q1_2012>
duration                    varchar
duration_seconds            int
start_time                  datetime
start_station               varchar
start_terminal              int
end_time                    datetime
end_station                 varchar
end_terminal                int
bike_number                 varchar
rider_type                  varchar
id                          int
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down