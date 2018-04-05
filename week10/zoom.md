### Zooming and Panning

D3 makes it super easy to add zoom and pan interactions to any svg element, mapped intuitively to scrolling/dragging on trackpads and pinching/touch+drag on mobile devices.

-----

Let's make a single change.

```js
//make an svg container for map
var svg = d3.select('body')
	.append('svg')
	.attr('height',height)
	.attr('width',width)
	.call(d3.zoom()
		.scaleExtent([1, 5])
		.translateExtent([[-width/2, -height/2 ], [width*1.5,height*1.5]])
		.on("zoom", function () {
			g.attr("transform", d3.event.transform)
			})
		);
;
```

This chunk of code adds interactive transformability, natively implemented and interpolated by D3, to our `g` SVG group. Anything added into that group will be transformed the same way by user interaction.

Note, importantly, the constraints implemented by `.scaleExtent([min,max])` and `.translateExtent([left,top],[right,bottom])`. These only allow the map to be transformed up to a certain point, so that the viewer doesn't accidentally zoom to close or far or pan the map out of view.

-----

What if we now wanted to add [some markers](point.md) to the interactive visualization? 
