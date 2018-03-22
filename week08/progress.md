### Complete Code

```html
<!DOCTYPE html>
<html>
<head>
	<title>Degree Types</title>
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
			cursor:pointer;
		}
 
	</style>
</head>
<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>

	<div class="buttonContainer">
		<div id='total' class="switch">All Bachelors' Degrees</div>
		<div id='compMathStat' class="switch">Computer Science, Mathematics, Statistics</div>
		<div id='visualPerformingArts' class="switch">Visual+Performing Arts</div>
		<div id='socialSci' class="switch">Social Sciences</div>
	</div>

	<script>
		var width = 1200;
		var height = width / 2;
		var xMargin = 20;
		var yMargin = 80;

		var svg = d3.select('body')
			.append('svg')
			.attr('height', height)
			.attr('width', width)
		;

		//background of svg container
		var background = d3.select('body')
			.select('svg')
			.append('rect')
			.attr('x',0)
			.attr('y',0)
			.attr('width',width)
			.attr('height',height)
			.attr('fill',"#d3d3d3")
		;

		d3.text('https://api.census.gov/data/2016/acs/acs1?get=NAME,B15010_001E,B15010_002E,B15010_014E,B15010_006E&for=state:*', function(census){

			var noBrackets = census.replace(/[\[\]]+/g,'');

			var censusDataset = d3.csvParse(noBrackets, function(d){
				return {
					name: d.NAME,
					total: parseInt(d.B15010_001E),
					compMathStat: parseInt(d.B15010_002E),
					visualPerformingArts: parseInt(d.B15010_014E),
					socialSci: parseInt(d.B15010_006E)
				}
			});
			//console.log(censusDataset)

			var barWidth = (width - xMargin*2) / censusDataset.length;

			var bars = d3.select('svg')
	    		.selectAll('.bars')
	    		.data(censusDataset)
	    		.enter()
	    		.append('rect')
	    		.attr('class','bars')
	    		.attr('x', function(d,i){return (i * barWidth) + xMargin})
	    		.attr('y', function(d){
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);
	    			return height - yScale(d.total) - yMargin;
	    		})
	    		.attr('width', barWidth)
	    		.attr('height', function(d){
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);
	    			return yScale(d.total);
	    		})
	    		.attr('fill', function(d){
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d.total;
	    			})
	    			var colorScale = d3.scaleLinear().domain(extents).range([0,1]);
	    			return d3.interpolateWarm(colorScale(d.total));
	    		})

	    		d3.select('body')
	    			.selectAll('.switch')
	    			.on('click', function(d){
	    				d3.selectAll('.switch').style('background-color','#333')
	    				d3.select(this).style('background-color','red')

	    				var topic = this.id;
	    				update(topic);
	    			})

			function update(dataPoint){

				d3.select('body')
					.selectAll('.bars')
					.data(censusDataset)
					.transition()
					.duration(1000)
					.ease(d3.easeElastic)
					.attr('y', function(d){
	    			var extents = d3.extent(censusDataset, function(d){
	    				return d[dataPoint];
	    			})
	    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);
	    			return height - yScale(d[dataPoint]) - yMargin;
		    		})
		    		.attr('height', function(d){
		    			var extents = d3.extent(censusDataset, function(d){
		    				return d[dataPoint];
		    			})
		    			var yScale = d3.scaleLinear().domain(extents).range([yMargin, height - yMargin*2]);
		    			return yScale(d[dataPoint]);
		    		})
		    		.attr('fill', function(d){
		    			var extents = d3.extent(censusDataset, function(d){
		    				return d[dataPoint];
		    			})
		    			var colorScale = d3.scaleLinear().domain(extents).range([0,1]);
		    			return d3.interpolateWarm(colorScale(d[dataPoint]));
		    		})
			}
		})


	</script>


</body>
</html>

```