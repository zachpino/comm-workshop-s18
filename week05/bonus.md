### Bonus Question from Last Week

As was asked last week — How many households who are *exclusively native american or alaskan native* have the broadband internet subscription necessary to access online native american language resources in each state? Are any of those numbers surprising? Is the percentage of native american households who can access that page smaller or larger than the entire population's equivalent percentage?

-----

To answer this question, we may want to look at the following data points for comparison.

- B28009C_004E: `Estimate!!Total!!Has a computer!!With a broadband Internet subscription` from the group `PRESENCE OF A COMPUTER AND TYPE OF INTERNET SUBSCRIPTION IN HOUSEHOLD (AMERICAN INDIAN AND ALASKA NATIVE ALONE)`

- B28009C_001E: `Estimate!!Total` of Native American Households

- B28002_004E: `Estimate!!Total!!With an Internet subscription!!Broadband of any type` from the group `PRESENCE AND TYPES OF INTERNET SUBSCRIPTIONS IN HOUSEHOLD`

- B28002_001E: `Estimate!!Total` of All Households

```
api.census.gov/data/2016/acs/acs1?get=NAME,B28009C_004E,B28009C_001E,B28002_004E,B28002_001E&for=state:*
```

```
[["NAME","B28009C_004E","B28009C_001E","B28002_004E","B28002_001E","state"],
["Alabama","20240","24269","1383347","1852518","01"],
["Alaska","80490","104186","213002","248468","02"],
["Arizona","161167","298774","2093778","2519052","04"],
["Arkansas","14073","18250","810624","1142718","05"],
["California","233630","281411","11055070","12944178","06"],
["Colorado","41164","52766","1833549","2108992","08"],
["Connecticut","8344","9639","1141859","1357269","09"],
["Delaware","2869","4004","292600","351085","10"],
["District of Columbia",null,null,"224417","281241","11"],
["Florida","43414","51202","6146650","7573456","12"],
["Georgia","26807","37188","2972994","3686135","13"],
["Hawaii","1949","2609","379173","455868","15"],
["Idaho","19356","25525","484859","610872","16"],
["Illinois","25122","29643","3953690","4822046","17"],
["Indiana","12426","16905","2006774","2533270","18"],
["Iowa","8430","10459","993659","1247932","19"],
["Kansas","16089","20698","891380","1110407","20"],
["Kentucky","6366","10648","1327986","1717706","21"],
["Louisiana","19330","24818","1279749","1720801","22"],
["Maine","6174","7808","429112","531660","23"],
["Maryland","12413","14878","1882709","2194657","24"],
["Massachusetts","10605","11915","2205726","2579398","25"],
["Michigan","40105","49223","3125926","3884153","26"],
["Minnesota","43511","59804","1794312","2148725","27"],
["Mississippi","8330","12951","771082","1091245","28"],
["Missouri","21912","30041","1880742","2372190","29"],
["Montana","44607","63874","328132","416125","30"],
["Nebraska","11377","14982","609850","747562","31"],
["Nevada","27050","33485","853406","1055158","32"],
["New Hampshire",null,null,"449977","520643","33"],
["New Jersey","14845","19673","2691001","3194519","34"],
["New Mexico","98881","191708","559204","758364","35"],
["New York","54118","70792","5887560","7209054","36"],
["North Carolina","73688","117408","3065238","3882423","37"],
["North Dakota","25483","40263","256509","315134","38"],
["Ohio","13200","17343","3740362","4624669","39"],
["Oklahoma","212794","289042","1133908","1469342","40"],
["Oregon","34799","43415","1334347","1571678","41"],
["Pennsylvania","16550","21955","3972509","4937771","42"],
["Rhode Island","3209","5228","338143","408239","44"],
["South Carolina","13522","15715","1446247","1877887","45"],
["South Dakota","41337","73647","265584","334003","46"],
["Tennessee","13699","18638","1960747","2556332","47"],
["Texas","105497","131681","7680552","9535612","48"],
["Utah","19121","31053","805275","943147","49"],
["Vermont",null,null,"206792","254851","50"],
["Virginia","17293","22216","2603133","3120692","51"],
["Washington","73867","90547","2419750","2768076","53"],
["West Virginia",null,null,"535880","722125","54"],
["Wisconsin","38192","50139","1891731","2326998","55"],
["Wyoming","8613","12372","186140","223619","56"],
["Puerto Rico","5089","8082","716292","1208438","72"]]
```

A bit of division gives...


