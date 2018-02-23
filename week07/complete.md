### Complete Code

```html
<html>
<head>
	<style> 
	.axis{
		margin:10px; 
		padding:5px; 
		float:left;
		font-family:'courier';
		text-align:center;
		border:1px solid #333;
	}

	.switch{
		margin:10px; 
		clear:both; 
		background-color:#333;
		color:white;
		padding:20px;
		width:100px;
		cursor:hand;
	}
	
	.switch:hover {
		background-color:#999
	}
	
</style>
</head>

<body>

	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
	
	<div class="axis">X-AXIS
		<div class="switch" id='departX'>Departure Time</div> <div class="switch" id='lengthX'>Travel Time</div> <div class="switch" id='methodX'>Travel Method</div>
	</div>

	<div class="axis">Y-AXIS
		<div class="switch" id='departY'>Departure Time</div>	<div class="switch" id='lengthY'>Travel Time</div> <div class="switch" id='methodY'>Travel Method</div>
	</div>


	<script>

 var money = { "0101" : 32050, "0107" : 27745, "0103" : 19650, "0102" : 19000, "0106" : 18600, "0104" : 12901, "0105" : 6500, "0200" : 10250, "0402" : 127290, "0409" : 27010, "0407" : 8900, "0406" : 12100, "0405" : 8700, "0408" : 5400, "0404" : 5000, "0401" : 2193, "0403" : 5, "0502" : 27750, "0504" : 15777, "0501" : 10500, "0503" : 4400, "0603" : 72500, "0623" : 119300, "0645" : 60450, "0639" : 59900, "0649" : 57575, "0610" : 52695, "0622" : 35500, "0625" : 33150, "0629" : 32000, "0621" : 29495, "0646" : 25849, "0642" : 25600, "0630" : 25200, "0601" : 25000, "0615" : 24350, "0605" : 20000, "0618" : 18500, "0608" : 14750, "0614" : 13450, "0632" : 12500, "0602" : 11250, "0650" : 11000, "0647" : 1090, "0631" : 10750, "0636" : 10400, "0652" : 10010, "0616" : 10000, "0648" : 9900, "0612" : 9200, "0634" : 8500, "0626" : 8177, "0651" : 8000, "0638" : 7010, "0643" : 5000, "0624" : 2090, "0635" : 6500, "0613" : 6000, "0620" : 5500, "0633" : 5500, "0628" : 5000, "0644" : 2500, "0653" : 9870, "0606" : 5000, "0607" : 4136, "0611" : 3500, "0609" : 5200, "0619" : 1500, "0640" : 7820, "0641" : 3250, "0604" : 2675, "0601" : 2500, "0637" : 1500, "0627" : 1150, "0617" : 500, "0806" : 68895, "0802" : 40200, "0803" : 34575, "0804" : 29600, "0807" : 22000, "0805" : 14000, "0801" : 5500, "0901" : 14940, "0905" : 13350, "0902" : 5450, "0904" : 5000, "0903" : 4250, "1000" : 250, "1100" : 6000, "1198" : 2500, "1218" : 59452, "1226" : 43045, "1225" : 38965, "1216" : 36495, "1217" : 35000, "1207" : 33150, "1223" : 32175, "1212" : 31300, "1206" : 28035, "1227" : 13400, "1208" : 13245, "1221" : 11400, "1214" : 10100, "1222" : 9500, "1213" : 9500, "1220" : 8250, "1219" : 5750, "1215" : 4495, "1202" : 3600, "1224" : 3000, "1205" : 3000, "1204" : 3000, "1203" : 2800, "1201" : 2700, "1210" : 2500, "1211" : 1200, "1212" : 5000, "1209" : 1269, "1306" : 34000, "1312" : 23750, "1313" : 21100, "1301" : 20100, "1303" : 8100, "1304" : 10000, "1302" : 19500, "1311" : 18250, "1309" : 16800, "1308" : 14950, "1307" : 12500, "1305" : 11700, "1314" : 11200, "1310" : 9500, "6600" : 500, "1502" : 12594, "1501" : 11275, "1601" : 12000, "1602" : 11000, "1704" : 70300, "1715" : 68475, "1710" : 61395, "1706" : 53220, "1712" : 48250, "1713" : 43700, "1716" : 42550, "1717" : 31491, "1718" : 30000, "1702" : 22000, "1705" : 12600, "1701" : 12500, "1714" : 11000, "1703" : 10000, "1708" : 7795, "1711" : 7000, "1709" : 5500, "1707" : 5500, "1809" : 180900, "1802" : 51300, "1803" : 47626, "1805" : 47100, "1808" : 19000, "1804" : 18650, "1806" : 17500, "1807" : 7250, "1801" : 1500, "1902" : 25900, "1903" : 23000, "1901" : 19750, "1904" : 4000, "2003" : 40445, "2004" : 27700, "2002" : 24000, "2001" : 3800, "2106" : 47900, "2102" : 35700, "2105" : 12400, "2103" : 9500, "2104" : 6700, "2101" : 5500, "2201" : 71200, "2206" : 36750, "2204" : 33600, "2203" : 23700, "2202" : 22200, "2205" : 5000, "2302" : 71900, "2301" : 500, "2408" : 194325, "2405" : 41750, "2402" : 9750, "2401" : 8600, "2406" : 8000, "2404" : 7820, "2407" : 4250, "2403" : 20, "2502" : 1250, "2504" : 22750, "2509" : 8000, "2508" : 7250, "2501" : 6000, "2503" : 6000, "2505" : 4500, "2507" : 3800, "2506" : 3003, "2607" : 90795, "2606" : 72300, "2608" : 66050, "2614" : 65733, "2612" : 54300, "2610" : 40300, "2611" : 49050, "2604" : 33350, "2609" : 24000, "2603" : 20200, "2602" : 17700, "2613" : 15755, "2605" : 14980, "2601" : 14000, "2703" : 71500, "2706" : 22000, "2701" : 12660, "2708" : 11247, "2704" : 8000, "2705" : 4725, "2702" : 2000, "2707" : 1000, "2801" : 36500, "2802" : 21500, "2804" : 18200, "2803" : 13000, "2902" : 75300, "2907" : 46050, "2908" : 45850, "2906" : 43000, "2903" : 26700, "2904" : 14100, "2901" : 7500, "2905" : 2500, "3000" : 44495, "3103" : 25500, "3102" : 16650, "3101" : 5000, "3203" : 116101, "3204" : 40295, "3202" : 12700, "3201" : 2000, "3301" : 34250, "3302" : 14144, "3409" : 31011, "3402" : 29400, "3406" : 26499, "3404" : 15800, "3405" : 26350, "3407" : 24500, "3403" : 13550, "3401" : 12500, "3411" : 12300, "3412" : 8000, "3408" : 7500, "3410" : 6500, "3503" : 41500, "3502" : 21045, "3501" : 9000, "3624" : 38350, "3623" : 35505, "3621" : 27550, "3627" : 26630, "3614" : 19500, "3613" : 17000, "3615" : 14325, "3625" : 15100, "3626" : 14700, "3620" : 14500, "3604" : 14500, "3608" : 13000, "3611" : 12100, "3616" : 10200, "3606" : 10000, "3609" : 9500, "3602" : 6050, "3603" : 5750, "3601" : 4775, "3618" : 3007, "3619" : 2000, "3605" : 3000, "3610" : 2860, "3617" : 2500, "3622" : 2500, "3612" : 1000, "3607" : 250, "3708" : 69415, "3710" : 37600, "3709" : 34250, "3713" : 33037, "3707" : 26000, "3705" : 25800, "3701" : 22750, "3706" : 20080, "3702" : 16200, "3712" : 10000, "3703" : 6700, "3704" : 4000, "3711" : 2500, "3800" : 19750, "3912" : 62650, "3916" : 52350, "3902" : 44250, "3915" : 44150, "3906" : 42150, "3914" : 39600, "3901" : 39050, "3908" : 37050, "3913" : 33200, "3909" : 28999, "3905" : 25700, "3910" : 17400, "3907" : 17400, "3903" : 16300, "3911" : 13500, "3904" : 10500, "4002" : 52500, "4004" : 27400, "4001" : 18150, "4003" : 7000, "4005" : 5000, "4102" : 63850, "4105" : 26000, "4103" : 12500, "4104" : 10225, "4101" : 3500, "4203" : 71650, "4208" : 30000, "4209" : 57750, "4212" : 42450, "4215" : 32300, "4207" : 29400, "4210" : 28400, "4213" : 24500, "4206" : 23800, "4218" : 23800, "4204" : 18500, "4205" : 17750, "4214" : 17500, "4211" : 17266, "4217" : 14400, "4201" : 10000, "4216" : 7000, "4202" : 3000, "4401" : 6000, "4402" : 750, "4502" : 29000, "4506" : 26000, "4501" : 25300, "4507" : 15750, "4504" : 14050, "4505" : 13750, "4503" : 4100, "4600" : 27365, "4701" : 18500, "4707" : 71100, "4706" : 49250, "4703" : 29700, "4709" : 26000, "4704" : 18700, "4705" : 12250, "4702" : 10000, "4708" : 8400, "4825" : 147245, "4823" : 76395, "4822" : 64895, "4803" : 52500, "4805" : 50150, "4826" : 48000, "4808" : 47000, "4832" : 44100, "4817" : 43400, "4828" : 43345, "4810" : 42600, "4829" : 40500, "4821" : 39250, "4833" : 35800, "4806" : 35600, "4836" : 30300, "4831" : 30300, "4824" : 29150, "4807" : 28700, "4812" : 27850, "4827" : 24200, "4820" : 21000, "4802" : 20700, "4834" : 20600, "4813" : 17475, "4811" : 15050, "4816" : 14845, "4804" : 12500, "4830" : 11000, "4835" : 7000, "4814" : 6500, "4809" : 4000, "4801" : 3200, "4818" : 3000, "4815" : 2500, "4819" : 2000, "4904" : 31855, "4903" : 30550, "4902" : 16300, "4901" : 11500, "5000" : 8500, "7800" : 500, "5108" : 101157, "5110" : 64645, "5102" : 30600, "5106" : 30150, "5104" : 27100, "5111" : 26500, "5107" : 24550, "5109" : 14000, "5101" : 9800, "5103" : 4500, "5105" : 1000, "5305" : 36200, "5309" : 1750, "5308" : 25050, "5306" : 22750, "5303" : 16750, "5304" : 16700, "5301" : 13640, "5310" : 7620, "5310" : 8750, "5302" : 7500, "5307" : 2500, "5403" : 35250, "5402" : 27950, "5401" : 18000, "5501" : 291164, "5507" : 31200, "5503" : 30000, "5506" : 12500, "5508" : 7700, "5505" : 4500, "5504" : 3500, "5502" : 1000, "5600" : 103102, "7298" : 0
};


		//variables for svg container
		var width = 1200;
		var height = 1200;

		// reusable value for uniform margins
		var margin = 75;
		var counter = 0;
		//create svg container
		var svg = d3.select('body')
		.append('svg')
		.attr('width', width)
		.attr('height', height)
		;

		//draw a background rectangle 
		var background = d3.select('svg')
		.append('rect')
		.attr('width', width)
		.attr('height', height)
		.attr('x',0)
		.attr('y',0)
		.attr('fill','#333')
		;

		//draw a horizontal line
		var xAxis = d3.select('svg')
		.append('line')
		.attr('x1' , margin)
		.attr('x2' , width - margin)
		.attr('y1' , height/2)
		.attr('y2' , height/2)
		.attr('stroke' , '#ccc')
		.attr('stroke-width' , '2px')
		;

		//draw a vertical line
		var yAxis = d3.select('svg')
		.append('line')
		.attr('x1' , width/2)
		.attr('x2' , width/2)
		.attr('y1' , margin)
		.attr('y2' , height - margin)
		.attr('stroke' , '#ccc')
		.attr('stroke-width' , '2px')
		;

		//draw x r label
		var xRightLabel = d3.select('svg')
		.append('text')
		.text('drive')
		.attr('x' , width - margin/1.5)
		.attr('y' , height/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','xRight')

		;

		//draw x l label
		var xLeftLabel = d3.select('svg')
		.append('text')
		.text('public')
		.attr('x' , 10)
		.attr('y' , height/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','xLeft')
		;



		//draw y top label
		var yTopLabel = d3.select('svg')
		.append('text')
		.text('long')
		.attr('x' , width/2 -20)
		.attr('y' , margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','yTop')
		;

		//draw y bottom label
		var yBottomLabel = d3.select('svg')
		.append('text')
		.text('short')
		.attr('x' , width/2 - 20)
		.attr('y' , height- margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','yBottom')
		;

		//draw key
		var key = d3.select('svg')
		.append('text')
		.text('')
		.attr('x' , margin/2)
		.attr('y' , margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','key')
		;


		d3.text("https://api.census.gov/data/2015/acs/acs5?get=NAME,B08006_003E,B08006_008E,B08006_014E,B08006_015E,B08006_016E,B08006_017E,B08006_004E,B08012_002E,B08012_003E,B08012_004E,B08012_005E,B08012_006E,B08012_007E,B08012_008E,B08012_009E,B08012_010E,B08012_011E,B08012_012E,B08012_013E,B08011_002E,B08011_003E,B08011_004E,B08011_005E,B08011_006E,B08011_007E,B08011_008E,B08011_009E,B08011_010E,B08011_011E,B08011_012E,B08011_013E,B08011_014E&for=congressional%20district", function(data) {
			var e = data.replace(/[\[\]]+/g,'')

			var dataset = d3.csvParse(e, function(d){


				var publicTotal = parseInt(d.B08006_008E) + parseInt(d.B08006_014E) + parseInt(d.B08006_015E) + parseInt(d.B08006_016E) + parseInt(d.B08006_017E) + parseInt(d.B08006_004E);

				var driveTotal = parseInt(d.B08006_003E);

				var total = driveTotal + publicTotal;

				var shortTravel = parseInt(d.B08012_002E) + parseInt(d.B08012_003E) + parseInt(d.B08012_004E) + parseInt(d.B08012_005E) + parseInt(d.B08012_006E) + parseInt(d.B08012_007E) ;

				var longTravel = parseInt(d.B08012_008E) + parseInt(d.B08012_009E) + parseInt(d.B08012_010E) + parseInt(d.B08012_011E) + parseInt(d.B08012_012E) + parseInt(d.B08012_013E) ;

				var travelTotal = shortTravel + longTravel;

				var earlyDepart = parseInt(d.B08011_002E) + parseInt(d.B08011_003E) + parseInt(d.B08011_004E) + parseInt(d.B08011_005E) + parseInt(d.B08011_006E) + parseInt(d.B08011_007E);

				var lateDepart = parseInt(d.B08011_008E) + parseInt(d.B08011_009E) + parseInt(d.B08011_010E) + parseInt(d.B08011_011E) + parseInt(d.B08011_012E) + parseInt(d.B08011_013E);


				var departTotal = earlyDepart + lateDepart;

				var congressCode = d.state + d["congressional district"];

				return {
					name: d.NAME,
					total: total,
					drive: driveTotal,
					public: publicTotal,
					driveParameter: driveTotal / total ,
					publicParameter: publicTotal / total,
					short: shortTravel,
					long: longTravel,
					shortParameter: shortTravel / travelTotal,
					longParameter: longTravel / travelTotal,
					early: earlyDepart,
					late: lateDepart,
					earlyParameter: earlyDepart / departTotal,
					lateParameter: lateDepart / departTotal,
					fips: d.state,
					district: d["congressional district"],
					districtMoney: money[congressCode]
				};
			});

			


			var xScale = d3.scaleLinear().domain([-1,1]).range([margin,width-margin]);
			var yScale = d3.scaleLinear().domain([-1,1]).range([margin, height-margin]);

			var moneyScale = d3.scaleLinear().domain([0,300000]).range([7,40]);
			var colorScale = d3.scaleLinear().domain([-1,1]).range([0,1]);

			var dots = d3.select('svg')
			.selectAll('.dots')
			.data(dataset)
			.enter()
			.append('circle')
			.attr('cx', function(d){
				return xScale(d.driveParameter - d.publicParameter);
			})
			.attr('cy', function(d){
				return yScale(d.longParameter - d.shortParameter);
			})		 					
			.attr('r', function(d){

				return moneyScale(d.districtMoney); 
			})
			.attr('stroke','white')
			.style('stroke-width',0)
			.attr('opacity',.5)
			.attr('class', 'dots')
			.attr('fill', function(d){
				return d3.interpolatePlasma(colorScale(d.longParameter - d.shortParameter));
				//return '#f2844b'

			})
			.on('mouseover', function(d) {
				d3.select('#key').text(d.name);
				console.log(d);
				d3.select(this).transition().ease(d3.easeBounce).duration(750).style('stroke-width',5).attr('opacity',1);

			})

			.on('mouseout', function(d) {
				d3.select('#key').text('');

				d3.select(this).transition().duration(500).style('stroke-width',0).attr('opacity',.5);
			})



			d3.select('#departX')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cx',function(d){
						return xScale(d.lateParameter - d.earlyParameter);
					})

					d3.select('#xLeft').text('early')
					d3.select('#xRight').text('late')
				})
			;

			d3.select('#lengthX')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cx',function(d){
						return xScale(d.longParameter - d.shortParameter);
					})

					d3.select('#xLeft').text('short')
					d3.select('#xRight').text('long')
				})
			;

			d3.select('#methodX')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cx',function(d){
						return xScale(d.driveParameter - d.publicParameter);					
					})

					d3.select('#xLeft').text('public')
					d3.select('#xRight').text('drive')
				})
			;



			d3.select('#departY')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cy',function(d){
						return yScale(d.lateParameter - d.earlyParameter);
					})
					.attr('fill', function(d){
						return d3.interpolatePlasma(colorScale(d.lateParameter - d.earlyParameter))
					})
			;


					d3.select('#yTop').text('early')
					d3.select('#yBottom').text('late')
				})
			;

			d3.select('#lengthY')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cy',function(d){
						return yScale(d.longParameter - d.shortParameter);
					})
					.attr('fill', function(d){
						return d3.interpolatePlasma(colorScale(d.longParameter - d.shortParameter))
					})
			;

					d3.select('#yTop').text('short')
					d3.select('#yBottom').text('long')
				})
			;

			d3.select('#methodY')
				.on('click', function(d){ 
				
					d3.selectAll('.dots')
					.transition()
					.duration(1500)
					.attr('cy',function(d){
						return yScale(d.driveParameter - d.publicParameter);					
					})
					.attr('fill', function(d){
						return d3.interpolatePlasma(colorScale(d.driveParameter - d.publicParameter))
					})
			;


					d3.select('#yTop').text('public')
					d3.select('#yBottom').text('drive')
				})
			;
		
	});





	</script>

</body>
</html>
```