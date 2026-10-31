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
Petersville HS	Brown	47	495	214	531	1