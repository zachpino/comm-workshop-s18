### Mapping Census Data to Geographic Entities

Confusingly (and rendering Google troubleshooting very difficult), the concept of matching data points with some other data entity based on a single shared property is called *mapping*. This is different from, though often pertinent to, drawing geographic or spatial visualizations colloquially called *maps*. 

Huh.

When discussing data, *map* always refers to data matching, wherein we map one data point to another after identifying one or more matching *keys*. *Geographic entity, feature, or vector* instead refers to a polygonal geospatial boundary that comes out of a shapefile.

-----

All we have to do is add a single line after acquiring our census data.

```js
var censusMap = d3.map(censusDataset, function(d) { return d.fips + d.district });
```

This line makes a new variable `censusMap` which exposes all of the census data based on one data point. Here, we combine the fips code and district number to produce a match for what is included in our geography file's properties arrays, `GEOID`, which is unique to each geographic vector.

```js
...
"properties":{"STATEFP":"17","CD115FP":"18","AFFGEOID":"5001500US1718","GEOID":"1718","LSAD":"C2","CDSESSN":"115","ALAND":27236513804,"AWATER":382224178}}
...
```

We can then search a map inside of an anonymous D3 function, for example when making a choropleth for Romance language speaking ability.

```js
var match = censusMap.get(d.properties.GEOID)
```

-----

And, in context...

```js
//don't consider puerto rico, guam, etc...
var romanceExtents = d3.extent(censusDataset, function(d){if (d.fips<60){return d.romance / d.total} else{return 0}});

var romanceScale = d3.scaleLinear().domain(romanceExtents).range([0,255]);

//draw all of the regions included in the 'features' child array
var districts = g
	.selectAll('.districts')
	.data(geojson.features)
	.enter()
	.append("path")
	.attr("d", path)
	.attr("class","districts")
	//.attr('stroke-width',1)
	.attr('stroke','none')
	.attr('fill', function(d){
		
		//We're iterating through the geographic entities.
		//Find the matching item in the census dataset for each geography.
		//Store that in match variable.
		var match = censusMap.get(d.properties.GEOID)
		//Check and make sure there's a match
		if(match){
			return "rgb(" + parseInt(romanceScale(match.romance / match.total)) + ",0,0)"
		}
		//if there isn't a match...
		else{
			console.log(d.properties.GEOID)
			return 'black';
		}

	})	
	.attr('opacity',1)		
;	

```

In this case, `d` refers to the geographic dataset, since that's what we're iterating through in our `.data()` line, and `match` refers to the census data.

-----

Spend some time on this page, using `console.log` to see how the datapoints are now available in your code.

Let's move on to some odds and ends like expected [geographic visualization interactiviy](zoom.md).
