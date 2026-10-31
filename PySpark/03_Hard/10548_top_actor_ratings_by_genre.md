# StrataScratch Question ID: 10548 - Top Actor Ratings By Genre

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10548` |
| **Title** | **Top Actor Ratings By Genre** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10548) |

---

## 1. Problem Description

Find the top actors based on their average movie rating within the genre they appear in most frequently.
•  For each actor, determine their most frequent genre (i.e., the one they’ve appeared in the most).
•   If there is a tie in genre count, select the genre where the actor has the highest average rating.
•   If there is still a tie in both count and rating, include all tied genres for that actor.


Rank the resulting actor + genre pairs by their average rating in descending order.
•  Return all actor + genre pairs that fall within the top 3 ranks (not rows), including ties.
•  Do not skip ranks — for example, if multiple actors are tied at rank 1, the next rank is 2.

---

## 2. Input Tables & Schema

```text
Table
top_actors_rating
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

actor_name	genre	avg_rating
Tom Hardy	romance	9.3
Jennifer Lawrence	thriller	9
Ryan Gosling	drama	9
Scarlett Johansson	thriller	9
Meryl Streep	romance	8.85
top_actors_rating
Preview
actor_name	genre	movie_rating	movie_title	release_date	production_company
Ryan Gosling	drama	9	Urban Hunt	2017-07-03	Google
Ryan Gosling	sci-fi	8.9	Veil of Secrets	2015-12-23	Apple
Chris Evans	drama	6.1	Crimson Chase	2017-08-10	Apple
Meryl Streep	drama	8.2	Veil of Secrets	2019-09-15	Google
Jennifer Lawrence	thriller	9	Whispers in the Wind	2016-10-15	Disney
Chris Evans	action	7.1	Crimson Chase	2018-10-10	Netflix
Ryan Gosling	romance	8.9	Frozen Horizon	2021-10-08	Amazon
Emma Stone	sci-fi	7.8	The Last Stand	2019-03-31	Netflix
Denzel Washington	action	9.3	Eternal Ember	2019-01-21	Apple
Leonardo DiCaprio	sci-fi	6.3	Urban Hunt	2018-03-31	Netflix
Leonardo DiCaprio	drama	7.5	Shadow Realm	2022-02-16	Warner Bros
Natalie Portman	comedy	7.5	Crimson Chase	2022-07-08	Amazon
Ryan Gosling	thriller	9	Veil of Secrets	2023-03-06	Google
Scarlett Johansson	romance	8.9	Veil of Secrets	2017-06-18	Disney
Natalie Portman	drama	6.9	Breaking th