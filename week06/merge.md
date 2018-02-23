### Merging Data

One of the biggest challenges facing data visualizers is how to combine discordant, though related, datasets into one visualization logic. We've already seen a few different way to join datasets. To formalize these learnings, let's imagine a set of datasets — all referencing California, Illinois, and New York — structured in different ways.

```
	//like what we would get from copying and pasting from an ACS response
	//first key line removed
	//total population per state
	var mdArrayData = [
		["California","39250017","06"],
		["Illinois","12801539","17"],
		["New York","19745289","36"]
	];

	//like what we would type in ourselves
	//number of Starbucks per state
	//CA, IL, NY
	var arrayData = [2821,575,645];

	//like what we would get from d3.csvParse()
	//number of gun dealers per state
	var objectData1 = [ 
		{name: "Illinois", fips:"17", gunDealers: 1915},
		{name: "California", fips:"06", gunDealers: 1782},
		{name: "New York", fips:"36", gunDealers: 1667}
	];

	//like what we would get from d3.csvParse()
	//number of walmarts per state
	var objectData2 = [
		{stateCode:"020317", walmarts: 167},
		{stateCode:"010236", walmarts: 87},
		{stateCode:"040906", walmarts: 137}
	];

	//like what we could make ourselves		
	//number of hospital beds per state
	var singleObjectData = { Illinois: 30704, California: 74793, 'New York': 57118 };
```

All of these structures are commonly encountered. But, how can we use these datasets in combination to plot points or otherwise construct a visualization?

-----

The only rule about combining datasets is a simple one: **something must be shared**.

##### Shared Index
The ordering of items in two arrays is shared.

##### Shared Object Key and Value
Something to the left and right of the colon `:` in an object is shared.

##### Shared Object Key
Something to the left of the colon `:` in an object is shared.

##### Shared Object Value
Something to the right of the colon `:` in an object is shared.


If any of these things are shared, we can probably combine the datasets. There are many ways to do this, and it will depend on the specific case and data structure. Here are some examples, though the techniques might need to be contorted or mixed & matched for your needs.

-----

##### Shared Index: Running `.data()` Twice

Let's use two datasets that have the same items in the same order — they have shared *indices* — to plot `cx` and `cy` separately. 

This will draw the circles at 0 on the y-axis, and then *immediately move them* to the new cy position. This happens so fast that they never even show up at their initial position.

```
	//like what we would get from copying and pasting from an ACS response
	//first header line removed
	//total population per state
	var mdArrayData = [
		["California","39250017","06"],
		["Illinois","12801539","17"],
		["New York","19745289","36"]
	];

	//like what we would type in ourselves
	//number of Starbucks per state
	//CA, IL, NY
	var arrayData = [2821,575,645];

	d3.select('svg')
		.selectAll('.dots')
		.data(mdArrayData)
		.enter()
		.append('circle')
		.attr('cx', function(d){return parseInt(d[1])})
		.attr('cy',0)
		.attr('r',15)
		.attr('class','dots')
	;
	 

	d3.select('svg')
		.selectAll('.dots')
		.data(arrayData)
		.attr('cy', function(d){return d})
	;
```

Though this is the most understandable, there are many weaknesses. Merging by index is inherently fragile. It's very easy for an unexpected item — like Washinton D.C. or Guam in a set of states — to be in one dataset, and not the other. The visualization will work, but the data might be incorrectly combined! This is also a poorly performant chunk of code -- there are 2 redundant search operations! 

-----

##### Shared Index: Running `.data()` Once

Very similar to the above example. The main difference is that we don't need to run `.data` twice, and instead use an indexing variable `i` to access the correct item in sequence in the second dataset.

```
	//like what we would get from copying and pasting from an ACS response
	//first header line removed
	//total population per state
	var mdArrayData = [
		["California","39250017","06"],
		["Illinois","12801539","17"],
		["New York","19745289","36"]
	];

	//like what we would type in ourselves
	//number of Starbucks per state
	//CA, IL, NY
	var arrayData = [2821,575,645];

	d3.select('svg')
		.selectAll('.dots')
		.data(mdArrayData)
		.enter()
		.append('circle')
		.attr('cx', function(d){return parseInt(d[1])})
		.attr('cy', function(d,i){return arrayData[i]})
		.attr('r',15)
		.attr('class','dots')
	;
	 

	d3.select('svg')
		.selectAll('.dots')
		.data(arrayData)
	;
```

This has better performance than the example above, but it is harder to maintain and understand. Merging by index is still inherently fragile. It's very easy for an unexpected item — like Washinton D.C. or Guam in a set of states — to be in one dataset, and not the other. The visualization will work, but the data might be incorrectly combined! 

-----

So, that's how we have to handle *standard arrays*, as they only way to merge them is through their indices. A much better approach is to use objects. 

-----

##### Convert Array to Object

So, how do we convert data from an array to an object? Data returned from the census can be handled with a `d3.csvParse()` method. But, sometimes it's simpler to just convert it directly.

