# StrataScratch Question ID: 10284 - Popularity Percentage

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10284` |
| **Title** | **Popularity Percentage** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10284) |

---

## 1. Problem Description

Find the popularity percentage for each user on Meta/Facebook. The dataset contains two columns, user1 and user2, which represent pairs of friends. Each row indicates a mutual friendship between user1 and user2, meaning both users are friends with each other. A user's popularity percentage is calculated as the total number of friends they have (counting connections from both user1 and user2 columns) divided by the total number of unique users on the platform. Multiply this value by 100 to express it as a percentage.


Output each user along with their calculated popularity percentage. The results should be ordered by user ID in ascending order.

---

## 2. Input Tables & Schema

```text
Table
facebook_friends
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

user1	popularity
1	55.56
2	33.33
3	33.33
