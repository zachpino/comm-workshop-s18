# Answer Key

1. The female populations are found in the concept "SEX BY AGE".

- Females Total : B01001_026E
- Females 18-19 : B01001_031E
- Females 20: B01001_032E
- Females 21: B01001_033E
- Females 22-24: B01001_034E
- Females 25-29: B01001_035E
- Females 30-34: B01001_036E

For clarity, four calls will be used.

Total women in the USA:
```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B01001_026E&for=us&key=...
```

Results in 160,780,741 people.

Women 18-34 in the USA:
```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B01001_031E,B01001_032E,B01001_033E,B01001_034E,B01001_035E,B01001_036E&for=us&key=...
```

Sums to 36,562,943 people.

36,562,943 / 160,780,741 = 22.74%

Total women in Illinois:
```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B01001_026E&for=state:17&key=...
```

Results in 6,556,862 people.

Women 18-34 in Illinois:

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B01001_031E,B01001_032E,B01001_033E,B01001_034E,B01001_035E,B01001_036E&for=state:17&key=...
```

These sum to 1,500,276 people.

1,500,276 / 6,556,862 = 22.88%

##### Illinois has a higher ratio of young females.

-----

2. We can define 'Mediterranean' as composed of the following countries accessible in the variables table under the "PEOPLE REPORTING SINGLE ANCESTRY" concept. 'Spaniards' are, however, located within "HISPANIC OR LATINO ORIGIN BY SPECIFIC ORIGIN".

- Egyptian: B04004_007E
- Lebanese: B04004_010E
- Moroccan: B04004_011E
- French: B04004_040E
- Greek: B04004_044E
- Israeli: B04004_050E
- Italian: B04004_051E
- Croatian: B04004_029E
- Cypriot: B04004_030E
- Turkish: B04004_091E
- Slovenian: B04004_071E
- Israeli: B04004_050E
- Syrian: B04004_013E
- Albanian: B04004_003E
- Maltese: B04004_056E
- Basque: B04004_020E
- Spaniard: B03001_028E

This leaves out five peoples: Montenegrins, Monegasque, Algerian, Tunisian, and Libyan.

We could optionally try to capture the Montenegrin population via the "Yugloslav" historical ethnic identity. The rest are impossible to distinguish from the comprehensive "Arab" ethnic data points.

- Yugoslav: B04004_107E

The call would thus look like this to capture the people with "Mediterranean" ancestry:

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B04004_007E,B04004_010E,B04004_011E,B04004_040E,B04004_044E,B04004_050E,B04004_051E,B04004_029E,B04004_030E,B04004_091E,B04004_071E,B04004_050E,B04004_013E,B04004_003E,B04004_056E,B04004_020E,B03001_028E,B04004_107E&for=us&key=...
```

This returns...

```
[["NAME","B04004_007E","B04004_010E","B04004_011E","B04004_040E","B04004_044E","B04004_050E","B04004_051E","B04004_029E","B04004_030E","B04004_091E","B04004_071E","B04004_050E","B04004_013E","B04004_003E","B04004_056E","B04004_020E","B03001_028E","B04004_107E","us"],
["United States","185873","236422","69413","1836991","582315","88952","6652806","153011","4817","138494","60043","88952","80135","156531","16582","24802","756552","181566","1"]]
```

These values sum to 11,314,257 people.

We can similarly look at the datapoints within the concept "ASIAN ALONE BY SELECTED GROUPS" for many of the South-East Asian countries.

- Vietnam: B02015_022E
- Laos: B02015_013E
- Cambodia: B02015_006E
- Thailand: B02015_021E
- Myanmar: B02015_005E
- Indonesia: B02015_010E
- Malaysia: B02015_014E
- Philippines: B02015_008E
- Hmong: B02015_009E

There is unfortunately no way to capture the East Timorese, Bruneian, and Singaporean populations.

