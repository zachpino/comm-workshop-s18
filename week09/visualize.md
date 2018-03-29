### Visualizing Geo Paths

D3 was built for drawing maps, and it's fundamentally the same thing as visualizing any other plot. There are, however some specific functions we need to prepare.

Note that we are including a new library, [D3's additional geoprojections](https://github.com/d3/d3-geo-projection) for more flexibility when projecting.

```html
<html>
<head>
	<title>
		Simple Map 
	</title>

</head>

<body>
	
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
	<script src="https://d3js.org/d3-geo-projection.v2.min.js"></script>

	<script>

		//display variables
		var width = 1200;
		var height = 800;

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

    		//decide how to project spherical coordinates to cartesian coorindates
		var proj = d3.geoAlbersUsa()
  			.scale(1500)
  			.translate([width/2, height/2]);
  		;

		//set up path projector. this converts the coordinates to svg path drawing instructions
	    	var path = d3.geoPath()
	    		.projection(proj);

	
		//access geojson file, err is if we get any errors in reading the file, geojson is the data
   		d3.json('counties.json', function(err, geojson) {
   		
			//draw all of the regions included in the 'features' child array
			g.selectAll('.counties')
				.data(geojson.features)
				.enter()
				.append("path")
				.attr("d", path)
				.attr("class","counties")
				.attr('stroke-width',1)
				.attr('stroke','white')
				.attr('fill', 'black')	
				.attr('opacity',1)			
		})
			

	</script>
</body>

</html>
```

-----

To see this map, we will likely need to [serve the content](simpleserver.md) to get past pesky browser security features.
