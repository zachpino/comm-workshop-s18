### Complete Code

```html
<html>
<head>
	<style> 
	#switch{background-color:#333;color:white;padding:20;width:100;text-align:center;font-family:'courier';cursor:hand;}
	#swtich:hover{}
</style>
</head>

<body>

	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
	<div id='switch'>Switch Dataset</div>


	<script>

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
		.attr('x' , width - margin/1.3)
		.attr('y' , height/2 + 3)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','xRight')
		;

		//draw x l label
		var xLeftLabel = d3.select('svg')
		.append('text')
		.text('public')
		.attr('x' , margin/6)
		.attr('y' , height/2 + 3)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','xLeft')
		;



		//draw y top label
		var yTopLabel = d3.select('svg')
		.append('text')
		.text('early commute')
		.attr('x' , width/2 - 57)
		.attr('y' , margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','yTop')
		;

		//draw y bottom label
		var yBottomLabel = d3.select('svg')
		.append('text')
		.text('late commute')
		.attr('x' , width/2 - 53)
		.attr('y' , height - margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','yBottom')
		;

		//draw key
		var key = d3.select('svg')
		.append('text')
		.text('district')
		.attr('x' , margin/2)
		.attr('y' , margin/2)
		.attr('font-family' , 'courier')
		.attr('font-size' , '14px')
		.attr('fill','white')
		.attr('id','key')
		;

		//query ACS
		d3.text("https://api.census.gov/data/2015/acs/acs5?get=NAME,B08006_003E,B08006_008E,B08006_014E,B08006_015E,B08006_016E,B08006_017E,B08006_004E,B08012_002E,B08012_003E,B08012_004E,B08012_005E,B08012_006E,B08012_007E,B08012_008E,B08012_009E,B08012_010E,B08012_011E,B08012_012E,B08012_013E,B08011_002E,B08011_003E,B08011_004E,B08011_005E,B08011_006E,B08011_007E,B08011_008E,B08011_009E,B08011_010E,B08011_011E,B08011_012E,B08011_013E,B08011_014E&for=congressional%20district", function(censusData) {
			
			//remove annoying brackets
			var noBracketsData = censusData.replace(/[\[\]]+/g,'')

			//parse the data based on csv logic
			var dataset = d3.csvParse(noBracketsData, function(d){

				//add up all applicable methods of public transit: bikes, walking, train, bus...
				var publicTotal = parseInt(d.B08006_008E) + parseInt(d.B08006_014E) + parseInt(d.B08006_015E) + parseInt(d.B08006_016E) + parseInt(d.B08006_017E) + parseInt(d.B08006_004E);

				//single drivers
				var driveTotal = parseInt(d.B08006_003E);

				//all commuters
				var commuteTotal = driveTotal + publicTotal;



				//commuters with commutes less than 30 minutes 
				var shortTravel = parseInt(d.B08012_002E) + parseInt(d.B08012_003E) + parseInt(d.B08012_004E) + parseInt(d.B08012_005E) + parseInt(d.B08012_006E) + parseInt(d.B08012_007E) ;

				//commuters with commutes more than 30 minutes 
				var longTravel = parseInt(d.B08012_008E) + parseInt(d.B08012_009E) + parseInt(d.B08012_010E) + parseInt(d.B08012_011E) + parseInt(d.B08012_012E) + parseInt(d.B08012_013E) ;

				//all people commuting as reported by travel duration
				var travelTotal = shortTravel + longTravel;



				//commuters who leave before 7:30am
				var earlyDepart = parseInt(d.B08011_002E) + parseInt(d.B08011_003E) + parseInt(d.B08011_004E) + parseInt(d.B08011_005E) + parseInt(d.B08011_006E) + parseInt(d.B08011_007E);

				//commuters who leave after 7:30am
				var lateDepart = parseInt(d.B08011_008E) + parseInt(d.B08011_009E) + parseInt(d.B08011_010E) + parseInt(d.B08011_011E) + parseInt(d.B08011_012E) + parseInt(d.B08011_013E);

				//all people commuting as reported by time of departure
				var departTotal = earlyDepart + lateDepart;

				return {
					name: d.NAME,
					
					drive: driveTotal,
					public: publicTotal,
					driveParameter: driveTotal / commuteTotal ,
					publicParameter: publicTotal / commuteTotal,
					
					short: shortTravel,
					long: longTravel,
					shortParameter: shortTravel / travelTotal,
					longParameter: longTravel / travelTotal,
					
					early: earlyDepart,
					late: lateDepart,
					earlyParameter: earlyDepart / departTotal,
					lateParameter: lateDepart / departTotal,
					
					fips: d.state,
					district: d["congressional district"]
				};
			});

			//scales for each axis, parameterized (percentage-based) domains
			var xScale = d3.scaleLinear().domain([-1,1]).range([margin,width-margin])
			var yScale = d3.scaleLinear().domain([-1,1]).range([margin,height-margin])

console.log(dataset);




			//scale to be used later for color mapping
			var colorScale = d3.scaleLinear().domain([-1,1]).range([1,0])

			//find the svg container
			var dots = d3.select('svg')
			//look for a set of objects that aren't there yet
			.selectAll('.dots')
			//as d3 to compare that selection with a dataset
			.data(dataset)
			//for each item in the dataset unmatched by a selected element...
			.enter()
			//add a circle
			.append('circle')
			//place the circle at the scaled position on x
			.attr('cx', function(d){
				return xScale(d.driveParameter - d.publicParameter)
			})
			//place the circle at the scaled position on y (be careful to not invert it!)
			.attr('cy', function(d){
						return yScale(d.lateParameter - d.earlyParameter);
			})		
			//radius of circles 					
			.attr('r',5)
			//default stylings
			.attr('stroke','white')
			.style('stroke-width',0)
			.attr('opacity',.5)
			//label them so we can find them later
			.attr('class', 'dots')
			//fill color, soon to be expanded
			.attr('fill', '#f2844b')
			//this object should respond to mouse hovering
						//this object should respond to mouse hovering
			.on('mouseover', function(d) {
				
				//look for an element with id name key and erase its text	
				d3.select('#key')
				//set the text of the key element to the name property of the dot
				.text(d.name);

				//'this' is a keyword that refers to the object that detected the event
				//select the rolled over dot
				d3.select(this)
				//turn on animation	
				.transition()
				//bounce animation
				.ease(d3.easeBounce)
				//animate over 1 second
				.duration(1000)
				//increase stroke width
				.style('stroke-width',5)
				//increase radius
				.attr('r',20)
				//increase opacity
				.attr('opacity',1);
		
			})
			//this object should respond to mouse moving away from it
			.on('mouseout', function(d) {

				//look for an element with id name key and set its text	back to default
				d3.select('#key').text('district');

				//reverse of the mouseover, without the fancy animation
				d3.select(this)
				.transition()
				.style('stroke-width',0)
				.attr('r',5)
				.attr('opacity',.5);
			})
		;
		});

	</script>

</body>
</html>
```