The call: 

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B02015_022E,B02015_013E,B02015_006E,B02015_021E,B02015_005E,B02015_010E,B02015_014E,B02015_008E,B02015_009E&for=us&key=...
```

The response:

```
[["NAME","B02015_022E","B02015_013E","B02015_006E","B02015_021E","B02015_005E","B02015_010E","B02015_014E","B02015_008E","B02015_009E","us"],
["United States","1710547","207999","263396","188673","126590","71451","18803","2717844","267009","1"]]
```

These values sum to 5,572,312 people.

##### There are more people in the USA that self-identify as single ancestry Mediterranean than South-East Asian, by 5,741,945 people.

-----

3. These numbers can be discovered in the concept of "PERIOD OF ENTRY BY NATIVITY AND CITIZENSHIP STATUS IN THE UNITED STATES".

- Total Entered 2000-2009: B05005_009E
- Total Entered 1990-1999: B05005_014E

Those who entered 2000-2009 in California (06) and New York (36).

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B05005_009E&for=state:06,36&key=...
```

```
[["NAME","B05005_009E","state"],
["California","2559124","06"],
["New York","1198605","36"]]
```

Those who entered 1990-1999 in California (06) and New York (36).

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B05005_014E&for=state:06,36&key=...
```

```
[["NAME","B05005_014E","state"],
["California","2600323","06"],
["New York","1150072","36"]]
```

[Quick Google searches](https://www.google.com/publicdata/explore?ds=kf7tgg1uo9ude_&met_y=population&hl=en&dl=en) yield a total population in 2009 for California of 36,961,200 and in 1999 a population of 33,499,200. 

California from 2000-2009: 2559124 / 36961200 = 6.923% of the population

California from 1990-1999: 2600323 / 33499200 = 7.762% of the population

New York from 2000-2009: 1198605 / 19307100 = 6.208% of the population

New York from 1990-1999: 1150072 / 18882700 = 6.090% of the population

##### California decreased, New York increased.

-----

4. In the concept "RATIO OF INCOME TO POVERTY LEVEL IN THE PAST 12 MONTHS BY NATIVITY OF CHILDREN UNDER 18 YEARS IN FAMILIES AND SUBFAMILIES BY LIVING ARRANGEMENTS AND NATIVITY OF PARENTS," we can find the answer to this question.

- Children Living under the Poverty Line (Poverty Level > Income): B05010_002E
- Children Living above double the Poverty Line (2.0 * Poverty Level < Income): B05010_018E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B05010_002E,B05010_018E&for=school%20district%20(unified):*&in=state:17&key=...
```

Dividing one value by the other yields a rankable list of numbers.

##### Brooklyn Community Unit School District 188 (23640) has 30x more students below the poverty line than above 2x the poverty line. It is located within the St. Louis metropolitan area, east of the Missippi.

##### Elmwood Community Unit School District 322 (14050) has an effectively infinite ratio, as it has 0 students below the poverty line, and 603 above 2x the poverty line. It is located in Central Illinois, northwest of Bloomington.

Population under 18 is available in its own concept, "POPULATION UNDER 18 YEARS BY AGE".

