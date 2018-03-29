### Homework due 4/6

Draw a choropleth with TIGER data! Please make use of something other than the national counties scope we used in class. Your choropleth could be counties in a single state state, tracts per urban area, CSAs in a division, states per region, etc.

Note that, if you are **not** working at the national level, you may want to avoid the use of the Albers USA composite projection. You can instead rely on `d3.geoEquirectangular()` or `d3.geoMercator()` in such circumstances. These allow you to center your projection to some `[longitude,latitude]` position, thereby shifting the focal point of the map.

Here, we are adjusting our projection to use the Mercator projection, and centering on Chicago. You can Google "[city name] lat long" to get coordinates for any United States city. Make sure, if the values are degrees West or South, you add a negative sign. Also, Google returns latitude before longitude, so you'll want to flip them.

```js
var proj = d3.geoMercator()
	.center([-87.6298,41.8781])
	.scale(1500)
	.translate( [width/2 , height/2 ] )
;

```

Make use of a chromatic scale to fill the geo boundaries depending on one of the scaled values that TIGER provides in the `properties` child array of each geo entity. For instance, `ALAND` or `AWATER`. These aren't that intereting of course, but we'll be able to add more compelling data soon.

Screenshot your work and submit to blackboard.
