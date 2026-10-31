# StrataScratch Question ID: 2102 - Flags Per Video

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2102` |
| **Title** | **Flags Per Video** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2102) |

---

## 1. Problem Description

For each video, find how many unique users flagged it. A unique user can be identified using the combination of their first name and last name. Do not consider rows in which there is no flag ID.

---

## 2. Input Tables & Schema

```text
Table
user_flags
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

video_id	num_unique_users
y6120QOlsfU	5
5qap5aO4i9A	2
Ct6BUPvE2sM	2
dQw4w9WgXcQ	5
jNQXAC9IVRw	3
user_flags
Preview
user_firstname	user_lastname	video_id	flag_id
Richard	Hasson	y6120QOlsfU	0cazx3
Mark	May	Ct6BUPvE2sM	1cn76u
Gina	Korman	dQw4w9WgXcQ	1i43zk
Mark	May	Ct6BUPvE2sM	1n0vef
Mark	May	jNQXAC9IVRw	1sv6ib
Gina	Korman	dQw4w9WgXcQ	20xekb
Mark	May	5qap5aO4i9A	4cvwuv
Daniel	Bell	5qap5aO4i9A	4sd6dv
Richard	Hasson	y6120QOlsfU	6jjkvn
Pauline	Wilks	jNQXAC9IVRw	7ks264
Courtney		dQw4w9WgXcQ	
Helen	Hearn	dQw4w9WgXcQ	8946nx
Mark	