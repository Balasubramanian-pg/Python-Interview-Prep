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
ct1uN_FOIyY1er8iLTsS6w	Eyeglass World	Westside	3819 W Sahara Ave	Las Vegas	NV	89102	36.14	-115.19	5	52	1	Ophthalmologists;Health & Medical;Eyewear & Opticians;Shopping;Optometrists;Doctors
qngp1XfBYWi7lB5S9Mg5ZA	Metropolitan Home Design		15220 Madison Ave	Lakewood	OH	44107	41.48	-81.8	5	3	0	Interior Design;Home Services;Home & Garden;Shopping;Real Estate;Home Staging;Home Decor
cDpUshHyJHDEc19TSTulJw	Urbana Acupuncture		155-A Lincoln Square Mall	Urbana	IL	61801	40.11	-88.21	5	8	1	Naturopathic/Holistic;Traditional Chinese Medicine;Doctors;Acupuncture;Health & Medical
YjfRCKCTqkcL1yTKPIwDlg	Savers		3121 N Rancho Dr	Las Vegas	NV	89130	36.22	-115.21	3	29	1	Shopping;Thrift Stores;Fashion;Used;Vintage & Consignment
4m5g6GUGDN9NqkfA0dk9fA	Test America Preview Studios	The Strip	3667 Las Vegas Blvd S, Ste H-82, Desert Passage Mall at the Aladdin	Las Vegas	NV	89109	36.11	-115.17	3	10	1	Arts & Entertainment;Local Services
cMlHcrlADb5gRWwFaNKhjg	Samurai Sam's	Anthem	10075 S Eastern Ave, Ste 116	Henderson	NV	89052	36.01	-115.11	3	19	0	Asian Fusion;Japanese;Restaurants;Salad
Ett_hy5k5_hI4GvPN9cyHg	Ulta Beauty	Southeast	6689 Las Vegas Blvd S	Las Vegas	NV	89119	36.07	-115.17	5	24	1	Hair Salons;Blow Dry/Out Services;Beauty & Spas;Cosmetics & Beauty Supply;Hair Extensions;Shopping
MYB1ZMspBk1Xc_awp_PtSw	Naked City Pizza Express	Southwest	6935 Blue Diamond Rd	Las Vegas	NV	89178	36.02	-115.24	3	46	1	Sandwiches;Chicken Wings;Restaurants;Pizza
FBptd43MkPFZxVLRMz0PFw	Orangetheory Fitness Solon		6025 Kruse Dr	Solon	OH	44139	41.39	-81.44	3	4	1	Fitness & Instruction;Active Life;Gyms;Trainers;Interval Training Gyms;Boot Camps
iQfx6lghJJbrb-fz-toOCQ	Swarovski Canada	Etobicoke	25 The West Mall	Etobicoke	ON	M9C 1B8	43.61	-79.56	3	3	1	Home Decor;Shopping;Jewelry;Home & Garden
9O0jWqGnHkBsXMOd-KOl4w	Hot and Sour	East Credit	1010 Dreamcrest Road, Unit 2	Mississauga	ON	L5V 3A4	43.59	-79.68	3	20	1	Restaurants;Asian Fusion;Halal;Chinese
z7ns1g4S82kaBdIAC_RMRw	Subway		1000 Airport Blvd	Pittsburgh	PA	15231	40.49	-80.25	3	5	1	Sandwiches;Fast Food;Restaurants
VdoNOOcO8HmLHbmxE_3psA	Sonora Quest Laboratories		9305 W Thomas Rd, Ste 300	Phoenix	AZ	85037	33.48	-112.26	3.5	7	1	Medical Centers;Diagnostic Services;Health & Medical;Laboratory Testing
D3Tpd4SrPAnZ1PaGVRGBfQ	Weinstube Klink		Epplestr. 1 C	Stuttgart	BW	70597	48.75	9.17	3.5	3	1	German;Bars;Nightlife;Wine Bars;Restaurants
p3My4o49oL_aOY2M2QLu8w	The Chanter	Old Town	30 - 32 Bread Street	Edinburgh	EDH	EH3 9AF	55.95	-3.2	5	21	1	Bars;Nightlife;Pubs
XVDR44P_74FmA0ANanm4CQ	House of Pizza	Plaza Midwood	3640 Central Ave	Charlotte	NC	28205	35.22	-80.78	3.5	75	0	Greek;Restaurants;Pizza;Italian
Ch7Kx4JPJePFvjpXw0PAVQ	AliKat Photography			Gilbert	AZ	85234	33.37	-111.75	5	12	1	Photographers;Event Photography;Session Photography;Event Planning & Services
CV05rBOr5DdDGvxUZkRFmg	Angeline's	Uptown	303 S Church St	Charlotte	NC	28202	35.23	-80.85	3.5	17	1	Restaurants;Nightlife;Pizza;Cocktail Bars;Bars;Italian
wHP1G6mEJJz5nDdA17R78w	Best Cleaners	Spring Valley	7080 S Jones Blvd, Ste 103	Las Vegas	NV	89118	36.06	-115.22	3.5	18	1	Local Services;Sewing & Alterations;Laundry Services;Dry Cleaning & Laundry
m1Arqxfo66oyOqPrLTSYzw	Scorpion Specialists			Gilbert	AZ	85297	33.33	-111.79	5	7	1	Local Services;Pest Control
RtcVbq18T0vNODpGwHzcVQ	Standard Restaurant Supply		5675 S Valley View	Las Vegas	NV	89118	36.09	-115.19	3.5	20	1	Kitchen & Bath;Shopping;Home & Garden;Restaurant Supplies;Professional Services;Wholesalers
RWuk_fBzdWc__FBEsPozZw	Walsh Heating and Cooling		1650 E 361st St	Eastlake	OH	44095	41.64	-81.43	5	3	1	Metal Fabricators;Heating & Air Conditioning/HVAC;Local Services;Home Services;Appliances & Repair
EsE8KTPqAJ2MjJdmuAifRw	Dante's Inferno Flats	East Bank	1059 Old River Rd	Cleveland	OH	44113	41.5	-81.71	3.5	21	1	Italian;Restaurants;Pizza
PmLFk1s8pPVNXChqETM4MA	Coco Lezzone	The Annex	137 Avenue Road	Toronto	ON	M5R 2H4	43.67	-79.4	5	17	0	Italian;Restaurants;Event Planning & Services;Caterers
tqEQd2LD0DeAqkE9tbZ7zA	#1 Cochran Hyundai - Monroeville		4520 William Penn Hwy	Monroeville	PA	15146	40.44	-79.75	3.5	25	1	Automotive;Car Dealers
CppOcUSapx5kU2lQNt2w5w	Freemans	Marchmont	2-6 Spottiswoode Road	Edinburgh	EDH	EH9 1DY	55.94	-3.19	5	20	0	Coffee & Tea;Food
vVz2o24e17PuQtHJOkHPfA	Brown Bag Deli	Downtown	817 Forbes Ave	Pittsburgh	PA	15219	40.44	-79.99	3.5	3	0	Cafes;Food;Food Delivery Services;Sandwiches;Restaurants
Oys6S-x8nYdTJqvY7ksGCA	La Cage Aux Sports	Ville-Marie	1437 Boul Rene-Levesque Ouest	Montréal	QC	H3G 1T7	45.49	-73.57	3.5	18	0	Restaurants
GaSR7qrkR5x0ubKe0av0rQ	Mr. Gao	Ville-Marie	1550 boulevard de Maisonneuve Ouest	Montréal	QC	H3G 1N2	45.5	-73.58	5	10	1	Restaurants;Chinese
YiaOpyu4qx0x1nJC_G33TQ	Grimaldi's Pizzeria		7131 West Ray Rd, Ste 23	Chandler	AZ	85226	33.32	-111.97	4	187	1	Pizza;Restaurants
owuI8y4A3iiYQlAp-fOmWQ	The Pilates Bodies		8961 E Bell Rd, Ste 202	Scottsdale	AZ	85260	33.64	-111.89	5	3	1	Active Life;Pilates;Fitness & Instruction
mRDyt98UXamjbSOX9NinlA	Juniper Branch Library		1825 West Union Hills Dr	Phoenix	AZ	85027	33.65	-112.1	4	16	1	Libraries;Public Services & Government
ueN-Y7p_fiRDSXeD9be14A	Lotus Bar & Grill		9030 E Via Linda	Scottsdale	AZ	85258	33.57	-111.89	4	18	0	Restaurants;Asian Fusion;Sports Bars;Bars;Nightlife
gazJFJoMqPP_aG76kAWcYw	Tortas La Presa #2		4425 W Glendale Ave	Glendale	AZ	85301	33.54	-112.15	4	8	1	Mexican;Restaurants
gBEWJ4b2OvUmN4Oh7ju3hw	Iron Chef		10810 N Tatum Blvd, Ste 106	Phoenix	AZ	85028	33.59	-111.98	4	331	1	Restaurants;Chinese;Japanese;Sushi Bars
NizoFauSY9EgFKXdz5WoNg	Super Cool Heating & Cooling		1014 E Southern Ave	Phoenix	AZ	85040	33.39	-112.06	5	3	1	Heating & Air Conditioning/HVAC;Home Services
QcTTRBfrd0rMzzuCDec_Cw	Jacquee's Espresso		40 N Central Ave, Ste 106	Phoenix	AZ	85004	33.45	-112.07	4	20	1	Delis;Coffee & Tea;Restaurants;Food
xTW5PkLEdMBs2f2W8RGy0g	Miele's Italian and Banquet Hall		2050 W Guadalupe Rd, Ste 9	Mesa	AZ	85202	33.36	-111.88	4	87	1	Desserts;Italian;Pizza;Event Planning & Services;Buffets;Sandwiches;Food;Venues & Event Spaces;Restaurants
sU26m6RAkTtaNUjiJUFqRw	Detroit Coney Cruiser			Scottsdale	AZ		33.49	-111.93	5	6	1	Food;Food Trucks
1MxyFhzNpeIvTQHjtp-bSg	Diva Nails		6611 W Peoria Ave, Ste 2	Glendale	AZ	85302	33.58	-112.2	4	43	1	Nail Salons;Beauty & Spas
yWmGplCGCnQBy9LJFaGa6A	Timesavers		7745 E Redfield Rd, Ste 500	Scottsdale	AZ	85260	33.61	-111.91	4	4	1	Local Services;Furniture Repair;Watch Repair
2CQc-0KPuF2S8axUdGH24w	Punto fisso		Christophstr. 14	Stuttgart	BW	70178	48.77	9.18	5	5	0	Financial Services;Wine Bars;Restaurants;Italian;Pizza;Financial Advising;Caterers;Nightlife;Food;Wedding Planning;Event Planning & Services;Bars
ZStsZ_B3RNY6mLNFfpYQfA	Würschtle Bude		Poststr. 13	Böblingen	BW	71032	48.68	9.01	4	3	1	German;Restaurants;Food Stands;Curry Sausage;Schnitzel
HJ5GABl8RsLYjiWC9Zf7PQ	Matthews Alive Festival		Trade St	Matthews	NC	28105	35.12	-80.72	4	5	1	Arts & Entertainment;Festivals
cTudgI-2jn-GlnZUmULy5Q	Bruegger's Bagels		1905 Matthews Township Pkwy	Matthews	NC	28105	35.12	-80.71	4	27	1	Restaurants;Sandwiches;Breakfast & Brunch;Bagels;Food
xl8jk0FbszttHyI_vjozkA	Ton V Lee, DDS	Southeast	2425 E Hacienda Ave, Ste 120, Summerlin Smiles	Las Vegas	NV	89120	36.09	-115.12	5	4	1	Health & Medical;Dentists;Cosmetic Dentists;General Dentistry
nUR_AQd_6Dhpx3sb2T6meg	Aces Bar & Grill	Southwest	7272 S El Capitan Way, Ste 2	Las Vegas	NV	89148	36.06	-115.29	4	77	1	Nightlife;Food;Specialty Food;Sports Bars;Bars
dJGMbloBEtXTAWSQBqS5pw	My Natural Health Centre		3241 Major MacKenzie Road E	Richmond Hill	ON	L4S 1P4	43.88	-79.38	4	6	1	Health & Medical;Traditional Chinese Medicine
ImIYQbWPsvLVSS0GyVz0og	T1 Rehabilitation & Wellness Center	Willowdale	77 Finch Avenue W, Unit103	Toronto	ON	M2N 2H5	43.78	-79.42	4	17	1	Massage;Medical Spas;Health & Medical;Chiropractors;Beauty & Spas;Physical Therapy;Acupuncture
XbtNbyIGaTitIuEgzEBCzg	Royal Care Medical Centre	Kensington Market	295 College Street	Toronto	ON	M5T 1S2	43.66	-79.4	5	6	1	Health & Medical;Walk-in Clinics;Medical Centers
rwOl_--ElAL1D50G8-BQLg	Signs Restaurant	Downtown Core	558 Yonge Street	Toronto	ON	M4Y 1Z1	43.66	-79.38	4	120	0	Gluten-Free;Food;Canadian (New);Restaurants;Beer;Wine & Spirits;Vegan
Wvst5nUM1Yd64cdjIPOD6w	Alima's Roti and Pastry	Malton	13 Kenview Boulevard, Unit 49	Brampton	ON	L6T 5K9	43.74	-79.65	4	19	1	Food;Caribbean;Specialty Food;Restaurants;Indian
lTxZFiWEd2NNF4Eh7_mlRg	Kassab's	South Side	1207 E Carson St	Pittsburgh	PA	15203	40.43	-79.99	4	101	1	Middle Eastern;Greek;Mediterranean;Lebanese;Restaurants
WCMt5LU2NnkmzjKNhTB7UA	VFW Day Post 7591	Lake Edge	301 Cottage Grove Rd	Madison	WI	53716	43.08	-89.32	5	7	1	American (Traditional);Restaurants;Fish & Chips
R6QCy5sVlySKgqvHb-HhTg	Jacs Dining and Tap House	Dudgeon-Monroe	2611 Monroe St	Madison	WI	53711	43.06	-89.43	4	197	1	American (New);Restaurants;Gluten-Free;Modern European
BXyOtdsnUfGxMYtoM7lIwQ	Arizona Armory			Phoenix	AZ	85009	33.44	-112.13	4.5	6	1	Guns & Ammo;Shopping;Gun/Rifle Ranges;Active Life
eyU4hQOMAG--PUFK-lihDA	Pepperwood Water & Ice Cream		805 W Baseline Rd, Ste 2	Tempe	AZ	85283	33.38	-111.95	5	13	1	Water Stores;Ice Cream & Frozen Yogurt;Shaved Ice;Food
d7y2sEZQGTUQIxKJ4fFS-w	Tahoe Designs			Phoenix	AZ	85003	33.44	-112.06	4.5	6	1	Cabinetry;Home Services;Contractors
vV6oNhupyM8gEhjmhqLPjQ	Anita Purves Nature Center		1505 N Broadway Ave	Urbana	IL	61801	40.13	-88.21	5	5	1	Parks;Active Life
eLRCVsfSUKteoCQi_LVdGg	Savvy Lingerie	Westside	750 S Rampart Blvd, Ste 5	Las Vegas	NV	89145	36.16	-115.29	4.5	11	0	Women's Clothing;Shopping;Swimwear;Lingerie;Fashion
dkLhVfBjMnlQeLl5SGb9KA	Sweets By Maggie		7660 Leavitt Rd	Amherst	OH	44001	41.38	-82.21	5	8	0	Bakeries;Food
l4xrBZAKLXpSR4iprqTw8A	Mark's		1015 Lakeshore Boulevard E, Unit 5	Toronto	ON	M4M 1B3	43.66	-79.33	5	3	1	Women's Clothing;Shopping;Fashion;Men's Clothing
ICdzSGuv70gpSk7aqpIrHw	Wok-In Bbq		3540 Rutherford Road, Unit 67	Vaughan	ON	L4H 3T8	43.83	-79.55	4.5	10	1	Chinese;Barbeque;Restaurants
wk3wGDfJb1V-ciZpyhoNAA	Bic's Pub and Grill		560 State Road 130	Trafford	PA	15085	40.39	-79.73	4.5	7	1	Pubs;American (Traditional);Nightlife;Bars;Pizza;Restaurants
NBYN4Nks_EsPHyAlJ_mdNw	Bistro Merlot		18425 Antoine Faucon	Pierrefonds	QC	H9K 1M7	45.45	-73.89	4.5	8	0	Salad;Pizza;Restaurants;Event Planning & Services;Vietnamese;Caterers
xPy6fq53MdGMxtbvxBD4RA	The Addison		2674 N Park Ln	Fitchburg	WI	53711	43	-89.4	5	5	1	Property Management;Condominiums;Apartments;Home Services;Real Estate
business_id:
string
name:
string
neighborhood:
string
address:
string
city:
string
state:
string
postal_code:
string
latitude:
double
longitude:
double
stars:
double
review_count:
bigint
is_open:
bigint
categories:
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
# Import your libraries
import pyspark
from pyspark.sql.functions import *
from pyspark.sql.window import Window
# Start writing code
# yelp_business.show(truncate=False)
# print(yelp_business.count())
yelp_business1 = yelp_business.where(yelp_business.stars>=5)
# print(yelp_business1.count())
yelp_business1=yelp_business1.select("state","stars").groupBy("state").agg(count("*").alias("n_businesses"))
yelp_business1=yelp_business1.orderBy(desc("n_businesses"),"state")
yelp_business1=yelp_business1.withColumn('rank',rank().over(Window.orderBy(desc("n_businesses"))))
yelp_business1=yelp_business1.where(yelp_business1.rank<=5).select("state","n_businesses")
# yelp_business1.show(truncate=False)
# To validate your solution, convert your final pySpark df to a pandas df
yelp_business1.toPandas()
```

---

## 5. Alternative Approach: PySpark SQL

```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName("StrataScratch_10046").getOrCreate()

# If using raw SQL query on registered temporary tables:
"""
-- Equivalent SQL logic for StrataScratch ID 10046\nSELECT * FROM input_table
"""
```

---

## 6. Key Takeaways & Best Practices

- **Avoid Shuffling When Possible**: Prefer `coalesce()` over `repartition()` when decreasing partition count after filtering large datasets.
- **Null Handling**: Explicitly account for potential `NULL` values in grouping or join keys to prevent dropped rows during inner joins.
- **Testing**: In the StrataScratch platform, solutions are typically verified by converting the final Spark DataFrame to a Pandas DataFrame using `.toPandas()`.
