### Handling Events

D3 makes it easy for developers to elect from a wide set of interaction *events* to which any given page element can respond. On the desktop and mobile devices, events include:

- Clicking and double clicking with a configurable delay
- Dragging and dropping
- Typed keyboard input
- Focus and blur (on input elements)
- (Multi)Touch taps

There are [more events too](https://developer.mozilla.org/en-US/docs/Web/API/Event), but that batch tends to be the useful set for data visualization purposes.

In order to make an element respond to any of the above listed events, the syntax is the same.

```js
d3.select('#interactiveElement').on('event', function(d){
	//code for when the event is detected goes here...

	})

```

You'll often see this kind of function referred to as a *handler*, and we say that such event *handlers* are *attached* to an element.

For instance, if we wanted to make it so that when a button on a page is clicked, all the elements on the page with a specific classname are converted to have a red fill...

```html
<div id="redMaker">Make things red!</div>

<script>

d3.select(#redMaker)
	.on('click', function(d){

		d3.selectAll('.blueElement')
			.attr('fill','red')
			;

})

</script>
```

Pretty cool, huh?

The `d` in this case will refer to the data attached to any element that was created by d3 and has data bound to it.

-----

There is a special javascript keyword `this` that causes all kinds of problems in other contexts. But, in D3, its use is clear — it refers to the specific element that detected the event. This is very useful for handling mouse hovering, for instance. The mouse cursor entering an object triggers the `mouseover` event, and when it leaves the object, the `mouseout` event occurs. Both can be attached to objects and do different things, or `mouseover` can alter a state, and `mouseout` can restore the original condition.

```js
d3.select('svg')
	.selectAll('.dots')
	.data(dataset)
	.enter()
	.append('circle')
	.attr('cx',function(d){ return xScale(d.myXValue) })
	.attr('cy',function(d){ return yScale(d.myYValue) })
	.attr('r', 30)
	.attr('fill','red')
	.on('mouseover', function(d) {

		//'this' is a keyword that refers to the object that detected the event
		//select the dot that was mouseovered
		
		d3.select(this)
			.attr('fill','blue')

	})
	.on('mouseout', function(d) {

		//'this' is a keyword that refers to the object that detected the event
		//select the dot that was mouseovered
		
		d3.select(this)
			.attr('fill','red')

	})
;
```				

You'll also see that the event handler is attached to the objects directly when they are created. This is the D3 convention, though it isn't mandatory. You could, for instance, make the object, and then select them again to add the event handlers later in your code.

-----

Let's use this new understanding of event handlers to [make some text dynamic](switch.md) to help see which congressional district dot is which.

