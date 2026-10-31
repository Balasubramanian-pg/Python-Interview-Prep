# StrataScratch Question ID: 9942 - Largest Olympics

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9942` |
| **Title** | **Largest Olympics** |
| **Difficulty** | `Hard` |
| **Company Tag** | **ESPN** |
| **Category** | `Aggregations & Grouping` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9942) |

---

## 1. Problem Description

Find the Olympics with the highest number of unique athletes. The Olympics game is a combination of the year and the season, and is found in the games column. Output the Olympics along with the corresponding number of athletes. The id column uniquely identifies an athlete.

---

## 2. Input Tables & Schema

```text
Table
olympics_athletes_events
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

games	athletes_count
1924 Summer	118
olympics_athletes_events
Preview
id	name	sex	age	height	weight	team	noc	games	year	season	city	sport	event	medal
3520	Guillermo J. Amparan	M				Mexico	MEX	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 800 metres	
35394	Henry John Finchett	M				Great Britain	GBR	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Rings	
21918	Georg Frederik Ahrensborg Clausen	M	28			Denmark	DEN	1924 Summer	1924	Summer	Paris	Cycling	Cycling Men's Road Race Individual	
110345	Marinus Cornelis Dick Sigmond	M	26			Netherlands	NED	1924 Summer	1924	Summer	Paris	Football	Football Men's Football	
54193	Thodore Tho Jeitz	M	26			Luxembourg	LUX	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Individual All-Around	
23240	Charles Barney Cory	M	47	180		United States	USA	1904 Summer	1904	Summer	St. Louis	Golf	Golf Men's Individual	
85019	Nicolaas Johannes Nederpeld	M	37			Netherlands	NED	1924 Summer	1924	Summer	Paris	Fencing	Fencing Men's Foil Individual	
25934	Jan Johannes de Blcourt	M	47			Netherlands	NED	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Free Pistol 50 yards	
35191	John Charles Field-Richards	M	29			Gyrinus-1	GBR	1908 Summer	1908	Summer	London	Motorboating	Motorboating Mixed B-Class (Under 60 Feet)	Gold
4073	Andreac	M				France	FRA	1900 Summer	1900	Summer	Paris	Fencing	Fencing Men's epee Individual	
120786	Pierre Tolar	M				Luxembourg	LUX	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Rings	
33723	August Oliver Gus Fager (Fagerstrm-)	M	32	178	61	United States	USA	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Cross-Country Team	Silver
82480	Mosso	M				France	FRA	1900 Summer	1900	Summer	Paris	Fencing	Fencing Men's epee Individual	
18257	Gustaf Vilhelm Carlberg	M	44			Sweden	SWE	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Rapid-Fire Pistol 25 metres	Silver
27874	Destin Destine	M				Haiti	HAI	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Free Rifle 400 600 and 800 metres Team	Bronze
5831	Sidney James Montford Sid Atkinson	M	23	186	76	South Africa	RSA	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 110 metres Hurdles	Silver
72917	Jaroslav Mach	M	37			Czechoslovakia	TCH	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Free Rifle 400 600 and 800 metres Team	
97418	Edmund John Pueschel	M	21			United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around Apparatus Work	
49768	Dora Honnywill (Neve-)	F	37			Great Britain	GBR	1908 Summer	1908	Summer	London	Archery	Archery Women's Double National Round	
63311	Jan Koutn	M	26			Czechoslovakia	TCH	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Rope Climbing	
81214	Englebert Mollin	M				Belgium	BEL	1924 Summer	1924	Summer	Paris	Wrestling	Wrestling Men's Lightweight Greco-Roman	
26259	Louis Verrant Gabriel Le Bailly de la Falaise	M	42			France	FRA	1908 Summer	1908	Summer	London	Fencing	Fencing Men's Sabre Individual	
100458	Leslie George Rich	M	21			United States	USA	1908 Summer	1908	Summer	London	Swimming	Swimming Men's 100 metres Freestyle	
25585	Henry D. Davids	M				Great Britain	GBR	1908 Summer	1908	Summer	London	Fencing	Fencing Men's epee Individual	
66696	Lucien lie Larg (Barreau-)	M	26			France	FRA	1900 Summer	1900	Summer	Paris	Fencing	Fencing Men's Foil Masters Individual	
47952	Helmer Hermansen	M	29			Norway	NOR	1900 Summer	1900	Summer	Paris	Shooting	Shooting Men's Free Rifle Kneeling 300 metres	
129248	Karl Magnus Wegelius	M	23			Finland	FIN	1908 Summer	1908	Summer	London	Gymnastics	Gymnastics Men's Team All-Around	Bronze
25610	Charles C. Davies	M				Great Britain	GBR	1908 Summer	1908	Summer	London	Athletics	Athletics Men's 400 metres	
13249	tienne Bonnes	M	29	172	76	France	FRA	1924 Summer	1924	Summer	Paris	Rugby	Rugby Men's Rugby	Silver
2723	Gaston Jules Louis Antoine Alibert	M	22			France	FRA	1900 Summer	1900	Summer	Paris	Fencing	Fencing Men's epee Individual	
123217	Fridrihs Uksti	M				Latvia	LAT	1924 Summer	1924	Summer	Paris	Cycling	Cycling Men's Team Pursuit 4000 metres	
51315	Richard Hutton	M				Great Britain	GBR	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Trap	
133878	Ricardo Zamora Martnez	M	23			Spain	ESP	1924 Summer	1924	Summer	Paris	Football	Football Men's Football	
6144	Charles Avrillon	M				France	FRA	1908 Summer	1908	Summer	London	Cycling	Cycling Men's Tandem Sprint 2000 metres	
66748	Jos-Mara Larrabeiti Eguidazu	M	23	173	72	Spain	ESP	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 200 metres	
63503	Stanisaw Bolesaw Kowalczewski	M	34			Poland	POL	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Free Rifle 400 600 and 800 metres Team	
115057	Thophilus Gerardus Gerard Steurs	M	22			Belgium	BEL	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Marathon	
99201	John Joseph Joe Ravannack	M	26			Independent Rowing Club-3	USA	1904 Summer	1904	Summer	St. Louis	Rowing	Rowing Men's Double Sculls	Bronze
33350	Fred Rudolph Etchen Sr.	M	39	183		United States	USA	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Trap Team	Gold
44725	John Percival Percy Hagerman	M	22	176		Canada	CAN	1904 Summer	1904	Summer	St. Louis	Athletics	Athletics Men's Triple Jump	
87211	Riccardo Nowak	M	23			Italy	ITA	1908 Summer	1908	Summer	London	Fencing	Fencing Men's epee Team	
48256	Max Hess	M	26	165	71	United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around	
115954	Albert Stdemann	M				Germany	GER	1908 Summer	1908	Summer	London	Hockey	Hockey Men's Hockey	
98018	Frank K. Raad	M				United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around Apparatus Work	
22877	Emma C. Cooke	F	55			United States	USA	1904 Summer	1904	Summer	St. Louis	Archery	Archery Women's Double Columbia Round	Silver
3493	Edward John Amoore	M	31			Great Britain	GBR	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Small-Bore Rifle Moving Target 25 yards	
130434	Louis Eugne Edmond Wilhelme	M	23			France	FRA	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Triple Jump	
128354	Gottlob Friedrich Walz	M	26			Germany	GER	1908 Summer	1908	Summer	London	Diving	Diving Men's Springboard	Bronze
3325	Santiago Amat Cansino	M	36			Amolgavar	ESP	1924 Summer	1924	Summer	Paris	Sailing	Sailing Mixed 6 metres	
85547	Sybil Fenton Newall	F	53			Great Britain	GBR	1908 Summer	1908	Summer	London	Archery	Archery Women's Double National Round	Gold
106413	Ole Andreas Sther	M	38			Norway	NOR	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Free Rifle Three Positions 300 metres Team	Gold
126142	Sotirios Versis	M				Greece	GRE	1900 Summer	1900	Summer	Paris	Athletics	Athletics Men's Shot Put	
121884	Tryfon Triantafyllakos	M				Greece	GRE	1924 Summer	1924	Summer	Paris	Fencing	Fencing Men's Sabre Team	
85860	George Nicol	M	21			Great Britain	GBR	1908 Summer	1908	Summer	London	Athletics	Athletics Men's 400 metres	
68934	Mario Lertora	M	26	165		Italy	ITA	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Horse Vault	
55651	E. J. Jones	M				Cornwall	GBR	1908 Summer	1908	Summer	London	Rugby	Rugby Men's Rugby	Silver
122748	Bertrand Turnbull	M	21			Wales-4	GBR	1908 Summer	1908	Summer	London	Hockey	Hockey Men's Hockey	Bronze
13725	Gerard Dagobert Henri Bosch van Drakestein	M	20			Netherlands	NED	1908 Summer	1908	Summer	London	Cycling	Cycling Men's 100 kilometres	
120119	Benjamin Leonard Ben Thrash	M	26	175		United States	USA	1924 Summer	1924	Summer	Paris	Diving	Diving Men's Plain High	
130983	Jerry Elmer Winholtz	M	29			United States	USA	1904 Summer	1904	Summer	St. Louis	Wrestling	Wrestling Men's Lightweight Freestyle	
53528	Benjamin Jamieson	M	30		75	Winnipeg Shamrocks-1	CAN	1904 Summer	1904	Summer	St. Louis	Lacrosse	Lacrosse Men's Lacrosse	Gold
129432	Ottokar Weise	M				Aschenbrodel	GER	1900 Summer	1900	Summer	Paris	Sailing	Sailing Mixed Open	Silver
126443	Maria Rie Vierdag (-Smit)	F	18	170		Netherlands	NED	1924 Summer	1924	Summer	Paris	Swimming	Swimming Women's 400 metres Freestyle	
66966	August Lass	M	20	177	71	Estonia	EST	1924 Summer	1924	Summer	Paris	Football	Football Men's Football	
125020	Albertson Van Zo Post	M	37	183		United States	USA	1904 Summer	1904	Summer	St. Louis	Fencing	Fencing Men's Foil Team	Gold
129495	John Weldon	M	33			Ireland	IRL	1924 Summer	1924	Summer	Paris	Art Competitions	Art Competitions Mixed Literature	
48394	Henry Hiatt	M				Great Britain	GBR	1900 Summer	1900	Summer	Paris	Gymnastics	Gymnastics Men's Individual All-Around	
115209	Stuart Grosvenor Stu Stickney	M	27			United States	USA	1904 Summer	1904	Summer	St. Louis	Golf	Golf Men's Individual	
2829	Richard Louis Pierre Allemane	M	18			USFSA	FRA	1900 Summer	1900	Summer	Paris	Football	Football Men's Football	Silver
10514	Gustaf Eugen Bergman	M	26			Sweden	SWE	1924 Summer	1924	Summer	Paris	Boxing	Boxing Men's Featherweight	
29107	Hugh Lawrence Laurie Doherty	M	24	178		Great Britain	GBR	1900 Summer	1900	Summer	Paris	Tennis	Tennis Men's Singles	Gold
49580	Martin Drummond Vesey Holt	M	43			Great Britain	GBR	1924 Summer	1924	Summer	Paris	Fencing	Fencing Men's epee Team	
127393	Herbert von Petersdorff	M	19			Germany	GER	1900 Summer	1900	Summer	Paris	Water Polo	Water Polo Men's Water Polo	
124979	Eduardus Ludovicus van Voorst tot Voorst	M	33			Netherlands	NED	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Trap Team	
76076	Claude-Lon Mascaux	M	41			France	FRA	1924 Summer	1924	Summer	Paris	Art Competitions	Art Competitions Mixed Sculpturing	Bronze
56960	Nikolaos Kaloudis	M				Greece	GRE	1924 Summer	1924	Summer	Paris	Water Polo	Water Polo Men's Water Polo	
27905	Christian Jacob Deubler	M	23			Germany	GER	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around	
119446	Louis Ren Texier	M	41			France	FRA	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Trap Team	
75884	Antnio Augusto da Silva Martins	M	32			Portugal	POR	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Discus Throw	
33484	Richmond Cavill Dick Eve	M	23	168		Australia	AUS	1924 Summer	1924	Summer	Paris	Diving	Diving Men's Springboard	
125020	Albertson Van Zo Post	M	37	183		United States	USA	1904 Summer	1904	Summer	St. Louis	Fencing	Fencing Men's Foil Individual	Silver
49855	Thomas Hopkins	M				Great Britain	GBR	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Side Horse	
129575	Jean Welter Sr.	M	23			Luxembourg	LUX	1924 Summer	1924	Summer	Paris	Boxing	Boxing Men's Light-Heavyweight	
50023	Marcel Horsch	M			74	Belgium	BEL	1924 Summer	1924	Summer	Paris	Weightlifting	Weightlifting Men's Middleweight	
7426	George A. Bamber	M				Great Britain	GBR	1924 Summer	1924	Summer	Paris	Art Competitions	Art Competitions Mixed Painting	
77749	Burt Plumb McKinnie	M	25			Trans-Mississippi Golf Association-2	USA	1904 Summer	1904	Summer	St. Louis	Golf	Golf Men's Team	Silver
68934	Mario Lertora	M	26	165		Italy	ITA	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Pommelled Horse	
13447	Claes Arne Borg	M	22			Sweden	SWE	1924 Summer	1924	Summer	Paris	Swimming	Swimming Men's 1500 metres Freestyle	Silver
42295	William Evans Graham	M	22			Ireland-2	GBR	1908 Summer	1908	Summer	London	Hockey	Hockey Men's Hockey	Silver
74446	Jean-Baptiste Manhs	M	27	183	79	France	FRA	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Marathon	
46989	Lacey Earnest Hearn	M	23			United States	USA	1904 Summer	1904	Summer	St. Louis	Athletics	Athletics Men's 1500 metres	Bronze
17070	Bror Erik Bylhn	M	26	172	61	Sweden	SWE	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 400 metres	
55942	Jhannes Jsefsson (- Borg)	M	24	174		Iceland	ISL	1908 Summer	1908	Summer	London	Wrestling	Wrestling Men's Middleweight Greco-Roman	
3365	Ernesto Ambrosini	M	29			Italy	ITA	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 3000 metres Steeplechase	
113507	Koloman Sovi	M	24			Yugoslavia	YUG	1924 Summer	1924	Summer	Paris	Cycling	Cycling Men's Road Race Individual	
116147	Josef Sucharda	M	41			Czechoslovakia	TCH	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Running Target Double Shot	
42822	John William Grieb	M	24	175		United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around	
70715	Martti Johannes Liuttula	M	30			Finland	FIN	1924 Summer	1924	Summer	Paris	Shooting	Shooting Men's Running Target Single Shot	
77408	Edward D'Arcy McCrea	M	28			Ireland	IRL	1924 Summer	1924	Summer	Paris	Tennis	Tennis Men's Singles	
123302	Charles Umbs	M	28			United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around Field Sports	
11132	Emil Beyer	M	27			United States	USA	1904 Summer	1904	Summer	St. Louis	Gymnastics	Gymnastics Men's Individual All-Around Field Sports	
10530	Sidney Bergmann	M				Austria	AUT	1924 Summer	1924	Summer	Paris	Wrestling	Wrestling Men's Lightweight Greco-Roman	
119590	Alexandros Theofilakis	M				Greece	GRE	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Free Pistol 50 yards	
14719	Rene Brasseur	F	21			Luxembourg	LUX	1924 Summer	1924	Summer	Paris	Swimming	Swimming Women's 100 metres Backstroke	
115606	Andrew John Andy Straden	M	26			United States	USA	1924 Summer	1924	Summer	Paris	Football	Football Men's Football	
30187	Andr du Bosch	M				Belgium	BEL	1908 Summer	1908	Summer	London	Fencing	Fencing Men's Sabre Team	
47254	John C. Hein	M	18			United States	USA	1904 Summer	1904	Summer	St. Louis	Wrestling	Wrestling Men's Light-Flyweight Freestyle	Silver
3818	Gerald C. Anderson	M				Great Britain	GBR	1908 Summer	1908	Summer	London	Cycling	Cycling Men's Sprint	
38835	Otto Garnus	M				Switzerland	SUI	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's Shot Put	
87390	Paavo Johannes Nurmi	M	26	174	65	Finland	FIN	1924 Summer	1924	Summer	Paris	Athletics	Athletics Men's 1500 metres	Gold
130936	Walter Winans	M	56			United States	USA	1908 Summer	1908	Summer	London	Shooting	Shooting Men's Small-Bore Rifle Disappearing Target 25 yards	
37932	Paul Gailly	M	29			Belgium	BEL	1924 Summer	1924	Summer	Paris	Water Polo	Water Polo Men's Water Polo	Silver
88943	Oscar G. Olson	M				United States	USA	1904 Summer	1904	Summer	St. Louis	Weightlifting	Weightlifting Men's Unlimited Two Hands	
41722	Harold Goodworth	M				Great Britain	GBR	1908 Summer	1908	Summer	London	Diving	Diving Men's Platform	
120786	Pierre Tolar	M				Luxembourg	LUX	1924 Summer	1924	Summer	Paris	Gymnastics	Gymnastics Men's Side Horse	
92116	John Neil Patterson	M	22			United States	USA	1908 Summer	1908	Summer	London	Athletics	Athletics Men's High Jump	
55169	Oskar Emil Johansson	M	23			Sweden	SWE	1908 Summer	1908	Summer	London	Tug-Of-War	Tug-Of-War Men's Tug-Of-War	
112278	Herbert Smith	M	30			Great Britain	GBR	1908 Summer	1908	Summer	London	Football	Football Men's Football	Gold
129828	Edvard Vilhelm Westerlund	M	23	174	77.5	Finland	FIN	1924 Summer	1924	Summer	Paris	Wrestling	Wrestling Men's Middleweight Greco-Roman	Gold
92249	Georges Marie Nestor Pauwels	M	20			Belgium-1	BEL	1900 Summer	1900	Summer	Paris	Equestrianism	Equestrianism Mixed Four-In-Hand Competition	
24838	Edward Martin Dahl	M	21			Sweden	SWE	1908 Summer	1908	Summer	London	Athletics	Athletics Men's 800 metres	
30732	A. Duponcheel	M				France	FRA	1908 Summer	1