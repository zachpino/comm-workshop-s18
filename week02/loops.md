### Javascript `for` Loops

All of this code goes inside of the `<script>` tags inside of an [html container](html_basics.md).

First, let's create an array of numbers, like what might come out of the Census API. In this case, we can imagine that we were attempting to visualize question 9 from the scavenger hunt about 

> Which Great Lakes bordering state — Minnesota, Wisconsin, Illinois, Indiana, Michigan, Ohio, Pennsylvania, or New York — has the highest number of individuals with graduate or professional degrees? What state in that set has the highest proportion of individuals with graduate or professional degrees?

```javascript

// from the census API call
// https://api.census.gov/data/2015/acs/acs5?get=NAME,B06009_006E,B01001_001E&for=state:27,55,17,18,26,39,42,36

var dataset = [
["NAME","B06009_006E","B01001_001E","state"],
["Illinois","1066084","12873761","17"],
["Indiana","375509","6568645","18"],
["Michigan","696956","9900571","26"],
["Minnesota","406930","5419171","27"],
["New York","1992047","19673174","36"],
["Ohio","761265","11575977","39"],
["Pennsylvania","986815","12779559","42"],
["Wisconsin","363838","5742117","55"]
] ;

```

Javascript uses the `for( ){ }` control structure to loop through items. The basic construction looks complicated, but is actually quite simple once the syntax is undestood.

```
for( beginning of loop state ; under what condition should the looping continue ; what happens after each iteration ){
	//things to do for each item
}

```

So, this comes together as...

```
for (var item = 0; item < list.length; item++) {
	//set of operations for each item
}

```

- `var item = 0;` : At the beginning of the loop, we make a placeholder variable called `item` and set it to equal to `0`.
- `item < list.length;` : The loop will run so long as the variable `item` is less than the number of items in the `list` array.
- `item++` : This is shortcut notation, commonly used, for `item = item + 1;`. After each item is processed, `item` is incremented by `1`.

The word `item` could be replace by any other string, it is simply the label that is used to refer to each item in the list. By convention, the label is usually just the letter `i`.

```
var example = [3,5,2,8];

for (var i = 0; i < example.length; i++) {
	
	alert(i);

} 

```

Each number will be printed in an `alert`.

A more complex example, prepared for the real census dataset from above:

```
for (var i = 0; i < dataset.length; i++) {

	var state = dataset[i][0];
	var count = dataset[i][1];

	alert( state + " has " + count + " individuals with graduate or professional degrees");

}

```

Again, seems complex, but it's simple after some study. The variable `i` is set equal to `0` and so long as `i` is less than the number of items in the `dataset`, we should draw an `alert`. After each `alert`, we add `1` to `i`.

Note the use of `i` inside the loop commands. This allows us to iterate through the dataset starting with the first item, then the second, then the third. The double brackets, for example `[i][0]`, is necessary since we are specifying a value of an array *inside of another array*. This is a commonly encountered reality of working with datasets.

If this code is run, an alert will popup for each item in the dataset and print a sentence. We could do some math for each state as well. `.toFixed(#)` can be applied to any number, and rounds to the specified number of decimal places.

```
for (var i = 0; i < dataset.length; i++) {

	var state = dataset[i][0];
	var count = dataset[i][1];
	var population = dataset[i][2];
	var percentage = ( (count / population) * 100 ).toFixed(2);

	alert( percentage + " % of the population of " + state + " have graduate or professional degrees");

}

```

Rather than generate an annoying popup, let's examine how we can draw these values to the screen visually using [SVG](svg.md).

