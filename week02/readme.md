### Simple Data Visualization : Bar Chart

#### A Basic HTML Shell for Data Visualization

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

-----

#### Javascript Variables

All of this code goes inside of the `<script>` tags added above.

First, let's add a javascript variable and look at it.

```javascript

//make a variable
var myText = "hello world";

//print a variable
alert(myText);

```

This will produce a popup window saying "hello world," should the code above be saved and opened in a web browser. This is the ideal workflow — edit code in a text editor of your choice, and then preview the results by reloading it in a browser. Small difference in how browsers handle Javascript and HTML will lead to minor variations in the instructions that follow — sadly, the reality of all web programming.

First things first, all lines in Javascript terminate in a semicolon, `;`. This is the most common issue that will get in the way of new coders. Indentation and empty lines are ignored by the Javascript compiler, so use whitespace to keep code legible and intelligently structured.

Javascript, a weakly typed language, doesn't care what kind of data is saved into variables. Here, a string of text, enclosed in either double or single quotation marks, is saved into a variable called `myText`. Camel Case (all lowercase letters except for the beginning of words, no spaces or hyphens) variable names are used by convention. Note that 2 slashes makes lines into comments in Javascript. Multi line comments begin with `/*` and end with `*/`.

We could similarly save integers into variables. Note that numbers don't need quotation mark encapsulation, and all the standard arithmetic operators work as expected.

```javascript

//make a variable
var myFirstInteger = 5;
var mySecondInteger = 3;

/*
returns 8
because JS can add! 
*/

alert(myFirstInteger + mySecondInteger);

```

Be careful, because Javascript doesn't care about data types, it's easy to make mistakes.

```javascript

//make a variable
var myFirstInteger = "5";
var mySecondInteger = 3;

//returns 53
alert(myInteger + yourInteger);

```

Because Javascript is treating the first variable as the actual text `"5"` and not the counting integer `5`, it *concatenates*, or glues, the two together as a string.

Text can be concatenated together with the addition `+` operator.

```javascript

//make a variable
var myIntro = "Greetings";
var space = " ";
var myStatement = "my name is";
var myName = "Robot";

//returns "Greetings, my name is Robot"
alert(myIntro + "," + space + mystatement + space + yourInteger);

```


-----

#### Javascript Lists

Very rarely in data visualization are variables singular. More often, data comes in as a *list*, also called an *array*.

```javascript

var myList = [5,2,1,3,9,7];

``` 

Lists are encapsulated by square brackets `[ ]` and separated by commas. Lists can include any kind of data, in any combination.

```javascript

var myList = [5,"hello",1,3,9,7,"goodbye",8,2];

``` 

Items from a list can be accessed with square brackets and an `index`. The first item in the list has the index of `0`, to make math easier and *confuse students*. The second item is index `1`, and on increasingly.

```javascript

var myList = [5,"hello",1,3,9,7,"goodbye",8,2];

//returns "hello goodbye"
alert(myList[1] + " " + myList[6]);

``` 

Math can be done too...

```javascript

var myList = [5,"hello",1,3,9,7,"goodbye",8,2];

//evaluates to (5 + 3 + 2 + 1) * 8
//and returns 88
alert( (myList[0] + myList[3] + myList[8] + myList[2]) * myList[7]);

``` 

Negative indices can be used to count backwards in the list.

```javascript

var myList = [5,"hello",1,3,9,7,"goodbye",8,2];

//returns 1
alert( (myList[-2] - myList[-4]);

``` 



