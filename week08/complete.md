### Complete Code

```html
<html>
<head>
	<style>
		
		.switch{
			font-size:9px;
			display:inline-block;
			font-family:courier; 
			margin-bottom: 3px; 
			margin-right: 3px; 
			padding:5px; 
			color:white; 
			background-color:#333;
			text-align: center;
			cursor: pointer;
		}

		.labels{
			font-size:9px;
			font-family:courier; 
		}

		.buttonContainer{
			width:1200px;
			margin-bottom:3px;}

		#legend{
			font-size:12px;
			font-family:courier; 
			background-color:red;
		}

	</style>

	<title>
		Bachelor Degrees by Area by State
	</title>

</head>

<body>	
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>

	<div class="buttonContainer">
		<div id="total" class="switch"> All Bachelors Degrees </div> 
		<div id="compMathStat" class="switch"> Computer Science, Mathematics, Statistics </div> 
		<div id="bioAgriEnviro" class="switch"> Biology, Agriculture, Environmental Sciences </div> 
		<div id="physSci" class="switch"> Physical Sciences </div> 
		<div id="psych" class="switch"> Psychology </div> 
		<div id="socialSci" class="switch"> Social Sciences </div> 
		<div id="multiSci" class="switch"> Multiple Sciences </div> 	
		<div id="engineering" class="switch"> Engineering </div> 
		<div id="business" class="switch"> Business </div> 
		<div id="education" class="switch"> Education </div> 
		<div id="litLang" class="switch"> Literature and Languages </div> 
		<div id="libArtsHistory" class="switch"> Liberal Arts and History </div> 
		<div id="visualPerformingArts" class="switch"> Visual and Performing Arts </div> 
		<div id="comm" class="switch"> Communications </div> 	
		<div id="otherArts" class="switch"> Other Liberal Arts </div>	
	</div>

	<script>

		//display variables
		var width = 1200;
		var height = 600;
		var xMargin = 50;
		var yMargin = 80;

		//make an svg container
		var svg = d3.select('body')
			.append('svg')
			.attr('height',height)
			.attr('width',width)
		;

		//rectangular background 
		var background = d3.select('body')
			.select('svg')
			.append('rect')
			.attr('x',0)
			.attr('y',0)
			.attr('width',width)
			.attr('height',height)
			.attr('fill','#eee')
		;

		//ask census for data
	    d3.text('https://api.census.gov/data/2016/acs/acs1?get=NAME,B15010_001E,B15010_002E,B15010_003E,B15010_004E,B15010_005E,B15010_006E,B15010_007E,B15010_008E,B15010_009E,B15010_010E,B15010_011E,B15010_012E,B15010_013E,B15010_014E,B15010_015E,B15010_016E&for=state:*',function(census){

	    	//remove brackets from census
	    	var noBrackets = census.replace(/[\[\]]+/g,'')

	    	//convert census into usable js object with necessary values precomputed
	    	var censusDataset = d3.csvParse(noBrackets, function(d){
				return {
					name: d.NAME,
					total: parseInt(d.B15010_001E),
					compMathStat: parseInt(d.B15010_002E),
					bioAgriEnviro: parseInt(d.B15010_003E),
					physSci: parseInt(d.B15010_004E),
					psych: parseInt(d.B15010_005E),
					socialSci: parseInt(d.B15010_006E),
					engineering: parseInt(d.B15010_007E),
					multiSci: parseInt(d.B15010_008E),
					business: parseInt(d.B15010_010E),
					education: parseInt(d.B15010_011E),
					litLang: parseInt(d.B15010_012E),
					libArtsHistory: parseInt(d.B15010_013E),
					visualPerformingArts: parseInt(d.B15010_014E),
					comm: parseInt(d.B15010_015E),
					otherArts: parseInt(d.B15010_016E)
	        	};
	    	});

	    	//console.log(censusDataset);

	    	//calculate width for each bar element
	    	var barWidth = ( width - (2*xMargin) ) / censusDataset.length;

	    	//draw bars in their default position, based on total degree holders
	    	var bars = d3.select('svg')
	    		.selectAll('bars')
	    		.data(censusDataset)
	    		.enter()
	    		.append('rect')
	    		.attr('class','bars')
	    		.attr('x', function(d,i){return (i * barWidth) + xMargin})
	    		.attr('y', function(d){
	    			//find high and low value
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			//scale to pixels
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);

	    			return height - yScale(d.total) - yMargin;

	    		})
	    		.attr('width', barWidth)
	    		.attr('height', function(d){
	    			//find high and low value
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			//scale to pixels
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);
	    			
	    			return yScale(d.total);

	    		})
	    		.attr('stroke','white')
	    		.attr('stroke-width','0')
	    		.attr('fill', function(d){
	    			//find high and low value
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			//scale for chromatic color fills
	    			var colorScale = d3.scaleLinear().domain(extents).range([0,1]);

	    			return d3.interpolateWarm(colorScale(d.total));
	    		})
	    		.on('mouseover',function(d,i){
	    			//find high and low value
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d[topic];
	    			})
	    			//scale to pixels
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);

	    			//find the moused-over object, and add a stroke to it
	    			d3.select(this).transition().duration(750).attr('stroke-width','3')

	    			//find the legend text object, change its content, and move it to the moused-over bar
	    			d3.select('#legend')
	    				.transition()
	    				.text(d.name + ": " + d[topic].toLocaleString() + " Degree Holders")
	    				.attr('x',(i*barWidth)+xMargin)
	    				.attr('y', height - yScale(d[topic]) - yMargin - 10)
	    			;
	    		})
	    		.on('mouseout',function(d){
	    			//remove stroke
	    			d3.select(this).transition().duration(500).attr('stroke-width','0')
	    			
	    			//remove text from legend
	    			d3.select('#legend').text('')
	    		})
	    	;

	    	//draw text labels underneath bars
	    	var labels = d3.select('svg')
	    		.selectAll('labels')
	    		.data(censusDataset)
	    		.enter()
	    		.append('text')
	    		.attr('class','labels')
	    		.attr('x', function(d,i){return (i * barWidth) + xMargin + (barWidth*.5)})
	    		.attr('y', height - (yMargin*.85))
	    		.text(function(d){
	    			//fix for long names
	    			if(d.name == "District of Columbia"){d.name = "DC"}
	    			return d.name
	    		})
	 			//rotate text, using an attribute of this format: rotate(angle,centerRotationX,centerRotationY)
	    		.attr('transform', function(d,i){
	    			return 'rotate(45 ' + ( (i * barWidth) + xMargin + (barWidth*.5)) + " " + (height - (yMargin*.85)) + ')'   
	    		})
	    	;

	    	//space to show mouseover text
			var legend = d3.select('body')
			.select('svg')
			.append('text')
			.attr('id','legend')
			.text('')
			;

			//ensure that, if the user hasn't selected anything, at default we show the 'total' variable
			var topic = "total";
			d3.select("#total").style('background-color', '#A147AD');

			//when the user clicks one of the switches, change the data
		    d3.select('body')
		    	.selectAll('.switch')
		    	.on('click', function(d){
		    		//reset all buttons
		    		d3.selectAll('.switch').style('background-color', '#333')

		    		//make the background of selected button a different color
		    		d3.select(this).style('background-color', '#A147AD')
		    		
		    		//change topic variable to hold the data that the user wants to see
		    		topic = this.id;

		    		//run the update routine
		    		update(this.id);
		    	})


		    //define reusable update routine for when users want a data switch
			function update(dataPoint){

				//find all the bars
				d3.select('body')
					.selectAll('.bars')
					.data(censusDataset)
					.transition()
					.duration(1000)
					//update the y, fill, and height attributes
					.attr('y', function(d){
	    				//find high and low value
		    			var extents = d3.extent(censusDataset, function(d){
		    				return d[dataPoint];
		    			})

		    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);

		    			return height - yScale(d[dataPoint]) - yMargin;

		    		})
		    		.attr('height', function(d){
	    				//find high and low value
		    			var extents = d3.extent(censusDataset, function(d){
		    				return d[dataPoint];
		    			})
	    				//scale to pixels
		    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);

		    			return yScale(d[dataPoint]);

		    		})
		    		.attr('fill', function(d){
	    				//find high and low value
		    			var extents = d3.extent(censusDataset, function(d){
		    				return d[dataPoint];
		    			})
	    				//scale to pixels
		    			var colorScale = d3.scaleLinear().domain(extents).range([0,1]);

		    			return d3.interpolateWarm(colorScale(d[dataPoint]));
		    		})
		    	;
			}
		})

	</script>
</body>
</html>

```