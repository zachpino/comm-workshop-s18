### HTML Container

Let's begin this introduction to D3 with the following recognizable code as an `index.html` prepared in Sublime. Remember, you can save your file as `index.html` and then type `<h` and hit tab for sublime to add much of it for you.

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

This code should be familiar. We have `head` and `body` tags nested inside of the `html` container.

We are going to make three additions to Sublime's default. First, add a `style` tag inside of `head`, ready for CSS rules.

And, two `<script>` tags have been added. The latter is a place for us to type our exercise data viz code. 

The former is a link to the [D3 data visualization library](http://www.d3js.org), a collection of functions and helpers that ease the work of producting data visualizations. Like `<img>` tags, the script tag takes a `src=""` attribute setting the path to the file. Rather than downloading this file directly, we are going to point browsers to the file on the D3 website so they always get the most up-to-date version. This is also one less file for us to manage.

By placing this line in our code, we are effectively including all of that [linked code](https://d3js.org/d3.v4.min.js) in our page. It's worth looking through, despite how hard it is to understand.

Now, we can use d3 functions to [select elements on the page](select.md).

