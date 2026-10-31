# StrataScratch Question ID: 10171 - Find The Genre Of The Person With The Most Number Of Oscar Winnings

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `10171` |
| **Title** | **Find The Genre Of The Person With The Most Number Of Oscar Winnings** |
| **Difficulty** | `Hard` |
| **Company Tag** | **Netflix** |
| **Category** | `Joins & Relational Data` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/10171) |

---

## 1. Problem Description

Find the genre of the person with the most number of oscar winnings.
If there are more than one person with the same number of oscar wins, return the first one in alphabetic order based on their name. Use the names as keys when joining the

---

## 2. Input Tables & Schema

```text
tables.

Tables
oscar_nominees
nominee_information
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

top_genre
Drama
oscar_nominees
Preview
year	category	nominee	movie	winner	id
2006	actress in a supporting role	Abigail Breslin	Little Miss Sunshine	FALSE	1
1984	actor in a supporting role	Adolph Caesar	A Soldier's Story	FALSE	2
2006	actress in a supporting role	Adriana Barraza	Babel	FALSE	3
2002	actor in a leading role	Adrien Brody	The Pianist	TRUE	4
1942	actress in a supporting role	Agnes Moorehead	The Magnificent Ambersons	FALSE	5
1944	actress in a supporting role	Agnes Moorehead	Mrs. Parkington	FALSE	6
1948	actress in a supporting role	Agnes Moorehead	Johnny Belinda	FALSE	7
1964	actress in a supporting role	Agnes Moorehead	Hush...Hush, Sweet Charlotte	FALSE	8
1936	actor in a supporting role	Akim Tamiroff	The General Died at Dawn	FALSE	9
1943	actor in a supporting role	Akim Tamiroff	For Whom the Bell Tolls	FALSE	10
1972	actor in a supporting role	Al Pacino	The Godfather	FALSE	11
1973	actor	Al Pacino	Serpico	FALSE	12
1974	actor	Al Pacino	The Godfather Part II	FALSE	13
1975	actor	Al Pacino	Dog Day Afternoon	FALSE	14
1979	actor in a leading role	Al Pacino	...And Justice for All	FALSE	15
1990	actor in a supporting role	Al Pacino	Dick Tracy	FALSE	16
1992	actor in a leading role	Al Pacino	Scent of a Woman	TRUE	17
1992	actor in a supporting role	Al Pacino	Glengarry Glen Ross	FALSE	18
2004	actor in a supporting role	Alan Alda	The Aviator	FALSE	19
1966	actor	Alan Arkin	The Russians Are Coming The Russians Are Coming	FALSE	20
1968	actor	Alan Arkin	The Heart Is a Lonely Hunter	FALSE	21
2006	actor in a supporting role	Alan Arkin	Little Miss Sunshine	TRUE	22
2012	actor in a supporting role	Alan Arkin	Argo	FALSE	23
1968	actor	Alan Bates	The Fixer	FALSE	24
1940	actor in a supporting role	Albert Basserman	Foreign Correspondent	FALSE	25
1987	actor in a supporting role	Albert Brooks	Broadcast News	FALSE	26
1963	actor	Albert Finney	Tom Jones	FALSE	27
1974	actor	Albert Finney	Murder on the Orient Express	FALSE	28
1983	actor in a leading role	Albert Finney	The Dresser	FALSE	29
1984	actor in a leading role	Albert Finney	Under the Volcano	FALSE	30
2000	actor in a supporting role	Albert Finney	Erin Brockovich	FALSE	31
2003	actor in a supporting role	Alec Baldwin	The Cooler	FALSE	32
1952	actor	Alec Guinness	The Lavender Hill Mob	FALSE	33
1957	actor	Alec Guinness	The Bridge on the River Kwai	TRUE	34
1977	actor in a supporting role	Alec Guinness	Star Wars	FALSE	35
1988	actor in a supporting role	Alec Guinness	Little Dorrit	FALSE	36
1944	actor	Alexander Knox	Wilson	FALSE	37
1983	actress in a supporting role	Alfre Woodard	Cross Creek	FALSE	38
1970	actress	Ali MacGraw	Love Story	FALSE	39
1936	actress in a supporting role	Alice Brady	My Man Godfrey	FALSE	40
1937	actress in a supporting role	Alice Brady	In Old Chicago	TRUE	41
1944	actress in a supporting role	Aline MacMahon	Dragon Seed	FALSE	42
2005	actress in a supporting role	Amy Adams	Junebug	FALSE	43
2008	actress in a supporting role	Amy Adams	Doubt	FALSE	44
2010	actress in a supporting role	Amy Adams	The Fighter	FALSE	45
2012	actress in a supporting role	Amy Adams	The Master	FALSE	46
1983	actress in a supporting role	Amy Irving	Yentl	FALSE	47
1985	actress in a supporting role	Amy Madigan	Twice in a Lifetime	FALSE	48
2007	actress in a supporting role	Amy Ryan	Gone Baby Gone	FALSE	49
1937	actress in a supporting role	Andrea Leeds	Stage Door	FALSE	50
1990	actor in a supporting role	Andy Garcia	The Godfather, Part III	FALSE	51
1993	actress in a leading role	Angela Bassett	What's Love Got to Do with It	FALSE	52
1944	actress in a supporting role	Angela Lansbury	Gaslight	FALSE	53
1945	actress in a supporting role	Angela Lansbury	The Picture of Dorian Gray	FALSE	54
1962	actress in a supporting role	Angela Lansbury	The Manchurian Candidate	FALSE	55
1999	actress in a supporting role	Angelina Jolie	Girl, Interrupted	TRUE	56
2008	actress in a leading role	Angelina Jolie	Changeling	FALSE	57
1985	actress in a supporting role	Anjelica Huston	Prizzi's Honor	TRUE	58
1989	actress in a supporting role	Anjelica Huston	Enemies, A Love Story	FALSE	59
1990	actress in a leading role	Anjelica Huston	The Grifters	FALSE	60
1945	actress in a supporting role	Ann Blyth	Mildred Pierce	FALSE	61
1987	actress in a supporting role	Ann Sothern	The Whales of August	FALSE	62
1971	actress in a supporting role	Ann-Margret	Carnal Knowledge	FALSE	63
1975	actress	Ann-Margret	Tommy	FALSE	64
2009	actress in a supporting role	Anna Kendrick	Up in the Air	FALSE	65
1955	actress	Anna Magnani	The Rose Tattoo	TRUE	66
1957	actress	Anna Magnani	Wild Is the Wind	FALSE	67
1993	actress in a supporting role	Anna Paquin	The Piano	TRUE	68
1987	actress in a supporting role	Anne Archer	Fatal Attraction	FALSE	69
1962	actress	Anne Bancroft	The Miracle Worker	TRUE	70
1964	actress	Anne Bancroft	The Pumpkin Eater	FALSE	71
1967	actress	Anne Bancroft	The Graduate	FALSE	72
1977	actress in a leading role	Anne Bancroft	The Turning Point	FALSE	73
1985	actress in a leading role	Anne Bancroft	Agnes of God	FALSE	74
1946	actress in a supporting role	Anne Baxter	The Razor's Edge	TRUE	75
1950	actress	Anne Baxter	All about Eve	FALSE	76
2008	actress in a leading role	Anne Hathaway	Rachel Getting Married	FALSE	77
2012	actress in a supporting role	Anne Hathaway	Les Mis_rables	TRUE	78
1987	actress in a supporting role	Anne Ramsey	Throw Momma from the Train	FALSE	79
1943	actress in a supporting role	Anne Revere	The Song of Bernadette	FALSE	80
1945	actress in a supporting role	Anne Revere	National Velvet	TRUE	81
1947	actress in a supporting role	Anne Revere	Gentleman's Agreement	FALSE	82
1937	actress in a supporting role	Anne Shirley	Stella Dallas	FALSE	83
1990	actress in a supporting role	Annette Bening	The Grifters	FALSE	84
1999	actress in a leading role	Annette Bening	American Beauty	FALSE	85
2004	actress in a leading role	Annette Bening	Being Julia	FALSE	86
2010	actress in a leading role	Annette Bening	The Kids Are All Right	FALSE	87
1966	actress	Anouk Aimee	A Man and a Woman	FALSE	88
1957	actor	Anthony Franciosa	A Hatful of Rain	FALSE	89
1991	actor in a leading role	Anthony Hopkins	The Silence of the Lambs	TRUE	90
1993	actor in a leading role	Anthony Hopkins	The Remains of the Day	FALSE	91
1995	actor in a leading role	Anthony Hopkins	Nixon	FALSE	92
1997	actor in a supporting role	Anthony Hopkins	Amistad	FALSE	93
1956	actor in a supporting role	Anthony Perkins	Friendly Persuasion	FALSE	94
1969	actor in a supporting role	Anthony Quayle	Anne of the Thousand Days	FALSE	95
1952	actor in a supporting role	Anthony Quinn	Viva Zapata!	TRUE	96
1956	actor in a supporting role	Anthony Quinn	Lust for Life	TRUE	97
1957	actor	Anthony Quinn	Wild Is the Wind	FALSE	98
1964	actor	Anthony Quinn	Zorba the Greek	FALSE	99
1996	actor in a supporting role	Armin Mueller-Stahl	Shine	FALSE	100
1974	actor	Art Carney	Harry and Tonto	TRUE	101
1952	actor in a supporting role	Arthur Hunnicutt	The Big Sky	FALSE	102
1949	actor in a supporting role	Arthur Kennedy	Champion	FALSE	103
1951	actor	Arthur Kennedy	Bright Victory	FALSE	104
1955	actor in a supporting role	Arthur Kennedy	Trial	FALSE	105
1957	actor in a supporting role	Arthur Kennedy	Peyton Place	FALSE	106
1958	actor in a supporting role	Arthur Kennedy	Some Came Running	FALSE	107
1955	actor in a supporting role	Arthur O'Connell	Picnic	FALSE	108
1959	actor in a supporting role	Arthur O'Connell	Anatomy of a Murder	FALSE	109
1953	actress	Audrey Hepburn	Roman Holiday	TRUE	110
1954	actress	Audrey Hepburn	Sabrina	FALSE	111
1959	actress	Audrey Hepburn	The Nun's Story	FALSE	112
1961	actress	Audrey Hepburn	Breakfast at Tiffany's	FALSE	113
1967	actress	Audrey Hepburn	Wait until Dark	FALSE	114
1953	actress	Ava Gardner	Mogambo	FALSE	115
1979	actress in a supporting role	Barbara Barrie	Breaking Away	FALSE	116
1948	actress in a supporting role	Barbara Bel Geddes	I Remember Mama	FALSE	117
1971	actress in a supporting role	Barbara Harris	Who Is Harry Kellerman and Why Is He Saying Those Terrible Things about Me?	FALSE	118
1996	actress in a supporting role	Barbara Hershey	The Portrait of a Lady	FALSE	119
1940	actress in a supporting role	Barbara O'Neil	All This, and Heaven Too	FALSE	120
1937	actress	Barbara Stanwyck	Stella Dallas	FALSE	121
1941	actress	Barbara Stanwyck	Ball of Fire	FALSE	122
1944	actress	Barbara Stanwyck	Double Indemnity	FALSE	123
1948	actress	Barbara Stanwyck	Sorry, Wrong Number	FALSE	124
1968	actress	Barbra Streisand	Funny Girl	TRUE	125
1973	actress	Barbra Streisand	The Way We Were	FALSE	126
1944	actor	Barry Fitzgerald	Going My Way	FALSE	127
1944	actor in a supporting role	Barry Fitzgerald	Going My Way	TRUE	128
1936	actor in a supporting role	Basil Rathbone	Romeo and Juliet	FALSE	129
1938	actor in a supporting role	Basil Rathbone	If I Were King	FALSE	130
1967	actress in a supporting role	Beah Richards	Guess Who's Coming to Dinner	FALSE	131
1976	actress in a supporting role	Beatrice Straight	Network	TRUE	132
1971	actor in a supporting role	Ben Johnson	The Last Picture Show	TRUE	133
1982	actor in a leading role	Ben Kingsley	Gandhi	TRUE	134
1991	actor in a supporting role	Ben Kingsley	Bugsy	FALSE	135
2001	actor in a supporting role	Ben Kingsley	Sexy Beast	FALSE	136
2003	actor in a leading role	Ben Kingsley	House of Sand and Fog	FALSE	137
2000	actor in a supporting role	Benicio Del Toro	Traffic	TRUE	138
2003	actor in a supporting role	Benicio Del Toro	21 Grams	FALSE	139
2011	actress in a supporting role	B_r_nice Bejo	The Artist	FALSE	140
1955	actress in a supporting role	Betsy Blair	Marty	FALSE	141
1938	actress	Bette Davis	Jezebel	TRUE	142
1939	actress	Bette Davis	Dark Victory	FALSE	143
1940	actress	Bette Davis	The Letter	FALSE	144
1941	actress	Bette Davis	The Little Foxes	FALSE	145
1942	actress	Bette Davis	Now, Voyager	FALSE	146
1944	actress	Bette Davis	Mr. Skeffington	FALSE	147
1950	actress	Bette Davis	All about Eve	FALSE	148
1952	actress	Bette Davis	The Star	FALSE	149
1962	actress	Bette Davis	What Ever Happened to Baby Jane?	FALSE	150
1979	actress in a leading role	Bette Midler	The Rose	FALSE	151
1991	actress in a leading role	Bette Midler	For the Boys	FALSE	152
1936	actress in a supporting role	Beulah Bondi	The Gorgeous Hussy	FALSE	153
1938	actress in a supporting role	Beulah Bondi	Of Human Hearts	FALSE	154
2003	actor in a leading role	Bill Murray	Lost in Translation	FALSE	155
1938	actress in a supporting role	Billie Burke	Merrily We Live	FALSE	156
1996	actor in a leading role	Billy Bob Thornton	Sling Blade	FALSE	157
1998	actor in a supporting role	Billy Bob Thornton	A Simple Plan	FALSE	158
1944	actor	Bing Crosby	Going My Way	TRUE	159
1945	actor	Bing Crosby	The Bells of St. Mary's	FALSE	160
1954	actor	Bing Crosby	The Country Girl	FALSE	161
1986	actor in a leading role	Bob Hoskins	Mona Lisa	FALSE	162
1963	actor in a supporting role	Bobby Darin	Captain Newman, M.D.	FALSE	163
1936	actress in a supporting role	Bonita Granville	These Three	FALSE	164
1975	actor in a supporting role	Brad Dourif	One Flew over the Cuckoo's Nest	FALSE	165
1995	actor in a supporting role	Brad Pitt	12 Monkeys	FALSE	166
2008	actor in a leading role	Brad Pitt	The Curious Case of Benjamin Button	FALSE	167
2011	actor in a leading role	Brad Pitt	Moneyball	FALSE	168
2012	actor in a leading role	Bradley Cooper	Silver Linings Playbook	FALSE	169
1953	actor in a supporting role	Brandon De Wilde	Shane	FALSE	170
1996	actress in a leading role	Brenda Blethyn	Secrets & Lies	FALSE	171
1998	actress in a supporting role	Brenda Blethyn	Little Voice	FALSE	172
1989	actress in a supporting role	Brenda Fricker	My Left Foot	TRUE	173
1975	actress in a supporting role	Brenda Vaccaro	Jacqueline Susann's Once Is Not Enough	FALSE	174
1939	actor in a supporting role	Brian Aherne	Juarez	FALSE	175
1939	actor in a supporting role	Brian Donlevy	Beau Geste	FALSE	176
1949	actor	Broderick Crawford	All the King's Men	TRUE	177
1990	actor in a supporting role	Bruce Davison	Longtime Companion	FALSE	178
1978	actor in a supporting role	Bruce Dern	Coming Home	FALSE	179
1975	actor in a supporting role	Burgess Meredith	The Day of the Locust	FALSE	180
1976	actor in a supporting role	Burgess Meredith	Rocky	FALSE	181
1958	actor in a supporting role	Burl Ives	The Big Country	TRUE	182
1953	actor	Burt Lancaster	From Here to Eternity	FALSE	183
1960	actor	Burt Lancaster	Elmer Gantry	TRUE	184
1962	actor	Burt Lancaster	Birdman of Alcatraz	FALSE	185
1981	actor in a leading role	Burt Lancaster	Atlantic City	FALSE	186
1997	actor in a supporting role	Burt Reynolds	Boogie Nights	FALSE	187
1976	actor in a supporting role	Burt Young	Rocky	FALSE	188
1979	actress in a supporting role	Candice Bergen	Starting Over	FALSE	189
1973	actress in a supporting role	Candy Clark	American Graffiti	FALSE	190
1958	actress in a supporting role	Cara Williams	The Defiant Ones	FALSE	191
2009	actress in a leading role	Carey Mulligan	An Education	FALSE	192
1967	actress in a supporting role	Carol Channing	Thoroughly Modern Millie	FALSE	193
1975	actress	Carol Kane	Hester Street	FALSE	194
1936	actress	Carole Lombard	My Man Godfrey	FALSE	195
1957	actress in a supporting role	Carolyn Jones	The Bachelor Party	FALSE	196
1970	actress	Carrie Snodgress	Diary of a Mad Housewife	FALSE	197
1956	actress	Carroll Baker	Baby Doll	FALSE	198
1941	actor	Cary Grant	Penny Serenade	FALSE	199
1944	actor	Cary Grant	None but the Lonely Heart	FALSE	200
2007	actor in a supporting role	Casey Affleck	The Assassination of Jesse James by the Coward Robert Ford	FALSE	201
2004	actress in a leading role	Catalina Sandino Moreno	Maria Full of Grace	FALSE	202
1998	actress in a leading role	Cate Blanchett	Elizabeth	FALSE	203
2004	actress in a supporting role	Cate Blanchett	The Aviator	TRUE	204
2006	actress in a supporting role	Cate Blanchett	Notes on a Scandal	FALSE	205
2007	actress in a leading role	Cate Blanchett	Elizabeth: The Golden Age	FALSE	206
2007	actress in a supporting role	Cate Blanchett	I'm Not There	FALSE	207
1969	actress in a supporting role	Catherine Burns	Last Summer	FALSE	208
1992	actress in a leading role	Catherine Deneuve	Indochine	FALSE	209
1999	actress in a supporting role	Catherine Keener	Being John Malkovich	FALSE	210
2005	actress in a supporting role	Catherine Keener	Capote	FALSE	211
2002	actress in a supporting role	Catherine Zeta-Jones	Chicago	TRUE	212
1980	actress in a supporting role	Cathy Moriarty	Raging Bull	FALSE	213
1948	actor in a supporting role	Cecil Kellaway	The Luck of the Irish	FALSE	214
1967	actor in a supporting role	Cecil Kellaway	Guess Who's Coming to Dinner	FALSE	215
1947	actress in a supporting role	Celeste Holm	Gentleman's Agreement	TRUE	216
1949	actress in a supporting role	Celeste Holm	Come to the Stable	FALSE	217
1950	actress in a supporting role	Celeste Holm	All about Eve	FALSE	218
1946	actress	Celia Johnson	Brief Encounter	FALSE	219
1943	actor in a supporting role	Charles Bickford	The Song of Bernadette	FALSE	220
1947	actor in a supporting role	Charles Bickford	The Farmer's Daughter	FALSE	221
1948	actor in a supporting role	Charles Bickford	Johnny Belinda	FALSE	222
1937	actor	Charles Boyer	Conquest	FALSE	223
1938	actor	Charles Boyer	Algiers	FALSE	224
1944	actor	Charles Boyer	Gaslight	FALSE	225
1961	actor	Charles Boyer	Fanny	FALSE	226
1940	actor	Charles Chaplin	The Great Dictator	FALSE	227
1941	actor in a supporting role	Charles Coburn	The Devil and Miss Jones	FALSE	228
1943	actor in a supporting role	Charles Coburn	The More the Merrier	TRUE	229
1946	actor in a supporting role	Charles Coburn	The Green Years	FALSE	230
1982	actor in a supporting role	Charles Durning	The Best Little Whorehouse in Texas	FALSE	231
1983	actor in a supporting role	Charles Durning	To Be or Not to Be	FALSE	232
1957	actor	Charles Laughton	Witness for the Prosecution	FALSE	233
2003	actress in a leading role	Charlize Theron	Monster	TRUE	234
2005	actress in a leading role	Charlize Theron	North Country	FALSE	235
1959	actor	Charlton Heston	Ben-Hur	TRUE	236
1994	actor in a supporting role	Chazz Palminteri	Bullets over Broadway	FALSE	237
1983	actress in a supporting role	Cher	Silkwood	FALSE	238
1987	actress in a leading role	Cher	Moonstruck	TRUE	239
1970	actor in a supporting role	Chief Dan George	Little Big Man	FALSE	240
1960	actor in a supporting role	Chill Wills	The Alamo	FALSE	241
1999	actress in a supporting role	Chlo� Sevigny	Boys Don't Cry	FALSE	242
2002	actor in a supporting role	Chris Cooper	Adaptation	TRUE	243
1975	actor in a supporting role	Chris Sarandon	Dog Day Afternoon	FALSE	244
2010	actor in a supporting role	Christian Bale	The Fighter	TRUE	245
1984	actress in a supporting role	Christine Lahti	Swing Shift	FALSE	246
2009	actor in a supporting role	Christoph Waltz	Inglourious Basterds	TRUE	247
2012	actor in a supporting role	Christoph Waltz	Django Unchained	TRUE	248
2009	actor in a supporting role	Christopher Plummer	The Last Station	FALSE	249
2011	actor in a supporting role	Christopher Plummer	Beginners	TRUE	250
1978	actor in a supporting role	Christopher Walken	The Deer Hunter	TRUE	251
2002	actor in a supporting role	Christopher Walken	Catch Me If You Can	FALSE	252
1972	actress	Cicely Tyson	Sounder	FALSE	253
1937	actress in a supporting role	Claire Trevor	Dead End	FALSE	254
1948	actress in a supporting role	Claire Trevor	Key Largo	TRUE	255
1954	actress in a supporting role	Claire Trevor	The High and the Mighty	FALSE	256
1939	actor	Clark Gable	Gone with the Wind	FALSE	257
1939	actor in a supporting role	Claude Rains	Mr. Smith Goes to Washington	FALSE	258
1943	actor in a supporting role	Claude Rains	Casablanca	FALSE	259
1944	actor in a supporting role	Claude Rains	Mr. Skeffington	FALSE	260
1946	actor in a supporting role	Claude Rains	Notorious	FALSE	261
1944	actress	Claudette Colbert	Since You Went Away	FALSE	262
1968	actor	Cliff Robertson	Charly	TRUE	263
1944	actor in a supporting role	Clifton Webb	Laura	FALSE	264
1946	actor in a supporting role	Clifton Webb	The Razor's Edge	FALSE	265
1948	actor	Clifton Webb	Sitting Pretty	FALSE	266
1992	actor in a leading role	Clint Eastwood	Unforgiven	FALSE	267
2004	actor in a leading role	Clint Eastwood	Million Dollar Baby	FALSE	268
2004	actor in a supporting role	Clive Owen	Closer	FALSE	269
1971	actress in a supporting role	Cloris Leachman	The Last Picture Show	TRUE	270
1952	actress in a supporting role	Colette Marchand	Moulin Rouge	FALSE	271
2009	actor in a leading role	Colin Firth	A Single Man	FALSE	272
2010	actor in a leading role	Colin Firth	The King's Speech	TRUE	273
1945	actor	Cornel Wilde	A Song to Remember	FALSE	274
1996	actor in a supporting role	Cuba Gooding, Jr.	Jerry Maguire	TRUE	275
1963	actress in a supporting role	Dame Edith Evans	Tom Jones	FALSE	276
1964	actress in a supporting role	Dame Edith Evans	The Chalk Garden	FALSE	277
1967	actress	Dame Edith Evans	The Whisperers	FALSE	278
1937	actress in a supporting role	Dame May Whitty	Night Must Fall	FALSE	279
1942	actress in a supporting role	Dame May Whitty	Mrs. Miniver	FALSE	280
1989	actor in a supporting role	Dan Aykroyd	Driving Miss Daisy	FALSE	281
1948	actor	Dan Dailey	When My Baby Smiles at Me	FALSE	282
1954	actor	Dan O'Herlihy	Adventures of Robinson Crusoe	FALSE	283
1989	actor in a leading role	Daniel Day Lewis	My Left Foot	TRUE	284
1993	actor in a leading role	Daniel Day-Lewis	In the Name of the Father	FALSE	285
2002	actor in a leading role	Daniel Day-Lewis	Gangs of New York	FALSE	286
2007	actor in a leading role	Daniel Day-Lewis	There Will Be Blood	TRUE	287
2012	actor in a leading role	Daniel Day-Lewis	Lincoln	TRUE	288
1968	actor in a supporting role	Daniel Massey	Star!	FALSE	289
1989	actor in a supporting role	Danny Aiello	Do the Right Thing	FALSE	290
1958	actor	David Niven	Separate Tables	TRUE	291
1992	actor in a supporting role	David Paymer	Mr. Saturday Night	FALSE	292
2005	actor in a leading role	David Strathairn	Good Night, and Good Luck.	FALSE	293
1949	actor in a supporting role	Dean Jagger	Twelve O'Clock High	TRUE	294
1988	actor in a supporting role	Dean Stockwell	Married to the Mob	FALSE	295
1964	actress	Debbie Reynolds	The Unsinkable Molly Brown	FALSE	296
1949	actress	Deborah Kerr	Edward, My Son	FALSE	297
1953	actress	Deborah Kerr	From Here to Eternity	FALSE	298
1956	actress	Deborah Kerr	The King and I	FALSE	299
1957	actress	Deborah Kerr	Heaven Knows, Mr. Allison	FALSE	300
1958	actress	Deborah Kerr	Separate Tables	FALSE	301
1960	actress	Deborah Kerr	The Sundowners	FALSE	302
1982	actress in a leading role	Debra Winger	An Officer and a Gentleman	FALSE	303
1983	actress in a leading role	Debra Winger	Terms of Endearment	FALSE	304
1993	actress in a leading role	Debra Winger	Shadowlands	FALSE	305
2011	actor in a leading role	Demian Bichir	A Better Life	FALSE	306
1986	actor in a supporting role	Denholm Elliott	A Room with a View	FALSE	307
1986	actor in a supporting role	Dennis Hopper	Hoosiers	FALSE	308
1987	actor in a supporting role	Denzel Washington	Cry Freedom	FALSE	309
1989	actor in a supporting role	Denzel Washington	Glory	TRUE	310
1992	actor in a leading role	Denzel Washington	Malcolm X	FALSE	311
1999	actor in a leading role	Denzel Washington	The Hurricane	FALSE	312
2001	actor in a leading role	Denzel Washington	Training Day	TRUE	313
2012	actor in a leading role	Denzel Washington	Flight	FALSE	314
1986	actor in a leading role	Dexter Gordon	Round Midnight	FALSE	315
1974	actress	Diahann Carroll	Claudine	FALSE	316
1972	actress	Diana Ross	Lady Sings the Blues	FALSE	317
1980	actress in a supporting role	Diana Scarwid	Inside Moves	FALSE	318
1963	actress in a supporting role	Diane Cilento	Tom Jones	FALSE	319
1977	actress in a leading role	Diane Keaton	Annie Hall	TRUE	320
1981	actress in a leading role	Diane Keaton	Reds	FALSE	321
1996	actress in a leading role	Diane Keaton	Marvin's Room	FALSE	322
2003	actress in a leading role	Diane Keaton	Something's Gotta Give	FALSE	323
1974	actress in a supporting role	Diane Ladd	Alice Doesn't Live Here Anymore	FALSE	324
1990	actress in a supporting role	Diane Ladd	Wild at Heart	FALSE	325
1991	actress in a supporting role	Diane Ladd	Rambling Rose	FALSE	326
2002	actress in a leading role	Diane Lane	Unfaithful	FALSE	327
1957	actress in a supporting role	Diane Varsi	Peyton Place	FALSE	328
1986	actress in a supporting role	Dianne Wiest	Hannah and Her Sisters	TRUE	329
1989	actress in a supporting role	Dianne Wiest	Parenthood	FALSE	330
1994	actress in a supporting role	Dianne Wiest	Bullets over Broadway	TRUE	331
2003	actor in a supporting role	Djimon Hounsou	In America	FALSE	332
2006	actor in a supporting role	Djimon Hounsou	Blood Diamond	FALSE	333
1985	actor in a supporting role	Don Ameche	Cocoon	TRUE	334
2004	actor in a leading role	Don Cheadle	Hotel Rwanda	FALSE	335
1956	actor in a supporting role	Don Murray	Bus Stop	FALSE	336
1941	actor in a supporting role	Donald Crisp	How Green Was My Valley	TRUE	337
1953	actress in a supporting role	Donna Reed	From Here to Eternity	TRUE	338
1959	actress	Doris Day	Pillow Talk	FALSE	339
1954	actress	Dorothy Dandridge	Carmen Jones	FALSE	340
1956	actress in a supporting role	Dorothy Malone	Written on the Wind	TRUE	341
1947	actress	Dorothy McGuire	Gentleman's Agreement	FALSE	342
1981	actor in a leading role	Dudley Moore	Arthur	FALSE	343
1967	actor	Dustin Hoffman	The Graduate	FALSE	344
1969	actor	Dustin Hoffman	Midnight Cowboy	FALSE	345
1974	actor	Dustin Hoffman	Lenny	FALSE	346
1979	actor in a leading role	Dustin Hoffman	Kramer vs. Kramer	TRUE	347
1982	actor in a leading role	Dustin Hoffman	Tootsie	FALSE	348
1988	actor in a leading role	Dustin Hoffman	Rain Man	TRUE	349
1997	actor in a leading role	Dustin Hoffman	Wag the Dog	FALSE	350
1969	actress in a supporting role	Dyan Cannon	Bob & Carol & Ted & Alice	FALSE	351
1978	actress in a supporting role	Dyan Cannon	Heaven Can Wait	FALSE	352
1962	actor in a supporting role	Ed Begley	Sweet Bird of Youth	TRUE	353
1995	actor in a supporting role	Ed Harris	Apollo 13	FALSE	354
1998	actor in a supporting role	Ed Harris	The Truman Show	FALSE	355
2000	actor in a leading role	Ed Harris	Pollock	FALSE	356
2002	actor in a supporting role	Ed Harris	The Hours	FALSE	357
1959	actor in a supporting role	Ed Wynn	The Diary of Anne Frank	FALSE	358
1953	actor in a supporting role	Eddie Albert	Roman Holiday	FALSE	359
1972	actor in a supporting role	Eddie Albert	The Heartbreak Kid	FALSE	360
2006	actor in a supporting role	Eddie Murphy	Dreamgirls	FALSE	361
1954	actor in a supporting role	Edmond O'Brien	The Barefoot Contessa	TRUE	362
1964	actor in a supporting role	Edmond O'Brien	Seven Days in May	FALSE	363
1947	actor in a supporting role	Edmund Gwenn	Miracle on 34th Street	TRUE	364
1950	actor in a supporting role	Edmund Gwenn	Mister 880	FALSE	365
1939	actress in a supporting role	Edna May Oliver	Drums along the Mohawk	FALSE	366
1988	actor in a leading role	Edward James Olmos	Stand and Deliver	FALSE	367
1996	actor in a supporting role	Edward Norton	Primal Fear	FALSE	368
1998	actor in a leading role	Edward Norton	American History X	FALSE	369
1980	actress in a supporting role	Eileen Brennan	Private Benjamin	FALSE	370
1956	actress in a supporting role	Eileen Heckart	The Bad Seed	FALSE	371
1972	actress in a supporting role	Eileen Heckart	Butterflies Are Free	TRUE	372
1950	actress	Eleanor Parker	Caged	FALSE	373
1951	actress	Eleanor Parker	Detective Story	FALSE	374
1955	actress	Eleanor Parker	Interrupted Melody	FALSE	375
1995	actress in a leading role	Elisabeth Shue	Leaving Las Vegas	FALSE	376
1965	actress	Elizabeth Hartman	A Patch of Blue	FALSE	377
1981	actress in a supporting role	Elizabeth McGovern	Ragtime	FALSE	378
1957	actress	Elizabeth Taylor	Raintree County	FALSE	379
1958	actress	Elizabeth Taylor	Cat on a Hot Tin Roof	FALSE	380
1959	actress	Elizabeth Taylor	Suddenly, Last Summer	FALSE	381
1960	actress	Elizabeth Taylor	Butterfield 8	TRUE	382
1966	actress	Elizabeth Taylor	Who's Afraid of Virginia Woolf?	TRUE	383
1971	actress in a supporting role	Ellen Burstyn	The Last Picture Show	FALSE	384
1973	actress	Ellen Burstyn	The Exorcist	FALSE	385
1974	actress	Ellen Burstyn	Alice Doesn't Live Here Anymore	TRUE	386
1978	actress in a leading role	Ellen Burstyn	Same Time, Next Year	FALSE	387
1980	actress in a leading role	Ellen Burstyn	Resurrection	FALSE	388
2000	actress in a leading role	Ellen Burstyn	Requiem for a Dream	FALSE	389
1948	actress in a supporting role	Ellen Corby	I Remember Mama	FALSE	390
2007	actress in a leading role	Ellen Page	Juno	FALSE	391
1969	actor in a supporting role	Elliott Gould	Bob & Carol & Ted & Alice	FALSE	392
1949	actress in a supporting role	Elsa Lanchester	Come to the Stable	FALSE	393
1957	actress in a supporting role	Elsa Lanchester	Witness for the Prosecution	FALSE	394
1996	actress in a leading role	Emily Watson	Breaking the Waves	FALSE	395
1998	actress in a leading role	Emily Watson	Hilary and Jackie	FALSE	396
1992	actress in a leading role	Emma Thompson	Howards End	TRUE	397
1993	actress in a leading role	Emma Thompson	The Remains of the Day	FALSE	398
1993	actress in a supporting role	Emma Thompson	In the Name of the Father	FALSE	399
1995	actress in a leading role	Emma Thompson	Sense and Sensibility	FALSE	400
2012	actress in a leading role	Emmanuelle Riva	Amour	FALSE	401
1985	actor in a supporting role	Eric Roberts	Runaway Train	FALSE	402
1950	actor in a supporting role	Erich von Stroheim	Sunset Blvd.	FALSE	403
1955	actor	Ernest Borgnine	Marty	TRUE	404
1967	actress in a supporting role	Estelle Parsons	Bonnie and Clyde	TRUE	405
1968	actress in a supporting role	Estelle Parsons	Rachel, Rachel	FALSE	406
2001	actor in a supporting role	Ethan Hawke	Training Day	FALSE	407
1944	actress in a supporting role	Ethel Barrymore	None but the Lonely Heart	TRUE	408
1946	actress in a supporting role	Ethel Barrymore	The Spiral Staircase	FALSE	409
1947	actress in a supporting role	Ethel Barrymore	The Paradine Case	FALSE	410
1949	actress in a supporting role	Ethel Barrymore	Pinky	FALSE	411
1949	actress in a supporting role	Ethel Waters	Pinky	FALSE	412
1980	actress in a supporting role	Eva Le Gallienne	Resurrection	FALSE	413
1954	actress in a supporting role	Eva Marie Saint	On the Waterfront	TRUE	414
1945	actress in a supporting role	Eve Arden	Mildred Pierce	FALSE	415
1984	actor in a leading role	F. Murray Abraham	Amadeus	TRUE	416
1938	actress	Fay Bainter	White Banners	FALSE	417
1938	actress in a supporting role	Fay Bainter	Jezebel	TRUE	418
1961	actress in a supporting role	Fay Bainter	The Children's Hour	FALSE	419
1967	actress	Faye Dunaway	Bonnie and Clyde	FALSE	420
1974	actress	Faye Dunaway	Chinatown	FALSE	421
1976	actress in a leading role	Faye Dunaway	Network	TRUE	422
2005	actress in a leading role	Felicity Huffman	Transamerica	FALSE	423
1998	actress in a leading role	Fernanda Montenegro	Central Station	FALSE	424
1946	actress in a supporting role	Flora Robson	Saratoga Trunk	FALSE	425
2006	actor in a leading role	Forest Whitaker	The Last King of Scotland	TRUE	426
1988	actress in a supporting role	Frances McDormand	Mississippi Burning	FALSE	427
1996	actress in a leading role	Frances McDormand	Fargo	TRUE	428
2000	actress in a supporting role	Frances McDormand	Almost Famous	FALSE	429
2005	actress in a supporting role	Frances McDormand	North Country	FALSE	430
1965	actor in a supporting role	Frank Finlay	Othello	FALSE	431
2008	actor in a leading role	Frank Langella	Frost/Nixon	FALSE	432
1942	actor in a supporting role	Frank Morgan	Tortilla Flat	FALSE	433
1953	actor in a supporting role	Frank Sinatra	From Here to Eternity	TRUE	434
1955	actor	Frank Sinatra	The Man with the Golden Arm	FALSE	435
1974	actor in a supporting role	Fred Astaire	The Towering Inferno	FALSE	436
1979	actor in a supporting role	Frederic Forrest	The Rose	FALSE	437
1937	actor	Fredric March	A Star Is Born	FALSE	438
1946	actor	Fredric March	The Best Years of Our Lives	TRUE	439
1951	actor	Fredric March	Death of a Salesman	FALSE	440
2009	actress in a leading role	Gabourey Sidibe	Precious: Based on the Novel 'Push' by Sapphire	FALSE	441
1936	actress in a supporting role	Gale Sondergaard	Anthony Adverse	TRUE	442
1946	actress in a supporting role	Gale Sondergaard	Anna and the King of Siam	FALSE	443
1978	actor in a leading role	Gary Busey	The Buddy Holly Story	FALSE	444
1936	actor	Gary Cooper	Mr. Deeds Goes to Town	FALSE	445
1941	actor	Gary Cooper	Sergeant York	TRUE	446
1942	actor	Gary Cooper	The Pride of the Yankees	FALSE	447
1943	actor	Gary Cooper	For Whom the Bell Tolls	FALSE	448
1952	actor	Gary Cooper	High Noon	TRUE	449
2011	actor in a leading role	Gary Oldman	Tinker Tailor Soldier Spy	FALSE	450
1994	actor in a supporting role	Gary Sinise	Forrest Gump	FALSE	451
1988	actress in a supporting role	Geena Davis	The Accidental Tourist	TRUE	452
1991	actress in a leading role	Geena Davis	Thelma & Louise	FALSE	453
1974	actress	Gena Rowlands	A Woman under the Influence	FALSE	454
1980	actress in a leading role	Gena Rowlands	Gloria	FALSE	455
1967	actor in a supporting role	Gene Hackman	Bonnie and Clyde	FALSE	456
1970	actor in a supporting role	Gene Hackman	I Never Sang for My Father	FALSE	457
1971	actor	Gene Hackman	The French Connection	TRUE	458
1988	actor in a leading role	Gene Hackman	Mississippi Burning	FALSE	459
1992	actor in a supporting role	Gene Hackman	Unforgiven	TRUE	460
1945	actor	Gene Kelly	Anchors Aweigh	FALSE	461
1938	actor in a supporting role	Gene Lockhart	Algiers	FALSE	462
1945	actress	Gene Tierney	Leave Her to Heaven	FALSE	463
1968	actor in a supporting role	Gene Wilder	The Producers	FALSE	464
1969	actress	Genevieve Bujold	Anne of the Thousand Days	FALSE	465
1996	actor in a leading role	Geoffrey Rush	Shine	TRUE	466
1998	actor in a supporting role	Geoffrey Rush	Shakespeare in Love	FALSE	467
2000	actor in a leading role	Geoffrey Rush	Quills	FALSE	468
2010	actor in a supporting role	Geoffrey Rush	The King's Speech	FALSE	469
1975	actor in a supporting role	George Burns	The Sunshine Boys	TRUE	470
1959	actor in a supporting role	George C. Scott	Anatomy of a Murder	FALSE	471
1961	actor in a supporting role	George C. Scott	The Hustler	FALSE	472
1970	actor	George C. Scott	Patton	TRUE	473
1971	actor	George C. Scott	The Hospital	FALSE	474
1961	actor in a supporting role	George Chakiris	West Side Story	TRUE	475
2005	actor in a supporting role	George Clooney	Syriana	TRUE	476
2007	actor in a leading role	George Clooney	Michael Clayton	FALSE	477
2009	actor in a leading role	George Clooney	Up in the Air	FALSE	478
2011	actor in a leading role	George Clooney	The Descendants	FALSE	479
1967	actor in a supporting role	George Kennedy	Cool Hand Luke	TRUE	480
1950	actor in a supporting role	George Sanders	All about Eve	TRUE	481
1966	actor in a supporting role	George Segal	Who's Afraid of Virginia Woolf?	FALSE	482
1939	actress in a supporting role	Geraldine Fitzgerald	Wuthering Heights	FALSE	483
1953	actress in a supporting role	Geraldine Page	Hondo	FALSE	484
1961	actress	Geraldine Page	Summer and Smoke	FALSE	485
1962	actress	Geraldine Page	Sweet Bird of Youth	FALSE	486
1966	actress in a supporting role	Geraldine Page	You're a Big Boy Now	FALSE	487
1972	actress in a supporting role	Geraldine Page	Pete 'n' Tillie	FALSE	488
1978	actress in a leading role	Geraldine Page	Interiors	FALSE	489
1984	actress in a supporting role	Geraldine Page	The Pope of Greenwich Village	FALSE	490
1985	actress in a leading role	Geraldine Page	The Trip to Bountiful	TRUE	491
1990	actor in a leading role	Gerard Depardieu	Cyrano de Bergerac	FALSE	492
1976	actor in a leading role	Giancarlo Giannini	Seven Beauties	FALSE	493
1951	actor in a supporting role	Gig Young	Come Fill the Cup	FALSE	494
1958	actor in a supporting role	Gig Young	Teacher's Pet	FALSE	495
1969	actor in a supporting role	Gig Young	They Shoot Horses, Don't They?	TRUE	496
1940	actress	Ginger Rogers	Kitty Foyle	TRUE	497
1942	actress in a supporting role	Gladys Cooper	Now, Voyager	FALSE	498
1943	actress in a supporting role	Gladys Cooper	The Song of Bernadette	FALSE	499
1964	actress in a supporting role	Gladys Cooper	My Fair Lady	FALSE	500
1936	actress	Gladys George	Valiant Is the Word for Carrie	FALSE	501
1970	actress	Glenda Jackson	Women in Love	TRUE	502
1971	actress	Glenda Jackson	Sunday Bloody Sunday	FALSE	503
1973	actress	Glenda Jackson	A Touch of Class	TRUE	504
1975	actress	Glenda Jackson	Hedda	FALSE	505
1982	actress in a supporting role	Glenn Close	The World According to Garp	FALSE	506
1983	actress in a supporting role	Glenn Close	The Big Chill	FALSE	507
1984	actress in a supporting role	Glenn Close	The Natural	FALSE	508
1987	actress in a leading role	Glenn Close	Fatal Attraction	FALSE	509
1988	actress in a leading role	Glenn Close	Dangerous Liaisons	FALSE	510
2011	actress in a leading role	Glenn Close	Albert Nobbs	FALSE	511
1947	actress in a supporting role	Gloria Grahame	Crossfire	FALSE	512
1952	actress in a supporting role	Gloria Grahame	The Bad and the Beautiful	TRUE	513
1997	actress in a supporting role	Gloria Stuart	Titanic	FALSE	514
1950	actress	Gloria Swanson	Sunset Blvd.	FALSE	515
1960	actress in a supporting role	Glynis Johns	The Sundowners	FALSE	516
1969	actress in a supporting role	Goldie Hawn	Cactus Flower	TRUE	517
1980	actress in a leading role	Goldie Hawn	Private Benjamin	FALSE	518
1953	actress in a supporting role	Grace Kelly	Mogambo	FALSE	519
1954	actress	Grace Kelly	The Country Girl	TRUE	520
1990	actor in a supporting role	Graham Greene	Dances With Wolves	FALSE	521
1964	actress in a supporting role	Grayson Hall	The Night of the Iguana	FALSE	522
1939	actress	Greer Garson	Goodbye, Mr. Chips	FALSE	523
1941	actress	Greer Garson	Blossoms in the Dust	FALSE	524
1942	actress	Greer Garson	Mrs. Miniver	TRUE	525
1943	actress	Greer Garson	Madame Curie	FALSE	526
1944	actress	Greer Garson	Mrs. Parkington	FALSE	527
1945	actress	Greer Garson	The Valley of Decision	FALSE	528
1960	actress	Greer Garson	Sunrise at Campobello	FALSE	529
1997	actor in a supporting role	Greg Kinnear	As Good as It Gets	FALSE	530
1945	actor	Gregory Peck	The Keys of the Kingdom	FALSE	531
1946	actor	Gregory Peck	The Yearling	FALSE	532
1947	actor	Gregory Peck	Gentleman's Agreement	FALSE	533
1949	actor	Gregory Peck	Twelve O'Clock High	FALSE	534
1962	actor	Gregory Peck	To Kill a Mockingbird	TRUE	535
1937	actress	Greta Garbo	Camille	FALSE	536
1939	actress	Greta Garbo	Ninotchka	FALSE	537
1998	actress in a leading role	Gwyneth Paltrow	Shakespeare in Love	TRUE	538
1937	actor in a supporting role	H. B. Warner	Lost Horizon	FALSE	539
2010	actress in a supporting role	Hailee Steinfeld	True Grit	FALSE	540
1984	actor in a supporting role	Haing S. Ngor	The Killing Fields	TRUE	541
2007	actor in a supporting role	Hal Holbrook	Into the Wild	FALSE	542
1999	actor in a supporting role	Haley Joel Osment	The Sixth Sense	FALSE	543
2001	actress in a leading role	Halle Berry	Monster's Ball	TRUE	544
194