- Minors: B09001_001E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B09001_001E&for=school%20district%20(unified):23640,14050&in=state:17&key=...
```

##### Brooklyn Community Unit School District 188 serves 325 minors. 

##### Elmwood Community Unit School District 322 serves 812 minors. 

---

#### A cool alternative approach to question 4 from Jessica Lee (Thanks Jessica!)

Find the "RATIO OF INCOME TO POVERTY LEVEL IN THE PAST 12 MONTHS" for all of the school districts.

- Under .50 Income to Poverty Level Ratio: C17002_002E 
- 0.50 to 0.99 Income to Poverty Level Ratio: C17002_003E 
- 1.00 to 1.24 Income to Poverty Level Ratio: C17002_004E 
- 1.25 to 1.49 Income to Poverty Level Ratio: C17002_005E 
- 1.50 to 1.84 Income to Poverty Level Ratio: C17002_006E 
- 1.85 to 1.99 Income to Poverty Level Ratio: C17002_007E 
- 2.00 and over Income to Poverty Level Ratio: C17002_008E 

```
api.census.gov/data/2015/acs/acs5?get=NAME,C17002_002E,C17002_003E,C17002_004E,C17002_005E,C17002_006E,C17002_007E,C17002_008E&for=school%20district%20(unified):*&in=state:17&key=...
```

|NAME	|Under .5	|.5 - .99	|1 - 1.24	|1.25 - 1.49	|1.5 - 1.84	|1.85 - 1.99	|Over 2.0	|school district (unified) # |
|---	|---	|---	|---	|---	|---	|---	|---	|---	|
|River Ridge Community Unit School District | 210	|139	|185	|104	|82	|250	|85	|2634	|00001|
|Casey-Westfield Community Unit School District | 4C	|360	|380	|320	|207	|710	|221	|3878	|00002|
|Blue Ridge Community Unit School District | 18	|193	|259	|102	|250	|327	|165	|3599	|00003|
|Norris City-Omaha-Enfield Community Unit School District | 3	|412	|205	|269	|299	|337	|78	|2970	|00004|
|Prairie Central Community Unit School District | 8	|492	|695	|580	|473	|632	|443	|7191	|00005|
|Eastland Community Unit School District | 308	|125	|200	|129	|293	|339	|169	|3010	|00007|
|Goreville Community Unit School District | 1	|90	|344	|108	|193	|122	|195	|2850	|00014|
|Joppa-Maple Grove Unit District | 38	|112	|175	|38	|44	|195	|84	|867	|00015|
|Gibson City-Melvin-Sibley Community Unit School District | 5	|216	|693	|276	|321	|380	|134	|3744	|00041|
...

Apply the same weighted averaging method as detailed in question 12 below to each income bucket. Multiply each population count that the API returns by the average of the range of income percentages (the 1.5 to 1.84 bucket is multipled by 1.67)

| Multiplier ->	| 0.25|	0.7|	1.12|	1.37|	1.67|	1.92|	2 | Ranking Sum |
|---	|---	|---	|---	|---	|---	|---	|---	|---	|
| River Ridge Community Unit School District 210 |	34.75 |	129.5|	116.4|	112.34|	417.5|	163.2|	5268 | 6241.77 |
| Casey-Westfield Community Unit School District 4C |	90	|266|	358.4|	283.59|	1185.7|	424.32|	7756 | 10364.01|
| Blue Ridge Community Unit School District 18 |	48.25	|181.3|	114.24|	342.5|	546.09|	316.8|	7198 | 8747.18|
| Norris City-Omaha-Enfield Community Unit School District 3 |	103|	143.5|	301.28|	409.63|	562.79|	149.76	| 5940 |7609.96|
| Prairie Central Community Unit School District 8 |	123| 486.5|	649.6|	648.01|	1055.44|	850.56|	14382 | 18195.11|
| Eastland Community Unit School District 308 |	31.25|	140|	144.48|	401.41|	566.13|	324.48|	6020 |7627.75|
| Goreville Community Unit School District 1 |	22.5|	240.8|	120.96|	264.41|	203.74|	374.4|	5700 | 6926.81|
| Joppa-Maple Grove Unit District 38 |	28|	122.5|	42.56|	60.28|	325.65|	161.28|	1734 | 2474.27|
| Gibson City-Melvin-Sibley Community Unit School District 5|	54	| 485.1|	309.12|	439.77|	634.6|	257.28|	7488 | 9667.87|
...

Summing the results per row yields a rankable indicator (held in the rightmost cell of each row above). The higher this number, the higher the income to poverty ratio is for that district. 

##### The lowest aggregate ratio is Brooklyn Community Unit School District 188, with an indicator of 847.

##### The highest aggregate ratio is Chicago Public School District 299, with 4,127,259.

Finding the minor counts for these districts is detailed above. 

This method uses a different logic for defining poverty, and is based on evaluating *individuals* rather than *households*. Depending on the story you seek to tell, one or the other method might be more appropriate.

-----

5. In the concept "RATIO OF INCOME TO POVERTY LEVEL IN THE PAST 12 MONTHS BY NATIVITY OF CHILDREN UNDER 18 YEARS IN FAMILIES AND SUBFAMILIES BY LIVING ARRANGEMENTS AND NATIVITY OF PARENTS," we can find the answer to this question.

Total children under 18 years of age with less than a 1.0 income to poverty ratio : B05010_002E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B05010_002E&for=school%20district%20(unified):*&in=state:17&key=...
```

