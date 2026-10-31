# StrataScratch Question ID: 10285 - Acceptance Rate By Date

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10285` |
| **Title** | **Acceptance Rate By Date** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10285) |

---

## 1. Problem Description

Calculate the friend acceptance rate for each date when friend requests were sent. A request is sent if action = sent and accepted if action = accepted. If a request is not accepted, there is no record of it being accepted in the

---

## 2. Input Tables & Schema

```text
table. The output will only include dates where requests were sent and at least one of them was accepted, as the acceptance rate can only be calculated for those dates. Show the results ordered from the earliest to the latest date.

Table
fb_friend_requests
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

request_date	percentage_acceptance
2020-01-04	0.75
2020-01-06	0.67
fb_friend_requests
Preview
user_id_sender	user_id_receiver	date	action
ad4943sdz	948ksx123d	2020-01-04	sent
ad4943sdz	948ksx123d	2020-01-06	accepted
dfdfxf9483	9djjjd9283	2020-01-04	sent
dfdfxf9483	9djjjd9283	2020-01-15	accepted
ffdfff4234234	lpjzjdi4949	2020-01-06	sent
fffkfld9499	993lsldidif	2020-01-06	sent
fffkfld9499	993lsldidif	2020-01-10	accepted
fg503kdsdd	ofp049dkd	2020-01-04	sent
fg503kdsdd	ofp049dkd	2020-01-10	accepted
hh643dfert	847