| NAME                 | B28009C_004E | B28009C_001E | B28002_004E | B28002_001E | Native Household % | All Households % | 
|----------------------|--------------|--------------|-------------|-------------|--------------------|------------------| 
| Alabama              | 20240        | 24269        | 1383347     | 1852518     | 83.4%              | 74.7%            | 
| Alaska               | 80490        | 104186       | 213002      | 248468      | 77.3%              | 85.7%            | 
| Arizona              | 161167       | 298774       | 2093778     | 2519052     | 53.9%              | 83.1%            | 
| Arkansas             | 14073        | 18250        | 810624      | 1142718     | 77.1%              | 70.9%            | 
| California           | 233630       | 281411       | 11055070    | 12944178    | 83.0%              | 85.4%            | 
| Colorado             | 41164        | 52766        | 1833549     | 2108992     | 78.0%              | 86.9%            | 
| Connecticut          | 8344         | 9639         | 1141859     | 1357269     | 86.6%              | 84.1%            | 
| Delaware             | 2869         | 4004         | 292600      | 351085      | 71.7%              | 83.3%            | 
| District of Columbia | 0            | 0            | 224417      | 281241      | 0.0%               | 79.8%            | 
| Florida              | 43414        | 51202        | 6146650     | 7573456     | 84.8%              | 81.2%            | 
| Georgia              | 26807        | 37188        | 2972994     | 3686135     | 72.1%              | 80.7%            | 
| Hawaii               | 1949         | 2609         | 379173      | 455868      | 74.7%              | 83.2%            | 
| Idaho                | 19356        | 25525        | 484859      | 610872      | 75.8%              | 79.4%            | 
| Illinois             | 25122        | 29643        | 3953690     | 4822046     | 84.7%              | 82.0%            | 
| Indiana              | 12426        | 16905        | 2006774     | 2533270     | 73.5%              | 79.2%            | 
| Iowa                 | 8430         | 10459        | 993659      | 1247932     | 80.6%              | 79.6%            | 
| Kansas               | 16089        | 20698        | 891380      | 1110407     | 77.7%              | 80.3%            | 
| Kentucky             | 6366         | 10648        | 1327986     | 1717706     | 59.8%              | 77.3%            | 
| Louisiana            | 19330        | 24818        | 1279749     | 1720801     | 77.9%              | 74.4%            | 
| Maine                | 6174         | 7808         | 429112      | 531660      | 79.1%              | 80.7%            | 
| Maryland             | 12413        | 14878        | 1882709     | 2194657     | 83.4%              | 85.8%            | 
| Massachusetts        | 10605        | 11915        | 2205726     | 2579398     | 89.0%              | 85.5%            | 
| Michigan             | 40105        | 49223        | 3125926     | 3884153     | 81.5%              | 80.5%            | 
| Minnesota            | 43511        | 59804        | 1794312     | 2148725     | 72.8%              | 83.5%            | 
| Mississippi          | 8330         | 12951        | 771082      | 1091245     | 64.3%              | 70.7%            | 
| Missouri             | 21912        | 30041        | 1880742     | 2372190     | 72.9%              | 79.3%            | 
| Montana              | 44607        | 63874        | 328132      | 416125      | 69.8%              | 78.9%            | 
| Nebraska             | 11377        | 14982        | 609850      | 747562      | 75.9%              | 81.6%            | 
| Nevada               | 27050        | 33485        | 853406      | 1055158     | 80.8%              | 80.9%            | 
| New Hampshire        | 0            | 0            | 449977      | 520643      | 0.0%               | 86.4%            | 
| New Jersey           | 14845        | 19673        | 2691001     | 3194519     | 75.5%              | 84.2%            | 
| New Mexico           | 98881        | 191708       | 559204      | 758364      | 51.6%              | 73.7%            | 
| New York             | 54118        | 70792        | 5887560     | 7209054     | 76.4%              | 81.7%            | 
| North Carolina       | 73688        | 117408       | 3065238     | 3882423     | 62.8%              | 79.0%            | 
| North Dakota         | 25483        | 40263        | 256509      | 315134      | 63.3%              | 81.4%            | 
| Ohio                 | 13200        | 17343        | 3740362     | 4624669     | 76.1%              | 80.9%            | 
| Oklahoma             | 212794       | 289042       | 1133908     | 1469342     | 73.6%              | 77.2%            | 
| Oregon               | 34799        | 43415        | 1334347     | 1571678     | 80.2%              | 84.9%            | 
| Pennsylvania         | 16550        | 21955        | 3972509     | 4937771     | 75.4%              | 80.5%            | 
| Rhode Island         | 3209         | 5228         | 338143      | 408239      | 61.4%              | 82.8%            | 
| South Carolina       | 13522        | 15715        | 1446247     | 1877887     | 86.0%              | 77.0%            | 
| South Dakota         | 41337        | 73647        | 265584      | 334003      | 56.1%              | 79.5%            | 
| Tennessee            | 13699        | 18638        | 1960747     | 2556332     | 73.5%              | 76.7%            | 
| Texas                | 105497       | 131681       | 7680552     | 9535612     | 80.1%              | 80.5%            | 
| Utah                 | 19121        | 31053        | 805275      | 943147      | 61.6%              | 85.4%            | 
| Vermont              | 0            | 0            | 206792      | 254851      | 0.0%               | 81.1%            | 
| Virginia             | 17293        | 22216        | 2603133     | 3120692     | 77.8%              | 83.4%            | 
| Washington           | 73867        | 90547        | 2419750     | 2768076     | 81.6%              | 87.4%            | 
| West Virginia        | 0            | 0            | 535880      | 722125      | 0.0%               | 74.2%            | 
| Wisconsin            | 38192        | 50139        | 1891731     | 2326998     | 76.2%              | 81.3%            | 
| Wyoming              | 8613         | 12372        | 186140      | 223619      | 69.6%              | 83.2%            | 
| Puerto Rico          | 5089         | 8082         | 716292      | 1208438     | 63.0%              | 59.3%            | 
|                      |              |              |             |             |                    |                  | 
| Average              |              |              |             |             | 68.5%              | 80.4%            | 


Glancing through the rows, it's clear that in most instances *the whole population is more web-connected than native populations*. However, there are some states where the inverse is true. Alabama, Arkansas, Connecticut, Florida, Illinois, Iowa, Louisiana, Massachusetts, Michigan, South Carolina, and Puerto Rico are the states where native households are more internet-connected. 

Why might this set of seemingly unrelated states share this property? 

The states with the highest native populations total — in order Alaska, Washington, North Carolina, Texas, New Mexico, Arizona, Oklahoma, California, New York, and South Dakota — have some of the highest discrepancies in web-access. Why might this be?

-----

Onwards to [this week's exercises](data.md).

