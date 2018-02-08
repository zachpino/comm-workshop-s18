### D3 Selecting

Fundamental to all web work is understanding that all HTML tags (and SVG tags too!) sit within a structured, nested hierarchy. If you are careful with your indentation, that heirarchy is obvious.

For example (this is intentionally different from the code on the previous page), let's consider this page. The text is from a [traditional Munsee Lenape story](http://talk-lenape.org/stories?id=27), because the romance-language-biased lorem ipsum tool is overplayed and misleading to designers in our global and multilingual era! Note that we need to specify a different character set in the `<head>` of our webpage if we want accented or non-latin characters to show up correctly in browsers.

Bonus census question! How many households who are exclusively native american have the internet subscription necessary to access that page in each state? Are those numbers surprising? Is the percentage of native american households who can access that page smaller or larger than the entire population's equivalent percentage?

```html
<html>
<head>
	<meta charset="utf-8"/>
 	<style> 
 	</style>
</head>

<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>

	<div id="first-block">
		<img src="" />
		<p class="story" id="intro">
			Lòmëwe hùnt luweyok yuki kikayuyëmënaninkahke xinkwi mah na xanikw.
		</p>
	</div>
	<div id="second-block">
		<img src="" />
		<p class="story" id="climax">
			Mësi lih yu ta e ënta mëkëkèk òk ënta shinkèk. Wèmi awèn tëli ènta kiskaot muhòn. òk wèmi aèsës ènta thunat, muhòò.
		</p>
	</div>
	<div id="third-block">
		<img src="" />
		<p class="story" id="judgment">
			Na wa Kishelëmùkònk luwe, "Kehëla yukwe kchipaihòsi. Alëmi yukwe wënchi këmohulëneyo ki òk nël knichanàk òk nèl ahanhùkwi kuxwisàk. 
		<p class="story" id="conclusion">
			"Tëtàch elamakamika wèmi yu tali këmohuke òk nèl nichana."
		</p>
	</div> 
</body>
</html>

```


This page has an ancestor `<html>` element. That `<html>` element has two children, `<head>` and `<body>`. `<body>` has three children, all page division elements, `<div>`. Those are all *sibling* to one another. The children of each `<div>` are sibling `<img>` and `<p>` tags. The parent of each `<p>` tag is a `<div>`, and the grandparent of the `<p>` is `<body>`. Variations on these familial analogies can be infinitely applied once they make sense. For example, `<div id="third-block">` is the aunt of `<p id="intro">` and `<p id="judgment">` is its cousin.

In addition, the `<p>` tags have the `class` attribute set, which lets us apply reusable style definitions. Each also has an `id`, unique identifiers to be used only once per page. On a standard designer portfolio site, one might have exactly one hero image at the top of the page that might have an `id`, and many image thumbnails underneath that all share a `class` designation. Hopefully, [this *selector* logic](https://www.w3schools.com/css/css_syntax.asp) is familiar from prior CSS work. 

-----

With an understanding of page hierarchy and CSS selectors, we can use D3 to find objects on the page. These examples change [arbitrary CSS properties](https://www.w3schools.com/cssref/default.asp) using the `.style()` D3 method.

Open your web inspector and visit the console tab. There, we can enter this javascript code live and see the results.

- Find the *first* instance of a specific tag and change the background color to blue.

```js
d3.select('p').style('background-color','blue')
```

- Find all the instances of a specific tag and change the text color to red.

```js
d3.selectAll('p').style('color','red')
```

- Find all the instances of a specific class name and add a 3 pixel magenta stroke. Note the *dot* character (.), used to identify `class`es.

```js
d3.selectAll('.story').style('border','3px solid magenta')
```

- Find a specific tag by id and change the font. Note the *sharp* character (#), used to identify `id`s.

```js
d3.selectAll('#climax').style('font-family','impact')
```

- Find an element by hierarchy and capitalize all the letters. Here we find the first `<p>` that is the child of an element with an `id` of `third-block`. A space is used to step down the page hierarchy. Note that `<body>` has been always assumed.

```js
d3.select('#third-block p').style('text-transform','uppercase')
```

-----

With selectors covered, let's use them to find an element on the page and [inject an SVG container](svg-container.md) for our dynamic content.