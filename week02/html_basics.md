### Basic HTML Shell for Data Visualization

All web pages have a few mandatory bits and pieces. We will talk about all of the ways to manipulate the structure and content of web pages, but for now, we'll simplify things.

First, let's declare the document as an html file, a file written in the *hypertext markup language*, the language of the internet, by wrapping the whole file in the appropriate tag along with some other mandatory bits and pieces.


```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

</body>
</html>
```

`<!DOCTYPE html>` declares the page to web browsers as and HTML document and to parse the file as HTML.

Note all of the angle brackets `< >`, sometimes called *virgolettes*. These demarcate html *tags*, markup code that defines the structure of the web page. 

The `<head>` tag contains any code or text that *should not be displayed* on the resulting web page. For instance, tags specifying links to necessary scripts, stylesheets, and analytics libraries will be placed inside of the `<head>` tag, along with the `<title>` of the page, which is displayed in tabs bars and browser window headers.

The `<body>` tag contains all of the visible parts of the webpage. We add content there that we want to be visible to a visitor.

Note some of the tags are preceded by slashes. These end the areas defined by the tags. So, everything between `<body>`	and `</body>` are within the body of the page. All tags should be ended explicitly. By convention, elements contained within other elements are indented, to show the hierarchy of the page. The `<title>` tag is within the `<head>` of the page, and is accordingly indented.

All of the data visualizations produced within this course in javascript will be stuffed within a `<script>` tag in the `<body>` of the page, added like so.
	
```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	This is text that will display.
	<!-- This is text that will not display. -->
	<script>




	</script>
</body>
</html>
```

Note also how we can make a commment -- content not shown on the page, in order to take notes in code -- within html by surrounding text with the necessary character sequences `<!--` at the beginning of the comment and `-->` to end the comment.

If the file is saved and then opened in a web browser, the sentence within the `<body>` tags should appear as a very simple web page.

Now, let's [add some code into the `<script>` tag](js_basics.md).