Counting minors requires some summing, or can be queried directly as in question 4. This would be the call for a summable set of numbers.

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B01001_003E,B01001_004E,B01001_005E,B01001_006E,B01001_027E,B01001_028E,B01001_029E,B01001_030E&for=school%20district%20(unified):09930&in=state:17&key=...
```

##### The Chicago Public Schools (Illinois District 299) has the highest count of children living under the poverty line, with 185,678 children, of a total of 603,463. This is a proportion of 30.768%. The district is the whole of metropolitan Chicago.

-----

6. Within "PLACE OF BIRTH BY LANGUAGE SPOKEN AT HOME AND ABILITY TO SPEAK ENGLISH IN THE UNITED STATES" we can find these data points.

- Speak Spanish and Speak English "very well": B06007_004E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B06007_004E&for=combined%20statistical%20area:176,348,408&key=...
```

##### Chicago has 891,717 bilingual English/Spanish individuals, Los Angeles has 3,484,207, and New York has 2,226,355.

-----

7. Within "PLACE OF BIRTH BY MARITAL STATUS IN THE UNITED STATES" we can find the necessary values.

- Total Divorced: B06008_004E
- Total Married: B06008_003E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B06008_004E,B06008_003E&for=state:*&key=...
```

##### Utah has the highest ratio, 6.045x more married people than divorced people. Washington DC has the lowest ration, 2.930x more married people than divorced.

-----

8. Under "TOTAL FIELDS OF BACHELOR'S DEGREES REPORTED" we can query for degree counts.

- Science and Engineering Related Fields: B15012_009E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B15012_009E&for=state:*&key=...
```

##### California has the most people with science and engineering bachelor's degrees: 670,716 people. 

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B15012_009E&for=county:*&in=state:06&key=...
```

##### Within California, Los Angeles County has the most, with 162,004 individuals. Perhaps *Hollywood* and its large opportunity count for individuals with expertise in audio and visual content has something to do with its rank? In addition, the [large concentration of technical universities](https://en.wikipedia.org/wiki/Category:Universities_and_colleges_in_Los_Angeles_County,_California), including Caltech and its NASA JPL relationship, certainly contributes.

-----

9. In the concept "PLACE OF BIRTH BY EDUCATIONAL ATTAINMENT IN THE UNITED STATES". 

- Graduate or professional degree: B06009_006E
- Total population: B01001_001E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B06009_006E,B01001_001E&for=state:27,55,17,18,26,39,42,36&key=...
```

```
[["NAME","B06009_006E","B01001_001E","state"],
["Illinois","1066084","12873761","17"],
["Indiana","375509","6568645","18"],
["Michigan","696956","9900571","26"],
["Minnesota","406930","5419171","27"],
["New York","1992047","19673174","36"],
["Ohio","761265","11575977","39"],
["Pennsylvania","986815","12779559","42"],
["Wisconsin","363838","5742117","55"]]
```

##### New York has the most individuals with advanced degrees: 19,673,174. It also has the highest proportion: 10.126%. Illinois is a close second in both, and Minnesota overperforms for its population count.

10. The concept "GEOGRAPHICAL MOBILITY IN THE PAST YEAR BY AGE FOR CURRENT RESIDENCE IN THE UNITED STATES" holds these numbers.

Moved from different state, 1 to 4 years: B07001_066E
Moved from abroad, 1 to 4 years: B07001_082E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B07001_066E,B07001_082E&for=state:*&key=...
```

##### 49,868 young children moved into Texas, and is the most mobile state for children by a significant margin.

-----

11. Within the concept "SEX OF WORKERS BY MEANS OF TRANSPORTATION TO WORK" such data is tabulated.

Total that Drove Alone via Car, Truck, or Van: B08006_003E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B08006_003E&for=congressional%20district:*&in=state:17&key=...
```

##### The 7th Congressional District in Illinois (Downtown Chicago and the west side) has the fewest solo drivers, and the 14th (North and West suburbs of Chicago) has the most solo drivers.

##### The representatives are Danny Davis (D-IL-7) and Randy Hultgren (R-IL-14).

