# StrataScratch Question ID: 10046 - Top 5 States With 5 Star Businesses

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10046` |
| **Title** | **Top 5 States With 5 Star Businesses** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Meta / Facebook** |
| **Category** | `Window Functions & Ranking` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10046) |

---

## 1. Problem Description

Find the top 5 states with the most 5 star businesses. Output the state name along with the number of 5-star businesses and order records by the number of 5-star businesses in descending order. In case there are ties in the number of businesses, return all the unique states. If two states have the same result, sort them in alphabetical order.

---

## 2. Input Tables & Schema

```text
Table
yelp_business
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

state	n_businesses
AZ	10
ON	5
NV	4
IL	3
OH	3
yelp_business
Preview
business_id	name	neighborhood	address	city	state	postal_code	latitude	longitude	stars	review_count	is_open	categories
G5ERFWvPfHy7IDAUYlWL2A	All Colors Mobile Bumper Repair		7137 N 28th Ave	Phoenix	AZ	85051	33.45	-112.07	1	4	1	Auto Detailing;Automotive
0jDvRJS-z9zdMgOUXgr6rA	Sunfare		811 W Deer Valley Rd	Phoenix	AZ	85027	33.68	-112.08	5	27	1	Personal Chefs;Food;Gluten-Free;Food Delivery Services;Event Planning & Services;Restaurants
6HmDqeNNZtHMK0t2glF_gg	Dry Clean Vegas	Southeast	2550 Windmill Ln, Ste 100	Las Vegas	NV	89123	36.04	-115.12	1	4	1	Dry Cleaning & Laundry;Laundry Services;Local Services;Dry Cleaning
pbt3SBcEmxCfZPdnmU9tNA	The Cuyahoga Room		740 Munroe Falls Ave	Cuyahoga Falls	OH	44221	41.14	-81.47	1	3	0	Wedding Planning;Caterers;Event Planning & Services;Venues & Event Spaces
CX8pfLn7Bk9o2-8yDMp_2w	The UPS Store		4815 E Carefree Hwy, Ste 108	Cave Creek	AZ	85331	33.8	-111.98	1.5	5	1	Notaries;Printing Services;Local Services;Shipping Centers
yzAB_pRwk8FJl3aILiiySA	CenturyLink	Spring Valley	4850 S Fort Apache Rd, Ste 100	Las Vegas	NV	89147	36.1	-115.3	1.5	35	0	Home Services;Television Service Providers;Professional Services;Internet Service Providers;Utilities
p8keQs0xw0TzP0JjYPiZPQ	The Enfield Fox		285 Enfield Place	Mississauga	ON	L5B 3Y6	43.59	-79.64	1.5	3	0	Bars;Restaurants;Pubs;British;Nightlife
lbxfIXUNUdSRO2t7z2PxPA	Budget Car Rental		7125 E Shea Blvd, Ste 101	Scottsdale	AZ	85254	33.58	-111.93	2	6	1	Hotels & Travel;Car Rental
xxCrRqqICzQyR0Q-iqCrNw	Subway	Plaza Midwood	1300 The Plz	Charlotte	NC	28205	35.22	-80.81	2	13	1	Fast Food;Sandwiches;Restaurants
WdQP8kl9SzcOdubWz0Rs5g	Red Beard Bodywork And Structural Integration	Capitol	301 S Bedford St	Madison	WI	53703	43.07	-89.39	5	10	1	Rolfing;Health & Medical;Beauty & Spas;Massage
g6KfICYxIFoXnz7KHzQDpw	Chase Bank		705 S Green Valley Pkwy	Henderson	NV	89052	36	-115.08	2	6	1	Financial Services;Banks & Credit Unions
Lhtl6hEr4BaAR4aA3RQDNQ	Dairy Queen		475 W Craig Rd	North Las Vegas	NV	89032	36.24	-115.15	2	57	1	Food;Ice Cream & Frozen Yogurt
6FmJM2SYWoUv_DC8FA7hpg	1st Choice Storage Solutions	Southeast	6360 S Pecos Rd, Ste 14	Las Vegas	NV	89120	36.07	-115.1	2	7	0	Shopping;Home & Garden;Home Services;Cabinetry;Furniture Stores
JJWQxF7ljXKVvCxn3ug-CA	Applebee's Neighborhood Grill & Bar		13756 W Bell Rd	Surprise	AZ	85374	33.64	-112.36	2.5	56	1	Burgers;Bars;American (Traditional);Nightlife;Restaurants;Sports Bars;Steakhouses
3rptIkeGoVRdPF4v6omLOg	Sunless Boutique	The Lakes	9921 Mahogany Grove Ln	Las Vegas	NV	89117	36.14	-115.31	5	20	1	Hair Removal;Beauty & Spas;Skin Care;Tanning;Spray Tanning;Hair Salons
JGvyv9jO8kfEnf4WtnpzfQ	Dairy Queen		13623 W Camino Del Sol	Sun City West	AZ	85375	33.65	-112.36	2.5	16	1	Restaurants;Ice Cream & Frozen Yogurt;Fast Food;Food
dRb2Xq8jorJV6tDCgmaQUg	Papa John's Pizza		703 E Bell Rd	Phoenix	AZ	85022	33.64	-112.07	5	3	1	Restaurants;Pizza
r7MJN_4aJdNP_mx6u_4czQ	Red Roof Inn		7400 W Boston St	Chandler	AZ	85226	33.3	-111.97	2.5	3	0	Hotels;Hotels & Travel;Event Planning & Services
_QEwts97jzVcvfVo4qveFA	Integrated Pain Specialists	Spring Valley	9333 W Sunset Rd, Ste A	Las Vegas	NV	89148	36.07	-115.3	2.5	8	0	Health & Medical;Physical Therapy
-M9S1wlZTvv6T9EOo5X2Yw	Grandeur Palace	Scarborough	2301 Brimley Road, Unit 128	Toronto	ON	M1S 5B8	43.8	-79.27	2.5	46	1	Restaurants;Seafood;Chinese;Dim Sum
-03HVYxkeYWaafEpNJo1SA	GoodLife Vapes	Mount Pleasant and Davisville	2095 Yonge Street	Toronto	ON	M4S 2A5	43.7	-79.4	5	5	1	Vape Shops;Shopping;Electronics;Tobacco Shops
Wd81DI2DICRtANydqJlFtQ	Brock Doors and Windows		278 Orenda Road	Brampton	ON	L6T 4X6	43.7	-79.72	5	3	1	Home Services;Windows Installation;Garage Door Services;Contractors
zXY_rBLlE2Kb_D1FZ8bH9g	Crabby Joe's		450 Holland Street W	Bradford	ON	L3Z 0G1	44.11	-79.59	2.5	5	1	Bars;Restaurants;Nightlife;American (Traditional);Burgers
aYSSqa0M5DZHjLT_jK5ezw	Amego Electric Vehicles		533 Richmond Street W	Toronto	ON	M5V 3Y1	43.65	-79.4	2.5	3	1	Bike Rentals;Motorcycle Dealers;Active Life;Shopping;Bikes;Sporting Goods;Automotive
diH4Pf4mYd1P-zZsQErVTQ	PetSmart		7077 E Mayo Blvd Ste 140	Phoenix	AZ	85054	33.65	-111.93	3	28	1	Pet Training;Pet Stores;Pets;Pet Groomers;Pet Services;Pet Sitting
OZC42gnhlJ_auXduDRfMoQ	Scratch		1011 N 3rd St	Phoenix	AZ	85004	33.46	-112.07	3	40	0	French;Restaurants
m5h7_IeiGaY4Z1ns1y8veQ	Arizona Custom Canine			Phoenix	AZ	85086	33.84	-112.12	5	13	1	Dog Walkers;Pet Training;Pet Services;Pets;Pet Sitting
U1QABk2PSkzTfHfPb_tZgA	Visionworks		Fiesta Mall, 1445 W Southern Ave, Ste 2192	Mesa	AZ	85202	33.39	-111.86	3	8	0	Health & Medical;Shopping;Eyewear & Opticians;Optometrists
IiKKDb5sS1KIAf5jjfmApg	Sun Valley Hand Surgery		15830 N 35th Ave, Ste 2	Phoenix	AZ	85053	33.63	-112.13	5	4	0	Doctors;Orthopedists;Health & Medical;Sports Medicine
rkSUOnANSaB3E9qMHhfpcA	Schwan's			Phoenix	AZ		33.45	-112.07	3	3	1	Ice Cream & Frozen Yogurt;Food
xhzUfaJ9BTa3EbD0bTeKWQ	IHOP		10662 E Southern Ave	Mesa	AZ	85209	33.39	-111.6	3	45	1	Breakfast & Brunch;Restaurants;American (New);American (Traditional)
JbWQtVLQDEOBlvbVWk2OFg	Chipotle Mexican Grill		903 W Anthony Dr, Ste A	Champaign	IL	61820	40.14	-88.26	5	40	1	Fast Food;Mexican;Restaurants
J8DxZ7enKZ0aAuF40e3rew	Charlotte Dentist: Joseph LoParo, DMD	Uptown	400 S Tryon St, Ste M-4	Charlotte	NC	28202	35.22	-80.85	3	4	1	Health & Medical;Cosmetic Dentists;Dentists;General Dentistry
zPSPUa9cgl68ydGNZt6gYQ	Thrifty Car Rental		5330 Wilkinson Blvd	Charlotte	NC	28208	35.23	-80.93	3	9	1	Car Rental;Hotels & Travel
