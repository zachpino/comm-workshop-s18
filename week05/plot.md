### Plotting Data

Our data is structured and ready to use. We'll map transit type to x and commute length to y.

This code goes within the `d3.text(){}` block, underneath the previous data structuring code. 

```js
			//find the svg container
			var dots = d3.select('svg')
				//look for a set of objects that aren't drawn yet
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
					return yScale(d.longParameter - d.shortParameter)
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
				.attr('fill', '#f2844b');
			;
```

Again, nothing new here! 

![simple plot](plot.png)

What are some learnings we can tease out from this plot? Note the nearly linear relationship we're seeing, when commutes are longer, people tend to take public transit. Counterintuitive? What might explain what we're seeing?

We can also swap the parameters begin visualized on the y axis, and change the y-axis labels, to view a different parameter.

```
					.attr('cy',function(d){
						return yScale(d.lateParameter - d.earlyParameter);
					})
```

![simple plot](late.png)

Again, another nice linear relationship, with a clear focus. Commuters leave earlier when they drive. Expected or unexpected?  

-----

It's currently impossible to get more information on which dot corresponds to which congressional district. Let's [add some interaction](animation.md) to improve that.