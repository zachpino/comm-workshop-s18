### SVG Intro

We need to take a slight detour into SVG, scalable vector graphics. SVG is an incredible tool for designers of interactive digital experiences, specifying a highly refined programmatic language for drawing interactive and animatable geometry to the browser that is infinitely scalable and interoperable. SVG sits underneath the proprietary interface of Adobe Illustrator and many other vector drawing tools, and gives us the ability to draw anything in the browser that we could draw in such applications.

SVG code can be written by hand very easily. It very much looks like html tags.

##### Container

We need a basic HTML page, with a special tag to alert browsers that SVG code is incoming.

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

	<!-- svg code goes below -->
	<svg width="1000" height="1000">



	</svg>

</body>
</html>
```

All of the code below will go inside of that `<svg>` tag. Note the configurable sizing available as *attributes* within the `<svg>` tag.

##### Circles

To draw a circular shape, the svg tag looks like this.

```html
<circle cx="" cy="" r="" fill="" stroke="" stroke-width="" />
```

The `cx` attribute specifies the *center of the circle on the x-axis* and similarly `cy` the *center of the circle on the y-axis*. `r` determines the radius of the circle, and together with `cx` and `cy` is mandatory.

`fill` for the *fill-color*, `stroke` for the *outline color*, and `stroke-width` for the *outline thickness* are optional but commonly set. Colors can be set in hexadecimal form of 3 digits `#fff` or 6 `#ffffff`, or as [named entitites](https://www.w3schools.com/colors/colors_names.asp) like `'red'`.

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

	<svg width="1000" height="1000">

		<circle cx="200" cy="200" r="50" fill="red" />

		<circle cx="250" cy="250" r="50" fill="yellow" />

		<circle cx="300" cy="300" r="50" fill="green" />

	</svg>

</body>
</html>
```

Note that, confusingly, SVG's shapes are drawn ('biased') from the upper-left. The upper-left corner is coordinate `(0,0)`, and all shapes are drawn positively from that position. Shapes can be drawn in any order, though shapes drawn later or layered above those drawn earlier.

![svg coordindate system](https://developer.mozilla.org/@api/deki/files/78/=Canvas_default_grid.png)


#### Rectangles 

Constructed similarly, SVG rectangles have a few more mandatory settings than circles.

```html
<rect x="" y="" width="" height="" fill="" stroke="" stroke-width="" />
```


```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

	<svg width="1000" height="1000">

		<rect x="200" y="200" width="100" height="100" fill="none" stroke="red" stroke-width="15px" />

		<rect x="250" y="250" width="200" height="75" fill="none" stroke="yellow" stroke-width="15px" />

		<rect x="300" y="300" width="75" height="200" fill="none" stroke="green" stroke-width="15px" />

	</svg>

</body>
</html>
```


Note that `none` can be used as a setting for transparent shapes.

#### Next Steps

A more in-depth treatment is [available from Mozilla](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Introduction). It is also worth looking through the [svg reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Element) to understand what kinds of shapes can be constructed, and how.

Let's use the basics of SVG and Javascript to draw some [simple data visualizations](barchart.md).