### Points on Maps

Projections can be used to draw a lon-lat point on a map in the same way that they draw geographic paths. A simple SVG circle is used here, though any shape could be drawn and placed in this way.

```js

var dc = {lon: -77.0369, lat:38.9072}

//make an svg container for map
var capital = g
	.append("circle")
	.attr('cx',proj([dc.lon, dc.lat])[0])
	.attr('cy',proj([dc.lon, dc.lat])[1])
	.attr('r','')
	.attr('fill','red')
	.attr('class','geopoint')
;
```

Projections need both a longitude and latitude value to arrive at final svg coordinates. But, we only want one of those values for `cx` and `cy` each, so we use bracket notation to pull the correct element from the projected array.

-----

You can do similar things based on geographic entity area centroids. This is useful for, for example, placing labels or other symbols based on the centers of regions.

```js

var centers = g
	.selectAll('.centers')
	.data(geojson.features)
	.enter()
	.append("circle")
	.attr("class","centers")
	.attr('cx', function(d){
		return path.centroid(d)[0]
	})
	.attr('cy', function(d){
		return path.centroid(d)[1]
	})
	.attr('r',10)
	.attr('stroke','none')
	.attr('fill', 'red')	
	.attr('opacity',1)
;

```

-----

