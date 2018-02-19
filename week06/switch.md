### Dynamic Text

Our plot looks good, but we still can't tell which district is which. So many indistinguishable orange dots!

![plot](late.png)

Let's use an event handler to change an svg text element on the page with an id of `key`, created previously but unused, to show the congressional district name.

Add this code onto the end of the creation of your dots, as though it were just another `.attr()` or `.style()`

```js
	//all the dot making stuff is above this line
	//when a dot is moused over...
	.on('mouseover', function(d) {
		//find a thing on the page with id 'key'
		d3.select('#key')
		//and show the name of the rolled over element in it
		.text(d.name)
		;

		//increase the visibility of the moused over dot 
		d3.select(this)
		.style('stroke-width',5)
		.attr('r',15)
		.attr('opacity',1)
		;
	})

	//when the mouse leaves the dot
	.on('mouseout', function(d) {
		//find a thing on the page with id 'key'
		d3.select('#key')
		//and empty its text
		.text('');

		//return the dot to its normal translucent style and size
		d3.select(this)
		.style('stroke-width',0)
		.attr('r',5)
		.attr('opacity',.5);

	})
;
```

![hover effect](hover.gif)

When a viewer mouses over a dot, we can see which congressional district that dot represents in the `#key` area of the svg.

With our visualization more interactive, can we reach any new insights in exploring our plot?

-----

We can now move on to another goal, adding another data point [encoded in the radius of the circle](money.md)! 