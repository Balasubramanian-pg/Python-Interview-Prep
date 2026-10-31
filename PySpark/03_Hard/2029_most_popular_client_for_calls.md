# StrataScratch Question ID: 2029 - Most Popular Client For Calls

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `2029` |
| **Title** | **Most Popular Client For Calls** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/2029) |

---

## 1. Problem Description

Select the most popular client_id based on the number of users who individually have at least 50% of their events from the following list: 'video call received', 'video call sent', 'voice call received', 'voice call sent'.

---

## 2. Input Tables & Schema

```text
Table
fact_events
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

CLIENT_ID
desktop
fact_events
Preview
id	time_id	user_id	customer_id	client_id	event_type	event_id
1	2020-02-28	3668-QPYBK	Sendit	desktop	message sent	3
2	2020-02-28	7892-POOKP	Connectix	mobile	file received	2
3	2020-04-03	9763-GRSKD	Zoomit	desktop	video call received	7
4	2020-04-02	9763-GRSKD	Connectix	desktop	video call received	7
5	2020-02-06	9237-HQITU	Sendit	desktop	video call received	7
6	2020-02-27	8191-XWSZG	Connectix	desktop	file received	2
7	2020-04-03	9237-HQITU	Connectix	desktop	video call received	7
8	2020-03-01	9237-HQITU	Connectix	mobile	message received	4
9	2020-04-02	4190-MFLUW	Connectix	mobile	video call received	7
10	2020-04-21	9763-GRSKD	Sendit	desktop	file received	2
11	2020-02-28	5129-JLPIS	Electric Gravity	mobile	video call started	6
12	2020-03-31	6713-OKOMC	Connectix	desktop	file received	2
13	2020-03-21	6388-TABGU	Connectix	desktop	message sent	3
14	2020-03-03	7469-LKBCI	Connectix	mobile	video call received	7
15	2020-02-11	9237-HQITU	Connectix	desktop	video call received	7
16	2020-03-01	5575-GNVDE	Zoomit	desktop	file received	2
17	2020-03-02	6388-TABGU	Connectix	desktop	message sent	3
18	2020-04-06	9305-CDSKC	Connectix	desktop	message received	4
19	2020-02-13	3668-QPYBK	Connectix	mobile	file sent	1
20	2020-04-03	9959-WOFKT	Connectix	desktop	file received	2
21	2020-03-15	9305-CDSKC	Zoomit	mobile	message received	4
22	2020-04-01	7892-POOKP	eShop	mobile	voice call started	8
23	2020-04-09	8191-XWSZG	Connectix	mobile	file received	2
24	2020-04-08	3668-QPYBK	eShop	desktop	message sent	3
25	2020-03-05	8191-XWSZG	Zoomit	mobile	file received	2
26	2020-02-24	3668-QPYBK	Connectix	mobile	api message received	5
27	2020-03-26	6388-TABGU	Zoomit	desktop	message received	4
28	2020-02-03	7795-CFOCW	Connectix	mobile	api message received	5
29	2020-03-19	7892-POOKP	Connectix	desktop	message received	4
30	2020-04-07	9763-GRSKD	Connectix	mobile	message sent	3
31	2020-04-06	9959-WOFKT	Connectix	desktop	message received	4
32	2020-02-15	9237-HQITU	Connectix	mobile	message sent	3
33	2020-04-06	4183-MYFRB	Sendit	desktop	file received	2
34	2020-03-13	9305-CDSKC	Connectix	desktop	video call received	7
35	2020-04-05	9959-WOFKT	Connectix	mobile	message received	4
36	2020-03-28	6388-TABGU	Connectix	desktop	message sent	3
37	2020-04-03	4183-MYFRB	Connectix	desktop	message received	4
38	2020-03-15	5575-GNVDE	Electric Gravity	desktop	video call started	6
39	2020-03-06	8091-TTVAX	Zoomit	desktop	file received	2
40	2020-03-25	4190-MFLUW	Connectix	mobile	file received	2
41	2020-04-13	9959-WOFKT	Zoomit	mobile	video call received	7
42	2020-02-20	7590-VHVEG	Sendit	desktop	file received	2
43	2020-03-13	9305-CDSKC	Connectix	mobile	voice call received	9
44	2020-02-22	1452-KIOVK	Zoomit	mobile	voice call started	8
45	2020-04-18	9959-WOFKT	Connectix	desktop	file received	2
46	2020-02-04	9305-CDSKC	Connectix	desktop	message sent	3
47	2020-04-06	4190-MFLUW	Connectix	mobile	file sent	1
48	2020-03-22	1452-KIOVK	Connectix	mobile	file sent	1
49	2020-04-06	5129-JLPIS	Sendit	desktop	message sent	3
50	2020-04-04	7469-LKBCI	Sendit	mobile	message received	4
51	2020-02-14	3668-QPYBK	Connectix	desktop	message received	4
52	2020-03-28	5575-GNVDE	Sendit	desktop	file received	2
53	2020-04-05	8091-TTVAX	Connectix	desktop	message sent	3
54	2020-03-01	7469-LKBCI	Connectix	desktop	video call started	6
55	2020-0