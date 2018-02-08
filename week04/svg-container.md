### Append an SVG Container

Back to our standard HTML container...

```html
<html>
<head>
  <style> 
  </style>
</head>

<body>

	<script src="https://d3js.org/d3.v4.min.js"></script>

	<script>
		//d3 data viz code goes here

	</script>
  
</body>
</html>
```

All of the code below will be inserted into the second `<script>` tag.

```html
	<script>
		//d3 data viz code goes here

		var width = 750;
		var height = 750;

		var svg = d3.select('body')
						.append('svg')
						.attr('width', width)
						.attr('height', height)
						;

		var background = d3.select('svg')
						.append('rect')
						.attr('width', width)
						.attr('height', height)
						.attr('x',0)
						.attr('y',0)
						.attr('fill','#ccc')
						;					

	</script>
```

First, we set-up some variables to store reusable values for `width` and `height`. Then, we scan the page for an HTML tag called `body`, inject an HTML tag called `svg` inside of it, and specify the mandatory `width` and `height` attribues so that the `<svg>` tag can be created on the page.

Since an svg element has now been created, we can search for it, and append *inside of it* an SVG `<rect>` with its four mandatory attributes `width`, `height`, `x`, and `y`. An additional `fill` attribute is set so we can specify the color of this background rectangle. Not mandatory at all, but a nice-to-have.

#### `.append()` creates an object *inside* of the element(s) previously selected, it creates *children*, not *siblings*.

With the svg container created, let's move on to considering [our data and how it will be mapped to pixels](scale.md).



