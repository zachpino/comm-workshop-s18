### Accessing the Census API

##### What is the Census and the American Community Survey?

The [US Census](https://en.wikipedia.org/wiki/United_States_Census) — an extraordinary resource for data scientists, policymakers, and social science researchers — is an attempt to collect information on every single person living within the boundaries of sovereign United States territory every ten years. It is called for by the Constitution of the United States, and has never been missed (even taking place during the United States Civil War ). Not only is the census vital for a better understanding of the makeup and condition of the United States, but it also serves as the official mechanism for drawing congressional and state goverment district boundaries — rendering the census a vital component of the United States political mechanism. Thousands of taxpayer-supported census workers campus the country, knock on doors, collect data, and ensure as accurate a count as possible.

Though an effort is made to deliver a wholistic and objective count with financial punishment for those who do not complete the census form ($100/household in 2010) and a promise of total confidentiality and indemnity, participation in the census is estimated at 74%, with some populations statistically underreporting. For instance, undocumented immigrant families are less likely to participate for fear of governmental reprisal. This skew has been modeled, and serves as a statistical adjustment in some of the census datasets which do not report raw numbers. Most census datasets, however, report nothing more than pure integer counts, and contextual offsets are left up to the data modeler. 

Historical census data, valuable and available, is tarnished by historical realities. The censuses of the early United States did not count women, people of color, or indigineous peoples, until the landmark census of 1850 — which was administered by the ahead-of-his-time sociopoltical activist and Civil War cartographer and strategist [Joseph C.G. Kennedy](https://en.wikipedia.org/wiki/Joseph_C._G._Kennedy). The census of 1940 was used surreptitiously to identify potential Italian, German, and Japanese sympathizers. The 2020 census is already being accused of similar potential misuse, and despite its importance, is under threat of defunding by both political sides.

Modeled on an Ancient Roman equivalent that tracked citizenry for military draft purposes (*censore* in Latin means *to determine value of something* ), the success of the US census has served as a model for similar efforts across the globe and supported by the United Nations. Many countries complete their own censuses, and provide them to citizens in a similar way to the United States model. 

Since the early aughts, the 10 year cadence of the census — clearly an outdated model in an era of constant data production and collection — has been supported by a motley assortment of supplemental data gathering efforts. One of the more successful attempts has been the American Community Survey, which aims to provide census-level details of a statistical sampling of the full American population at a higher frequency for large population centers. The ACS occurs once every year with a (relatively) small sample size (population centers of 65,000 individuals or greater), and every five years with a larger sampling (population centers of 20,000 individuals or greater).

The ACS tracks around 65,000 *variables*, and provides projections and estimates for another 20,000 or so. The data is voluminous, to say the least. Many of these indicators are aimed at constructing a picture of the United States' identity makeup — gender, race, ethnicity, derivation, age. Others are financial — income, employment status, employment industry, labor force participation. Further indicators support a better understanding of the American household — children/family, household size, number of rooms, rent/mortgage cost, frequency of housing changes, languages spoken at home. A large proportion of these variables have been tracked in the same way over many years, allowing data scientists and visualizers to track and understand the increasingly tumultuous social dynamics of the United States.

This course will provide walkthroughs for accessing this ACS data, cleaning and transforming it, combining it with other datasets, finding insights, using statistical tools for proving those insights, and rendering it visual through the D3 data visualization library.


##### Census API

The ACS are available online, along with an increasing number of historical census datasets, as an Application Programming Interface (API).  

	> An API is a formalized way of accessing complex and/or voluminous data-stores. Making a query to an API is termed 'calling' and API.

Some terminology: 

	> Data Store : Repository (physical of virtual) where data is located.
	> Data Set : An organized collection of related information
	> Data Point : A singular piece of encoded information

	>The Census API, a *data store*, offers a *data set* on uninsured people in each state, wherein we can find the data point for Illinois in 2016, which had an uninsured population of 71319 people under the age of 18.

Through the use of the Census API, very specific queries can be generated to access information at different geographic resolutions — from whole country tabulations to data bucketed for each state to county- and block-level raw counts.

The [Census API homepage](https://census.gov/developers/) offers a good sense of what is avaiable, though highly specific language is often used.

The [available APIs](https://census.gov/data/developers/data-sets.html) are also enumerated and you can find the ACS there, and [many exploratory tools](https://census.gov/data/data-tools.html) are provided.


##### API Key

The first step to accessing most APIs is to acquire an API cryptographic key.

	> A cryptographic key is a long, alphanumeric, random string that uniquely identifies each user.

Despite census data being fully public, API access is gated to prevent abuse and to anonymously track developers who access the repository. This tracking is benevolent, and helps the maintainers of the API know what is interesting to developers, and where their queries fail unexpectedly.

[Request an API Key](https://api.census.gov/data/key_signup.html), which will be sent to the email address you provide within 15 minutes or so. It may go to your spam folder.

Keep this 41 character string to yourself, and never share it online. Doing so could allow someone else to masquerade as you and hammer the Census API servers.

Make sure you copy the string somewhere so that it will be easily accessible.


##### Accessing the API

Let's compose a simple query of the ACS.

The [yearly ACS API](https://census.gov/data/developers/data-sets/acs-1year.html) offers many different way of learning about the data available within. The page lays out four main, confusingly named presentations of the underlying data.

	> Detail Tables : Actual raw datapoints, mostly pure counts, the most data at the highest specificity
	> Subject Tables : The raw data points scaled up and converted into population percentages and averages
	> Data Profile : Percentages and estimations of larger statistical trends derived from the data points
	> Comparison Profile: Shows changes over time for specific data points

The querying format is different for each type of presentation, though the process is similar. 

Underneath each presentation is an set of resources that looks something like this:

Detail Tables
- Example Call: api.census.gov/data/2016/acs/acs1?get=NAME,B01001_001E&for=state:*&key=...
- 2016 ACS Detail Table Variables [ html | xml | json ]
- ACS Technical Documentation
- Examples and Supported Geography

Selecting the [html](https://api.census.gov/data/2016/acs/acs1/variables.html) link will display a webpage listing all of the data dimensions available and is the best place to start browsing. On that linked page thousands of rows will display exactly what is avaiable.

| Name        | Label           | Concept  | Required | Attributes | Limit | Predicate Type | Group | Valid Value |
| :------     |:-------------   | :-----   | :------- |:---------  | :-----| :------------- |:------| :-----------|
B24121_014E    |   Estimate!! Total!!Industrial production managers	   |    DETAILED OCCUPATION BY MEDIAN EARNINGS IN THE PAST 12 MONTHS (IN 2016 INFLATION-ADJUSTED DOLLARS) FOR THE FULL-TIME, YEAR-ROUND CIVILIAN EMPLOYED POPULATION 16 YEARS AND OVER   |    not required    | B24121_014M, B24121_014EA   |   0   |   int   |   B24121   |   N/A

ff 

<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

	<script src="https://d3js.org/d3.v4.min.js"></script>

	<script>
/*
var dataset = [12,13,4,7,10,1];

var dataColors = [17,3,7,11,3,7]

width=500;
height=500;

barWidth=50;

var xAxis = 300;

var svg = d3.select('body').append('svg').attr('width', width).attr('height',height);

var background = d3.select('svg').append('rect').attr('width',width).attr('height',height).attr('fill',"#eee").attr('x',0).attr('y',0);

var drawAxis = d3.select('svg').append('line').attr('x1',0).attr('y1',xAxis).attr('x2',width).attr('y2',xAxis).attr('stroke','#000','stroke-width',3);


for (var i = 0; i < dataset.length; i++) {
//	console.log(dataset[i]);

	fill = dataColors[i];


	var bars = d3.select('svg').append('rect').attr('width',barWidth).attr('height', dataset[i]*10).attr('fill','#333').attr('x',i*(barWidth+20)+50).attr('y',xAxis-(dataset[i]*10)).attr('class','bars');

	var labels = d3.select('svg').append('text').text(i).attr('x',i*(barWidth+20)+50+(barWidth*.5)).attr('y',xAxis + 30).attr('class','labels').attr('font-family','courier');

	var values = d3.select('svg').append('text').text(dataset[i]).attr('x',i*(barWidth+20)+50+(barWidth*.45)).attr('y',xAxis-(dataset[i]*5)).attr('class','labels').attr('font-family','courier').attr('fill','#fff');
}

*/

/*

d3.csv('https://api.census.gov/data/2016/acs/acs1/profile?get=DP02_0070E&for=state:*&key=e0f41b3ce147e2d2ca2d7ee4085fbefd43c142a5', function(data){

	for (var i = 0; i < data.length; i++) {
		console.log(data[i]);
	}

})

*/



var dataset = [["4782529","01"],["718419","02"],["6824645","04"],["2934272","05"],["38763815","06"],["5447760","08"],["3525154","09"],["937935","10"],["670985","11"],["20294479","12"],["10120788","13"],["1378730","15"],["1662867","16"],["12620388","17"],["6534914","18"],["3091437","19"],["2850862","20"],["4354380","21"],["4577182","22"],["1317148","23"],["5918535","24"],["6736017","25"],["9818099","26"],["5462438","27"],["2924168","28"],["5977199","29"],["1027510","30"],["1877654","31"],["2905767","32"],["1316467","33"],["8837578","34"],["2046001","35"],["19505596","36"],["9957830","37"],["741486","38"],["11439848","39"],["3845697","40"],["4054353","41"],["12579422","42"],["1040259","44"],["4861188","45"],["848774","46"],["6546914","47"],["27386023","48"],["3024767","49"],["618622","50"],["8199576","51"],["7184110","53"],["1802572","54"],["5706681","55"],["576027","56"]];


var states = ["ALABAMA","ALASKA","ARIZONA","ARKANSAS","CALIFORNIA","COLORADO","CONNECTICUT","DELAWARE","DISTRICTOFCOLUMBIA","FLORIDA","GEORGIA","HAWAII","IDAHO","ILLINOIS","INDIANA","IOWA","KANSAS","KENTUCKY","LOUISIANA","MAINE","MARYLAND","MASSACHUSETTS","MICHIGAN","MINNESOTA","MISSISSIPPI","MISSOURI","MONTANA","NEBRASKA","NEVADA","NEW HAMPSHIRE","NEW JERSEY","NEW MEXICO","NEW YORK","NORTH CAROLINA","NORTH DAKOTA","OHIO","OKLAHOMA","OREGON","PENNSYLVANIA","PUERTO RICO","RHODE ISLAND","SOUTH CAROLINA","SOUTH DAKOTA","TENNESSEE","TEXAS","UTAH","VERMONT","VIRGINIA","WASHINGTON","WEST VIRGINIA","WISCONSIN","WYOMING"]

width=3000;
height=500;

barWidth=width/dataset.length;

var xAxis = 300;

var svg = d3.select('body').append('svg').attr('width', width).attr('height',height);

var background = d3.select('svg').append('rect').attr('width',width).attr('height',height).attr('fill',"#eee").attr('x',0).attr('y',0);

var drawAxis = d3.select('svg').append('line').attr('x1',0).attr('y1',xAxis).attr('x2',width).attr('y2',xAxis).attr('stroke','#000','stroke-width',3);


for (var i = 0; i < dataset.length; i++) {
//	console.log(dataset[i]);

if(i%2==0){labelPos = xAxis+30}
	else{labelPos = xAxis+60}

	fill = '#f00';
	console.log(dataset[i][0])

	var bars = d3.select('svg').append('rect').attr('width',barWidth).attr('height', parseInt((dataset[i][0])/100000)).attr('fill','#333').attr('x',i*barWidth).attr('y',xAxis-parseInt((dataset[i][0])/100000)).attr('class','bars');

	var labels = d3.select('svg').append('text').text(states[i]).attr('x',i*barWidth).attr('y',labelPos).attr('class','labels').attr('font-family','courier').style('font-size','10px');
}

</script>

</body>
</html>