[OpenSecrets](http://www.opensecrets.org) is a wonderful resource for discovering how much money congressional representatives receive. 

##### Danny Davis receives $10,500 from transportation sector lobbying groups (of which $5,000 is railroad related), and Randy Hultgren receives $18,500 (no railroad contributions, all automobile-related).

-----

12. We need to do some intermediate calculations to determine the answer to this question, from the "SEX OF WORKERS BY TIME LEAVING HOME TO GO TO WORK" concept.

- 5:00 a.m. to 5:29 a.m.: B08011_003E
- 5:30 a.m. to 5:59 a.m.: B08011_004E
- 6:00 a.m. to 6:29 a.m.: B08011_005E
- 6:30 a.m. to 6:59 a.m.: B08011_006E
- 7:00 a.m. to 7:29 a.m.: B08011_007E
- 7:30 a.m. to 7:59 a.m.: B08011_008E
- 8:00 a.m. to 8:29 a.m.: B08011_009E
- 8:30 a.m. to 8:59 a.m.: B08011_010E


```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B08011_003E,B08011_004E,B08011_005E,B08011_006E,B08011_007E,B08011_008E,B08011_009E,B08011_010E&for=combined%20statistical%20area:122,176,216,288,348,408,500&key=...
```

This returns...

```
[["NAME","B08011_003E","B08011_004E","B08011_005E","B08011_006E","B08011_007E","B08011_008E","B08011_009E","B08011_010E","combined statistical area"],
["Atlanta--Athens-Clarke County--Sandy Springs, GA CSA","88890","113665","249473","255886","409975","298753","325509","142964","122"],
["Chicago-Naperville, IL-IN-WI CSA","194824","221985","437065","417461","638768","477743","498765","232360","176"],
["Denver-Aurora, CO CSA","56828","76511","149472","168601","239502","188866","171511","87763","216"],
["Houston-The Woodlands, TX CSA","147476","176860","344168","313699","453903","302418","301768","127525","288"],
["New York-Newark, NY-NJ-CT-PA CSA","286207","353544","800537","856477","1552336","1216090","1669010","819991","408"],
["Seattle-Tacoma, WA CSA","95055","119603","188208","196880","264763","217463","207595","121546","500"]]
```

We can mass sum all of the values to acquire aggregate commuter counts.

Atlanta: 1885115
Chicago: 3118971
Denver: 1139054
Houston: 2167817
LA: 5190114
NYC: 7554192
Seattle: 1411113

And then arrive at percentages.

|   	|5:00 a.m. to 5:29 a.m.   	|5:30 a.m. to 5:59 a.m.   	|6:00 a.m. to 6:29 a.m.   	|6:30 a.m. to 6:59 a.m.   	|7:00 a.m. to 7:29 a.m.   	|7:30 a.m. to 7:59 a.m.   	|8:00 a.m. to 8:29 a.m.   	|8:30 a.m. to 8:59 a.m.   	|
|---	|---	|---	|---	|---	|---	|---	|---	|---	|
|Atlanta|4.72%|6.03%|13.23%|13.57%|21.75%|15.85%|17.27%|7.58%|
|Chicago|6.25%|7.12%|14.01%|13.38%|20.48%|15.32%|15.99%|7.45%|
|Denver |4.99%|6.72%|13.12%|14.80%|21.03%|16.58%|15.06%|7.70%|
|Houston|6.80%|8.16%|15.88%|14.47%|20.94%|13.95%|13.92%|5.88%|
|LA 	|7.05%|7.02%|13.45%|12.16%|20.51%|14.38%|17.14%|8.28%|
|NYC   	|3.79%|4.68%|10.60%|11.34%|20.55%|16.10%|22.09%|10.85%|
|Seattle|6.74%|8.48%|13.34%|13.95%|18.76%|15.41%|14.71%|8.61%|

General patterns are already obvious, but we can do some [weighted averaging](https://en.wikipedia.org/wiki/Weighted_arithmetic_mean) to get a full ranking. By assigning consistently larger numbers to each time domain, we can then multiply that number by the percentage in each cell, and sum for each city.

|   	|1	  |2	|3	   |4     |5   	 |6   	|7   	|8   	|Sum   | Rank 				|
|---	|---  |---	|---   |---	  |---	 |---	|---	|---	|---   |---  				|
|Atlanta|0.0472|0.1206|0.3970|0.5430|1.0874|0.9509|1.2087|0.6067|4.9614|6 				|
|Chicago|0.0625|0.1423|0.4204|0.5354|1.0240|0.9190|1.1194|0.5960|4.8190|3 				|
|Denver |0.0499|0.1343|0.3937|0.5921|1.0513|0.9949|1.0540|0.6164|4.8866|5 				|
|Houston|0.0680|0.1632|0.4763|0.5788|1.0469|0.8370|0.9744|0.4706|4.6153|1 (Earliest Drivers) 				|
|LA 	|0.0705|0.1405|0.4035|0.4865|1.0255|0.8628|1.1999|0.6626|4.8519|4 				|
|NYC   	|0.0379|0.0936|0.3179|0.4535|1.0275|0.9659|1.5466|0.8684|5.3112|7 (Latest Drivers) 				|
|Seattle|0.0674|0.1695|0.4001|0.5581|0.9381|0.9246|1.0298|0.6891|4.7767|2 				|

##### Houston drivers leave earliest, which is helped by the fact that the city is decently impacted by a poorly matching timezone. New Yorkers leave latest.

![timezone drift](http://i.kinja-img.com/gawker-media/image/upload/19ghg6nbgk7f1png.png)

-----

13. The aptly named concept "SEX BY AGE BY VISION DIFFICULTY" gives this easily.

- Male: B18105_004E
- Female: B18103_021E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B18103_002E,B18103_021E&for=us&key=...
```

##### There are 159,396,497 women in America with vision difficulties, and 152,119,835 men. 7,276,662 more women have vision difficulties.

-----

14. All public assistance programs show up under "RECEIPT OF SUPPLEMENTAL SECURITY INCOME (SSI), CASH PUBLIC ASSISTANCE INCOME, OR FOOD STAMPS/SNAP IN THE PAST 12 MONTHS BY HOUSEHOLD TYPE FOR CHILDREN UNDER 18 YEARS IN HOUSEHOLDS".

- Household Count with Children under 18: B09010_001E
- Household Receiving Public Assistance with Children under 18 : B09010_002E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B09010_001E,B09010_002E&for=state:*&key=...
```

##### Simple division shows that a bit more than half, 50.177% of Puerto Rican households receive some sort of federal assistance. It is the highest state in this respect. It receives around [$21 billion in aid from the US federal goverment, much less than it would receive if it were a full state](https://en.wikipedia.org/wiki/Welfare_in_Puerto_Rico#Federal_aid).

-----

15. Data on walking and other gross motor impairments can be found in the "SEX BY AGE BY AMBULATORY DIFFICULTY" concept.

- Male, 5-17, with an Ambulatory Impairment: B18105_004E
- Female, 5-17, with an Ambulatory Impairment: B18105_020E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B18105_004E,B18105_020E&for=school%20district%20(unified)&in=state:17&key=...
```

##### The highest school district in Illinois in terms of students with ambulatory impairments is not a school district at all, but rather "Remainder of Illinois," which here can be parsed as a combination of [homeschooled children and places where there exists elementary schools but not a matching secondary school](https://www.census.gov/geo/reference/gtc/gtc_sd.html). Chicago Public Schools (Illinois Unified School District 299) have the second highest number of children with ambulatory impairments, with 3,416 students needing mobility assistance.

CPS recently reworked their algorithm for disbursing the $900 million budget for special education, and then reversed course twice after [public outcry](https://www.wbez.org/shows/wbez-news/wbez-investigation-cps-secretly-overhauled-special-education-at-students-expense/2f6907ea-6ad2-4557-9a03-7da60710f8f9).

-----

16.  Data on cognitive impairments can be found in the "SEX BY AGE BY COGNITIVE DIFFICULTY" concept.

- Male, 5-17, with an Cognitive Impairment: B18104_004E
- Female, 5-17, with an Cognitive Impairment: B18104_020E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B18104_004E,B18104_020E&for=school%20district%20(unified)&in=state:17&key=...
```

##### Same as above, with "Remainder of Illinois" first and CPS second, with 12,198 students needing cognitive assistance.
	
-----

17. The hyper-specific concept "SEX BY WORK EXPERIENCE IN THE PAST 12 MONTHS BY INCOME IN THE PAST 12 MONTHS (IN 2016 INFLATION-ADJUSTED DOLLARS) FOR THE POPULATION 15 YEARS AND OVER" helps answer this.

- Male, With income $100,000 or more: B19325_025E
- Female, With income $100,000 or more: B19325_072E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B19325_025E,B19325_072E&for=state:06,17,36&key=...
```

California has 1,504,067 high-earning men and 619,676 high-earning women, a difference of 884,392 people. 2.427x more men than women earn more than $100,000.
Illinois has 467,166 high-earning men and 163,503 high-earning women, a difference of 303,663 people. 2.857x more men than women earn more than $100,000.
New York has 761,823 high-earning men and 354,982 high-earning women, a difference of 406,841 people 2.146x more men than women earn more than $100,000.

##### California has the biggest difference between the genders, but Illinois has the highest percentage gap.

-----

18. Quite the descriptive concept for these: "DETAILED OCCUPATION BY MEDIAN EARNINGS IN THE PAST 12 MONTHS (IN 2016 INFLATION-ADJUSTED DOLLARS) FOR THE FULL-TIME, YEAR-ROUND CIVILIAN EMPLOYED POPULATION 16 YEARS AND OVER".

Artists: B24121_143E
Designers: B24121_144E
Musicians: B24121_149E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B24121_143E,B24121_144E,B24121_149E&for=state:*&key=...
```

But null data results! So sad. Whenever 'null' is returned, that means that the data is [suppressed](https://www.census.gov/programs-surveys/acs/technical-documentation/data-suppression.html) for some specific sociopolitical reason, or is only used to track other variables and isn't designed for consumption. In this case, the data is only collected to track wage changes per industry, and so the raw counts are not made available. The data is, though, not suppressed at the USA level.

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B24121_143E,B24121_144E,B24121_149E&for=us&key=...
```


##### Unanswerable, though data is collected.

-----

19. The aptly named "YEAR STRUCTURE BUILT" concept holds the key here.

- Total Structures: B25034_001E
- Built 2014 or Later: B25036_003E
- Built 1939 or Earlier: B25034_011E

```
https://api.census.gov/data/2015/acs/acs5?get=NAME,B25034_001E,B25036_003E,B25034_011E&for=combined%20statistical%20area:176,348,408&key=...
```

```
[["NAME","B25034_001E","B25036_003E","B25034_011E","combined statistical area"],
["Chicago-Naperville, IL-IN-WI CSA","3964430","1308","882907","176"],
["Los Angeles-Long Beach, CA CSA","6346543","2434","605701","348"],
["New York-Newark, NY-NJ-CT-PA CSA","9319133","2390","2577416","408"]]
```

- Chicago CSA: Of 3,964,430 countable structures, 1,308 were built after 2014 (0.0329%) and 882,907 before 1939 (22.270%).
- Los Angeles CSA: Of 6,346,543 countable structures, 2,434 were built after 2014 (.0383%) and 605,701 before 1939 (9.543%).
- New York CSA: Of 9,319,133 countable structures, 2,390 were built after 2014 (.0256%) and 2,577,416 before 1939 (27.657%).

##### New York has the highest percentage of old homes, and Los Angeles has the highest percentage of new homes. Chicago is intermediate in both.

-----

20. This requires querying the 2016 1 Year ACS, as it is a newly tracked variable.

Total Households: B28002_001E
With a Broadband Internet Subscription: B28002_004E

```
https://api.census.gov/data/2016/acs/acs1?get=NAME,B28002_001E,B28002_004E&for=county&in=state:17&key=...
```

Note that not all counties are tabulated in the 1 year ACS, and so only a small subset of the 102 Illinois counties are publicized.

##### McHenry County does the best with internet access, at 91.66% penetration. Williamson County, near the southern tip of the state, is the worst at 74.62% broadband access. Cook County households, home to Chicago, has only an 80.573% broadband connection rate.
