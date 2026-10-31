# StrataScratch Question ID: 9610 - Find Students At Median Writing

| Attribute | Details |
| :--- | :--- |
| **Question ID** | `9610` |
| **Title** | **Find Students At Median Writing** |
| **Difficulty** | `Medium` |
| **Company Tag** | **Tech Industry** |
| **Category** | `Date & Time Analytics` |
| **StrataScratch Link** | [View Problem on StrataScratch](https://platform.stratascratch.com/coding/9610) |

---

## 1. Problem Description

Solve the 'Find Students At Median Writing' interview challenge from StrataScratch. Process the input records and compute the requested metrics as specified by the requirements.

---

## 2. Input Tables & Schema

```text
Table
sat_scores
More about this question
Hints
Expected Output
All required columns and the first 5 rows of the solution are shown

student_id
113
109
100
sat_scores
Preview
school	teacher	student_id	sat_writing	sat_verbal	sat_math	hrs_studied	id	average_sat	love
Washington HS	Frederickson	1	583	307	528	190	1	583	
Washington HS	Frederickson	2	401	791	248	149	2	401	
Washington HS	Frederickson	3	523	445	756	166	3	523	
Washington HS	Frederickson	4	306	269	327	137	4	306	
Washington HS	Frederickson	5	300	539	743	115	5	300	
Washington HS	Frederickson	6	213	500	771	173	6	213	
Washington HS	Frederickson	7	548	683	740	47	7	548	
Washington HS	Frederickson	8	314	503	341	174	8	314	
Washington HS	Frederickson	9	401	630	666	111	9	401	
Washington HS	Frederickson	10	532	683	316	134	10	532	
Washington HS	Frederickson	11	654	422	350	118	11	654	
Washington HS	Frederickson	12	642	287	282		12	642	
Washington HS	Frederickson	13	424	230	393	111	13	424	
Washington HS	Spellman	14	481	710	681	175	14	481	
Washington HS	Spellman	15	569	286	268	118	15	569	
Washington HS	Spellman	16	399	290	248	195	16	399	
Washington HS	Spellman	17	353	308	231	4	17	353	
Washington HS	Spellman	18	502	292	264	94	18	502	
Washington HS	Spellman	19	799	406	247	178	19	799	
Washington HS	Spellman	20	451	690	238	51	20	451	
Washington HS	Spellman	21	624	331	796	71	21	624	
Washington HS	Spellman	22	481	608	420	124	22	481	
Washington HS	Spellman	23	406	724	518	97	23	406	
Washington HS	Spellman	24	206	709	615	38	24	206	
Washington HS	Spellman	25	502	291	716		25	502	
Washington HS	Spellman	26	333	478	603	106	26	333	
Washington HS	Spellman	27	661	782	393	89	27	661	
Washington HS	Spellman	28	254	630	629	118	28	254	
Washington HS	Spellman	29	378	363	750	34	29	378	
Washington HS	Spellman	30	690	692	363	13	30	690	
Washington HS	Spellman	31	600	545	314	65	31	600	
Petersville HS	Davis	32	635	743	695	161	32	635	
Petersville HS	Davis	33	756	595	427		33	756	
Petersville HS	Davis	34	627	429	541	37	34	627	
Petersville HS	Davis	35	304	780	516	145	35	304	
Petersville HS	Davis	36	346	337	435	172	36	346	
Petersville HS	Davis	37	533	438	494	21	37	533	
Petersville HS	Davis	38	779	656	724		38	779	
Petersville HS	Davis	39	502	368	639	23	39	502	
Petersville HS	Davis	40	513	614	780	186	40	513	
Petersville HS	Davis	41	664	439	472	49	41	664	
Petersville HS	Davis	42	431	427	454	109	42	431	
Petersville HS	Davis	43	426	470	448	184	43	426	
Petersville HS	Davis	44	376	330	724	17	44	376	
Petersville HS	Brown	45	564	402	319	120	45	564	
Petersville HS	Brown	46	797	392	337	101	46	797	
Petersville HS	Brown	47	495	214	531	166	47	495	
Petersville HS	Brown	48	426	745	314	163	48	426	
Petersville HS	Brown	49	322	369	531	157	49	322	
Petersville HS	Brown	50	794	732	519	102	50	794	
Petersville HS	Brown	51	540	517	347	197	51	540	
Petersville HS	Brown	52	640	600	699	27	52	640	
Petersville HS	Brown	53	436	321	679	63	53	436	
Petersville HS	Brown	54	303	235	506	100	54	303	
Petersville HS	Brown	55	531	380	325	95	55	531	
Petersville HS	Brown	56	245	378	678	62	56	245	
Petersville HS	Brown	57	552	597	669	72	57	552	
Petersville HS	Brown	58	457	599	275	162	58	457	
Petersville HS	Brown	59	318	377	603	130	59	318	
Petersville HS	Brown	60	431	314	205	15	60	431	
Petersville HS	Brown	61	315	520	719	142	61	315	
Petersville HS	Perry	62	793	365	240	140	62	793	
Petersville HS	Perry	63	529	623	239	23	63	529	
Petersville HS	Perry	64	322	385	765	95	64	322	
Petersville HS	Perry	65	481	697	594	19	65	481	
Petersville HS	Perry	66	725	646	216	196	66	725	
Petersville HS	Perry	67	668	738	256	17	67	668	
Petersville HS	Perry	68	648	336	216	40	68	648	
Petersville HS	Perry	69	695	545	201	52	69	695	
Petersville HS	Perry	70	550	669	651	161	70	550	
Petersville HS	Perry	71	649	654	636		71	649	
Petersville HS	Perry	72	264	210	545	51	72	264	
Petersville HS	Perry	73	430	707	739	56	73	430	
Petersville HS	Perry	74	647	656	669	47	74	647	
Petersville HS	Perry	75	271	587	504	187	75	271	
Petersville HS	Perry	76	637	435	240	65	76	637	
Petersville HS	Perry	77	677	371	509	55	77	677	
Petersville HS	Perry	78	311	396	552	108	78	311	
Petersville HS	Perry	79	615	681	633	194	79	615	
Petersville HS	Perry	80	738	313	580	67	80	738	
Petersville HS	Perry	81	608	584	580	93	81	608	
Petersville HS	Perry	82	518	799	730	10	82	518	
Petersville HS	Perry	83	649	200	586	86	83	649	
Petersville HS	Perry	84	747	290	729	144	84	747	
St. John's	Rajaram	85	395	495	649	197	85	395	
St. John's	Rajaram	86	360	359	651	30	86	360	
St. John's	Rajaram	87	697	798	767	187	87	697	
St. John's	Rajaram	88	211	441	667	199	88	211	
St. John's	Rajaram	89	563	488	236	47	89	563	
St. John's	Rajaram	90	268	288	359	51	90	268	
St. John's	Rajaram	91	394	214	735	191	91	394	
St. John's	Rajaram	92	242	471	350	83	92	242	
St. John's	Rajaram	93	324	649	509	85	93	324	
St. John's	Rajaram	94	742	604	629	82	94	742	
St. John's	Rajaram	95	686	708	489	88	95	686	
St. John's	Rajaram	96	365	266	762	181	96	365	
St. John's	Rajaram	97	413	344	718	52	97	413	
St. John's	Rajaram	98	785	237	383	90	98	785	
St. John's	Rajaram	99	667	541	510	74	99	667	
St. John's	Rajaram	100	512	614	481	183	100	512	
St. John's	Rajaram	101	407	535	312	0	101	407	
St. John's	Rajaram	102	208	295	682	163	102	208	
St. John's	Rajaram	103	759	316	477	96	103	759	
St. John's	Rajaram	104	458	432	268	55	104	458	
St. John's	Williams	105	669	316	409	9	105	669	
St. John's	Williams	106	521	722	591	8	106	521	
St. John's	Williams	107	220	597	667	147	107	220	
St. John's	Williams	108	780	447	345	51	108	780	
St. John's	Williams	109	512	242	357	67	109	512	
St. John's	Williams	110	246	698	223	91	110	246	
St. John's	Williams	111	581	617	613	102	111	581	
St. John's	Williams	112	303	208	427	15	112	303	
St. John's	Williams	113	512	559	686	197	113	512	
St. John's	Williams	114	636	402	201	157	114	636	
St. John's	Williams	115	541	453	704	193	115	541	
St. John's	Williams	116	457	406	723	20	116	457	