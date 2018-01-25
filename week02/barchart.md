### Simple Bar Chart

This chunk of code draws an SVG rectangle for each item in a list of numbers, combining all of the previous lessons. It requires the [D3](http://www.d3js.org) data visualization library, but only uses it for item selection and creation.

![vertical bar chart](vertical_bar.png)

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<!-- this imports the D3 library -->
	<script src="https://d3js.org/d3.v4.min.js"></script>

	<script>
		//array of numbers
		var dataset = [120,230,40,70,150,100,25];

		//two variables for the size of the svg container
		width = 500;
		height = 500;

		//a variable to specify how tall the bars are
		barWidth = 50;

		//this line of code uses d3 to find the <body> tag on the page, and then injects, with .append(), an <svg> object into it
		//.attr() sets the attributes of the svg tag.
		var svg = d3.select('body')
						.append('svg')
						.attr('width', width)
						.attr('height', height)
		;

		//draw a rectangle as large as the svg container for background color choice
		var background = d3.select('svg')
						.append('rect')
						.attr('width', width)
						.attr('height', height)
						.attr('x', 0)
						.attr('y', 0)
						.attr('fill',"#eee")
		;

		//loop through the dataset
		for (var i = 0; i < dataset.length; i++) {

			//draw the bars. i is used to draw each bar lower than the previous one
			var bars = d3.select('svg')
						.append('rect')
						.attr('width', dataset[i])
						.attr('height', barWidth)
						.attr('x', 100)
						.attr('y', i * barWidth)
						.attr('fill', '#555')
			;
		}

	</script>
</body>
</html>

```

A more complex example, to draw a horizontal chart with labels using the SVG `<text>` tag, which is defined similarly to a `<rect>`.

![horizontal bar chart](horizontal_bar.png)

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<!-- this imports the D3 library -->
	<script src="https://d3js.org/d3.v4.min.js"></script>

	<script>
		//array of numbers
		var dataset = [120,230,40,70,150,100,25];

		//array of colors of the same length as the array above
		var dataColors = ["#ccc","#444","#999","#555","#aaa","#888","#333"];

		//two variables for the size of the svg container
		var width = 500;
		var height = 500;

		//two variables for the chart
		var barWidth = 50;
		var xAxis = 400;

		//this line of code uses d3 to find the <body> tag on the page, and then injects, with .append(), an <svg> object into it
		//.attr() sets the attributes of the svg tag.
		var svg = d3.select('body')
					.append('svg')
					.attr('width', width)
					.attr('height', height)
		;
		
		//draw a rectangle as large as the svg container for background color choice
		var background = d3.select('svg')
						.append('rect')
						.attr('width', width)
						.attr('height', height)
						.attr('x', 0)
						.attr('y', 0)
						.attr('fill', "#eee")
		;

		//loop throught the dataset
		for (var i = 0; i < dataset.length; i++) {
			
			//draw bars. subtraction from a set height is used to draw from the bottom rather than the top
			var bars = d3.select('svg')
						.append('rect')
						.attr('width', barWidth)
						.attr('height', dataset[i])
						.attr('x', i * barWidth)
						.attr('y', xAxis - dataset[i])
						.attr('fill', dataColors[i])
			;

			//draw text labels
			var labels = d3.select('svg')
						.append('text')
						.text(i)
						.attr('x', (i * barWidth) + .5 * barWidth)
						.attr('y', xAxis + 30)
						.attr('font-family','courier')
			;

		}

	</script>
</body>
</html>
```

Now, some [homework for review](homework.md)!