```
	//like what we would get from copying and pasting from an ACS response
	//first header line removed
	//total population per state
	var mdArrayData = [
		["California","39250017","06"],
		["Illinois","12801539","17"],
		["New York","19745289","36"]
	];

	var newObjectArray = [];

	mdArrayData.forEach(function(item) {
	    var newObject = {};
	    newObject.name = item[0];
	    newObject.population = parseInt(item[1]);
	    newObject.fips = item[2];
	    newObjectArray.push(newObject); 

	});

	console.log(newObjectArray);
	//returns 
	//[{name: "California", population: 39250017, fips: "06"}, 
	//{name: "Illinois", population: 12801539, fips: "17"}, 
	//{name: "New York", population: 19745289, fips: "36"}]

```

Easy peasy. 

-----

##### Shared Key and Value: Running `.data` Twice

In the example above, we created a `.name` attribute in our dataset, which is potentially shared between multiple datasets. Note, that the indices of these objects *don't match*, the states are in a different order, so we can't use any of the tricks we used above.

```
	//like what we would get from d3.csvParse()
	//number of gun dealers per state
	var objectData1 = [ 
		{name: "Illinois", fips:"17", gunDealers: 1915},
		{name: "California", fips:"06", gunDealers: 1782},
		{name: "New York", fips:"36", gunDealers: 1667}
	];

	//the mdArrayData was converted in the above example
	var convertedArrayObj = [
		{name: "California", population: 39250017, fips: "06"}, 
		{name: "Illinois", population: 12801539, fips: "17"}, 
		{name: "New York", population: 19745289, fips: "36"}
	];

	d3.select('svg')
		.selectAll('.dots')
		.data(objectData1)
		.enter()
		.append('circle')
		.attr('cx', function(d){return d.gunDealers})
		.attr('cy',0)
		.attr('r',15)
		.attr('class','dots')
	;
	 
	d3.select('svg')
		.selectAll('.dots')
		.data(convertedArrayObj, function(d){return d.name})
		.attr('cy', function(d){return d.population})
	;

```

Note that, in the second `.data()` call when we introduce our second dataset, we can add an *accessor function* to the `.data()` line. This is a *keying* function, where we're telling D3 to use the `d.name` attribute of both datasets to figure out how the objects should be merged *as an alternative to their indices*.

-----

##### Shared Value: Editing Objects to Match

In these two objects, the fips code for the states is available in both datasets, but in the second dataset it is prepended by its region and division codes. For example, New York (fips 36) is in the Northeast Region (fips 01) and the Middle Atlantic Division (fips 02). So it is formally, from largest to smallest geographic region, fips 	`010236`.

In order to mate these datasets, we need to make a unifying edit to synthesize the simpler state fips code, since we ultimately need *both the key and value to match*.

```
	//like what we would get from d3.csvParse()
	//number of gun dealers per state
	var objectData1 = [ 
		{name: "Illinois", fips:"17", gunDealers: 1915},
		{name: "California", fips:"06", gunDealers: 1782},
		{name: "New York", fips:"36", gunDealers: 1667}
	];

	//like what we would get from d3.csvParse()
	//number of walmarts per state
	var objectData2 = [
		{stateCode:"020317", gunDealers: 167},
		{stateCode:"010236", gunDealers: 87},
		{stateCode:"040906", gunDealers: 137}
	];

	objectData2.forEach(function(item){
		item.fips = item.stateCode.substring(4,6)
	})

	d3.select('svg')
		.selectAll('.dots')
		.data(objectData1)
		.enter()
		.append('circle')
		.attr('cx', function(d){return d.gunDealers})
		.attr('cy',0)
		.attr('r',15)
		.attr('class','dots')
	;
	 
	d3.select('svg')
		.selectAll('.dots')
		.data(objectData2, function(d){return d.fips})
		.attr('cy', function(d){return d.walmarts})
	;
```

Again, `.data()` is taking a keying function to ensure the datapoints are matched appropriately: this time by fips code. Fips code matching is often how we'll combine data with geographic vector shapes when drawing maps.

-----

##### Shared Keys: Matrix Flipping

This is a common scenario when the two datasets to be combined are transpositions (flipped matrices) of one another. This means that what is a row in one dataset is a column in the other.

```
	//like what we would get from d3.csvParse()
	//number of gun dealers per state
	var objectData1 = [ 
		{name: "Illinois", fips:"17", gunDealers: 1915},
		{name: "California", fips:"06", gunDealers: 1782},
		{name: "New York", fips:"36", gunDealers: 1667}
	];

	//like what we could make ourselves		
	//number of hospital beds per state
	var singleObjectData = { Illinois: 30704, California: 74793, 'New York': 57118 };

	objectData1.forEach(function(item) {
		var state = item.name;
		item.hospitalBeds = singleObjectData[state];
	})

	console.log(objectData1);
	//returns
	//[{name: "New York", fips: "36", gunDealers: 1667, hospitalBeds: 57118},
	//{name: "Illinois", fips: "17", gunDealers: 1915, hospitalBeds: 30704},
	//{name: "California", fips: "06", gunDealers: 1782, hospitalBeds: 74793}];
```

The outcome is a single dataset to push through your visualization logic, combining all necessary data. 

------

As mentioned above, every dataset merge attempt will have its own unique challenges, and will likely need some variation and combination of the techniques outlined here. Give these a try when an opportunity presents itself.

Return to this page frequently! 

Take a look at this week's [completed code](complete.md).

And, let's [practice with some homework](homework.md) to reinforce these learning.






