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
Natalie Portman	drama	6.9	Breaking the Silence	2018-07-16	Meta
Tom Hardy	drama	9	Time’s Edge	2023-01-19	Amazon
Leonardo DiCaprio	sci-fi	8	Shadow Realm	2016-08-08	Amazon
Scarlett Johansson	comedy	9	Veil of Secrets	2017-12-12	Disney
Meryl Streep	romance	9.6	Deep Impact	2019-01-22	Google
Scarlett Johansson	thriller	9	Breaking the Silence	2016-03-25	Google
Scarlett Johansson	sci-fi	8.9	Edge of Memory	2019-04-26	Meta
Meryl Streep	romance	8.1	Veil of Secrets	2015-02-17	Disney
Ryan Gosling	sci-fi	9	Echoes of War	2022-03-10	Amazon
Ryan Gosling	action	9	Shadow Realm	2015-01-14	Disney
Tom Hardy	thriller	9.2	Bound by Honor	2016-03-11	Warner Bros
Tom Hardy	sci-fi	8.9	Crimson Chase	2016-09-18	Amazon
Scarlett Johansson	thriller	9	Bound by Honor	2015-01-03	Apple
Natalie Portman	romance	6.1	Frozen Horizon	2018-06-13	Google
Emma Stone	comedy	9.5	Edge of Memory	2015-12-17	Disney
Jennifer Lawrence	drama	9	Veil of Secrets	2016-05-30	Google
Jennifer Lawrence	thriller	9	Bound by Honor	2021-10-20	Meta
Leonardo DiCaprio	thriller	9	Crimson Chase	2022-12-30	Amazon
Chris Evans	sci-fi	8.6	Shadow Realm	2020-10-20	Meta
Ryan Gosling	comedy	9	The Silent Voice	2015-03-28	Apple
Denzel Washington	comedy	8.4	Whispers in the Wind	2015-10-18	Disney
Emma Stone	comedy	6.3	Breaking the Silence	2018-09-15	Netflix
Denzel Washington	comedy	7.1	Chasing Infinity	2017-05-27	Apple
Scarlett Johansson	sci-fi	9	Time’s Edge	2021-06-18	Meta
Leonardo DiCaprio	romance	9.2	Crimson Chase	2016-01-22	Netflix
Chris Evans	action	7.7	Shadow Realm	2023-03-06	Netflix
Ryan Gosling	drama	9	The Silent Voice	2016-03-23	Google
Leonardo DiCaprio	comedy	8.1	Nightfall	2019-09-25	Google
Tom Hardy	romance	9.3	Edge of Memory	2019-12-21	Warner Bros
Denzel Washington	drama	6.2	Veil of Secrets	2015-03-02	Netflix
Leonardo DiCaprio	comedy	7.6	Chasing Infinity	2017-05-25	Warner Bros
Chris Evans	drama	6.7	Whispers in the Wind	2019-05-19	Amazon
Jennifer Lawrence	action	8.9	Veil of Secrets	2022-06-04	Disney
Jennifer Lawrence	comedy	9	Crimson Chase	2015-08-28	Apple
Denzel Washington	drama	9	Breaking the Silence	2015-07-25	Apple
Jennifer Lawrence	thriller	9	Bound by Honor	2016-10-06	Netflix
actor_name:
string
genre:
string
movie_rating:
double
movie_title:
string
release_date:
date
production_company:
string
```

---

## 3. Interview Strategy & Logic

1. **Requirement Analysis**:
   - Understand the primary entity and granularity required in the final output.
   - Filter down the dataset early if specific cond