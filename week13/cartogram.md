### Cartogram

Sometimes, we want to visualize data that is meaningfully spatial or regional, but we want to flatten the geographic differences between entities. Any visualization where geographic data is shown on a *manipulated* version of geography is called a **cartogram**.

For example, if we wanted to plot data about what percentage of the population worked from home in each state, it might be important to see regional trends. But, we also might want to have Rhode Island and Washington DC be just as visible as California for easier comparison since the actual geographic forms themselves don't matter as much, and might obfuscate the data.

![cartogram](cartogram.png)

This simplified version of geography makes it easier to compare all the states at a glance, as well as discover geospatial trends since the states are plotted in a matrix spot approximate to their real locations.

Cartograms can be much more expressive than this simple matrix approach, [specifically adjusting the space alloted to each entity](https://medium.com/google-news-lab/tilegrams-make-your-own-cartogram-hexmaps-with-our-new-tool-df46894eeec1) or even [distorting the actual shape of the geo-entity with data](http://archive.worldmapper.org/thumbnails/mapindex1-12.html)!

-----

This code draws circles or squares for each state based on a JSON array that includes simple cartesian coordinate positions. It's really hard to fit the states into a grid -- try to adjust the coordinates to change the layout -- it's a great design exercise! 

```html
<html>
<head>
	<title>
		Cartogram 
	</title>

</head>

<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>

	<script>

		//display variables
		var width = 800;
		var height = width * (9 / 13);
		//the cartogram is a 9x13 grid, so we can get perfect proportions if we calculate the aspect ratio

		//make an svg container for map
		var svg = d3.select('body')
			.append('svg')
			.attr('height',height)
			.attr('width',width)
		;

		//rectangular background for map svg
		var background = svg
			.append('rect')
			.attr('x',0)
			.attr('y',0)
			.attr('width',width)
			.attr('height',height)
			.attr('fill','black')
		;

		var cartogram = [
				{"state":"Alabama","short":"AL","fips":"01","x":6,"y":5},
				{"state":"Alaska","short":"AK","fips":"02","x":0,"y":8},
				{"state":"Arizona","short":"AZ","fips":"04","x":1,"y":4},
				{"state":"Arkansas","short":"AR","fips":"05","x":4,"y":4},
				{"state":"California","short":"CA","fips":"06","x":0,"y":3},
				{"state":"Colorado","short":"CO","fips":"08","x":2,"y":3},
				{"state":"Connecticut","short":"CT","fips":"09","x":10,"y":3},
				{"state":"Delaware","short":"DE","fips":"10","x":10,"y":4},
				{"state":"Washington, District of Columbia","short":"DC","fips":"11","x":9,"y":5},
				{"state":"Florida","short":"FL","fips":"12","x":9,"y":7},
				{"state":"Georgia","short":"GA","fips":"13","x":7,"y":5},
				{"state":"Hawaii","short":"HI","fips":"15","x":1,"y":8},
				{"state":"Idaho","short":"ID","fips":"16","x":1,"y":1},
				{"state":"Illinois","short":"IL","fips":"17","x":5,"y":3},
				{"state":"Indiana","short":"IN","fips":"18","x":6,"y":3},
				{"state":"Iowa","short":"IA","fips":"19","x":4,"y":2},
				{"state":"Kansas","short":"KS","fips":"20","x":3,"y":4},
				{"state":"Kentucky","short":"KY","fips":"21","x":6,"y":4},
				{"state":"Louisiana","short":"LA","fips":"22","x":4,"y":5},
				{"state":"Maine","short":"ME","fips":"23","x":12,"y":0},
				{"state":"Maryland","short":"MD","fips":"24","x":9,"y":4},
				{"state":"Massachusetts","short":"MA","fips":"25","x":10,"y":2},
				{"state":"Michigan","short":"MI","fips":"26","x":7,"y":2},
				{"state":"Minnesota","short":"MN","fips":"27","x":4,"y":1},
				{"state":"Mississippi","short":"MS","fips":"28","x":5,"y":5},
				{"state":"Missouri","short":"MO","fips":"29","x":4,"y":3},
				{"state":"Montana","short":"MT","fips":"30","x":2,"y":1},
				{"state":"Nebraska","short":"NE","fips":"31","x":3,"y":3},
				{"state":"Nevada","short":"NV","fips":"32","x":1,"y":2},
				{"state":"New Hampshire","short":"NH","fips":"33","x":11,"y":1},
				{"state":"New Jersey","short":"NJ","fips":"34","x":9,"y":3},
				{"state":"New Mexico","short":"NM","fips":"35","x":2,"y":4},
				{"state":"New York","short":"NY","fips":"36","x":9,"y":2},
				{"state":"North Carolina","short":"NC","fips":"37","x":8,"y":5},
				{"state":"North Dakota","short":"ND","fips":"38","x":3,"y":1},
				{"state":"Ohio","short":"OH","fips":"39","x":7,"y":3},
				{"state":"Oklahoma","short":"OK","fips":"40","x":3,"y":5},
				{"state":"Oregon","short":"OR","fips":"41","x":0,"y":2},
				{"state":"Pennsylvania","short":"PA","fips":"42","x":8,"y":3},
				{"state":"Puerto Rico","short":"PR","fips":"72","x":12,"y":8},
				{"state":"Rhode Island","short":"RI","fips":"44","x":11,"y":3},
				{"state":"South Carolina","short":"SC","fips":"45","x":8,"y":6},
				{"state":"South Dakota","short":"SD","fips":"46","x":3,"y":2},
				{"state":"Tennessee","short":"TN","fips":"47","x":5,"y":4},
				{"state":"Texas","short":"TX","fips":"48","x":3,"y":6},
				{"state":"Utah","short":"UT","fips":"49","x":1,"y":3},
				{"state":"Vermont","short":"VT","fips":"50","x":10,"y":1},
				{"state":"Virgina","short":"VA","fips":"51","x":8,"y":4},
				{"state":"Washington","short":"WA","fips":"53","x":0,"y":1},
				{"state":"West Virgina","short":"WV","fips":"54","x":7,"y":4},
				{"state":"Wisconsin","short":"WI","fips":"55","x":5,"y":2},
				{"state":"Wyoming","short":"WY","fips":"56","x":2,"y":2}
			]; 

		//ask census for population statistics
	    d3.text('https://api.census.gov/data/2016/acs/acs5?get=NAME,B01001_001E,B08301_021E&for=state:*',function(census){

	    	//remove brackets from census response
	    	var noBrackets = census.replace(/[\[\]]+/g,'')

	    	//convert census into usable js object, with relevant data precomputed
	    	var censusDataset = d3.csvParse(noBrackets, function(d){
				return {
					state: d.state,
					name: d.NAME,
					total: +d.B01001_001E,
					homeWorkersPercentage: +d.B08301_021E / +d.B01001_001E
		      	};
	    	})

	    	//expose census division data by the division number
	    	var censusMap = d3.map(censusDataset, function(d){ return d.state });
	    	var censusMax = d3.max(censusDataset, function(d){ return d.homeWorkersPercentage });
			var colorScale = d3.scalePow().exponent(1).domain([0,censusMax]).range([0,1]);

	    	//chart sizing variables
	    	var cellSize = width/13;
	    	var cellSpacing = .1;
	    	var cellMargin = cellSize * cellSpacing;
	    	var stateSize = cellSize - (cellMargin*2);

	    	//draw circles
			svg.selectAll('.circleStates')
				.data(cartogram)
				.enter()
				.append('circle')
				.attr('cx', function(d){return d.x * cellSize + cellSize*.5 })
				.attr('cy', function(d){return d.y * cellSize + cellSize*.5 })
				.attr('r', stateSize/2)
				.attr('fill',function(d){
					var match = censusMap.get(d.fips); 
					if (match){
						return d3.interpolateViridis(colorScale(match.homeWorkersPercentage))
					}
					else{
						console.log("data for " + d.state + " is missing")
					}
				})
				.attr('class','circleStates')
			;

	    	//draw squares
			// svg.selectAll('.rectStates')
			// 	.data(cartogram)
			// 	.enter()
			// 	.append('rect')
			// 	.attr('x', function(d){return d.x * cellSize + cellMargin})
			// 	.attr('y', function(d){return d.y * cellSize + cellMargin})
			// 	.attr('width', stateSize)
			// 	.attr('height', stateSize)
			// 	.attr('fill',function(d){
			// 		var match = censusMap.get(d.fips); 
			// 		if (match){
			// 			return d3.interpolateInferno(colorScale(match.homeWorkersPercentage))
			// 		}
			// 		else{
			// 			console.log("data for " + d.state + " is missing")
			// 		}
			// 	})
			// 	.attr('class','rectStates')
			// ;

			svg.selectAll('.labels')
				.data(cartogram)
				.enter()
				.append('text')
				.attr('x', function(d){return d.x * cellSize + cellMargin + cellSize/4})
				.attr('y', function(d){return d.y * cellSize + cellMargin + cellSize/2})
				.attr('class','labels')
				.attr('font-family','courier')
				.text(function(d){return d.short})
			;
	    })

	</script>
</body>

</html>
```
