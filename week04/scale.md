### D3 Scales

A fundamental aspect of working with data in D3 is the notion of *scaling* data from one coordinate system to another. For instance, datasets in the census tend to be measured in the tens of thousands. 

We might want to visualize this very large data as a bar chart, but perhaps we only have 500 x 500 pixels to work with! In the past, we just divided large numbers to arrive at usable pixel coordinates. This is neither accurate, nor extensible. Scales solve this problem.

Scales use *domains* and *ranges* to manage visualization intent. 

- A *domain* is the boundary of our data. For instance, if our dataset comprised timestamps collected all day, our domain might be 0.00 to 24.00. A dataset of city longitude and latitudes would require two domains: the longitude domain would run from -180 to 180 (where negative longitudes are *degrees west* and positive longitudes are *degrees east*) and the latitude domain would run from -90 to 90 (negative latitudes for *degrees south* and positive latitudes for *degrees north*). The domain on the census dataset above would be 18,000 to 23,000, its minimum to its maximum value.

- A *range* is the boundaries of our data's intended representation. For example, we might want any of the above domains to fit into a 500 pixel square, so the range would be to 0 to 500. We also might want to make some data fit into the range between 0 and 1 to make relative arithmetic easier, a process called *parameterization*.

That's a lot of words, but a picture makes it a lot easier to understand.

![linear scale](http://www.jeromecukier.net/wp-content/uploads/2011/08/d3scale1.png)

This image and description match *linear scales* which scale data from the domain linearly to the range. There are many other scales available, for instance logarithmic, time, color, and quantile 'bucket' scales.

-----

D3 uses scales, made up of domains and ranges, most commonly to map data to intended screen coordinates. They are often called *maps* or *remapping* functions in other programming languages, and all they do is cross-multiply!

In this example, we might have numbers that fall between 25 and 50, and we want those values mapped to pixels 200 through 400. Domains and ranges are passed to scales as an array of two objects.

```js
	var myScale = d3.scaleLinear().domain([25,50]).range([200, 400]);

	//this will pop open an alert with the number 264
	alert( "The number 33 is mapped to " + myScale(33) );

```

There are many settings for scales, notable among them: 

- `.clamp()` forces numbers that are outside the domain to get scaled to the extremes of the range. A domain `0 to 100` and a range of `0 to 10` maps the number 30 to 3. Great! But, it also maps the number -30 to -3. We might want all negative numbers instead to be mapped to 0. `.clamp()` does this on both ends of the range, so 200, which would normally scale to 20, would instead be mapped with a clamped scale to 10. 

- `.nice()` extends the domains to the nearest round number or order of magnitude intelligently, so your charts don't begin and end at weirdly specific numbers.

More info, options, and examples are available on the [D3 reference page](https://github.com/d3/d3-scale).

-----

Commonly, we want to define the domain dynamically (for instance, if we don't actually know what data is flowing into our visualization but want it to behave predictably).

D3 can dynamically find the lowest and highest value in a dataset.

- Smallest Value: `d3.min(dataset_to_evaluate)` 
- Largest Value: `d3.min(dataset_to_evaluate)` 
- Array of Smallest and Largest Value: `d3.extent(dataset_to_evaluate)`

As you can imagine, we very often use the last one because its format matches what scales expect for their domains and ranges.

```js
dataset = [325,271,31,672,879,17];

var extents = d3.extent(dataset);

var myScale = d3.scaleLinear().domain(extents).range([0,200]);

alert( dataset[0] + " is mapped to " + myScale(dataset[0]) );
```

The browser should throw an alert "325 is mapped to 71.46171693735499".

------

When you have an array of arrays, you can also use `.extent()` with an *accessor function* to reach into the children arrays for specific values. This is a common approach with census datasets, and shows the way to more advanced D3 data manipulation.

Let's say, for example, we wanted to plot by region the percentage of total public transit commuters that take the ferry to work. We can divide ferry commuters by total commuters, and use those values as the extents for the domain of the scale.

The *accessor* takes an arbitrary value, usually just the letter `d` for *datum*. D3 runs an internal `for` loop whenever an *accessor* is called, and as a result, we can gain access to values from each item in the dataset without bothering with any `[i]` business. The code we write within an accessor function is as if the dataset *only had one datapoint*.

```js

//number of public transit ferry commuters, and total public transit commuters, per US geographic region

var dataset = [
	["Northeast Region","28077","3949163","1"],
	["Midwest Region","3207","986206","2"],
	["South Region","5521","1201415","3"],
	["West Region","22109","1512426","4"]
];

var extents = d3.extent(dataset, function(d){
					return d[1] / d[2];
				});

var ferryScale = d3.scaleLinear().domain(extents).range([0,100]);

```

Let's now use scales to [draw a dataset to the screen](line.md).
