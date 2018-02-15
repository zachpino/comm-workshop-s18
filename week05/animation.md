### Animating Elements and Handling Mouseover/Mouseout Events

Adding animation and interactivity is what D3 was designed for. All we have to do is identify an *event* to respond to, and then set up the new state we want our objects to transform into. D3 *tweens* the initial state to the new state over a configurable period of time. Moreover, D3 gives us the ability to set an *easing* parameter. This is a concept unique to animation: *how should the object animate with respect to time*. Read more and [view the possible variations and settings here](https://bl.ocks.org/d3noob/1ea51d03775b9650e8dfd03474e202fe).

To trigger all this functionality, all we need to do is elect which event to respond to with  `.on('event', function(d){})`, and call `.transition()` inside — which tells D3 to animate things. We also often set `.ease` for custom easing and `.duration()` — how long the animation should last, measured in milliseconds. 

All this code gets added on to the bottom of the `var dots = ...` chunk of drawing code. It is part of the same code block that plots the svg circles.

```js
			//this object should respond to mouse hovering
			.on('mouseover', function(d) {
				
				//look for an element with id name key and erase its text	
				d3.select('#key')
				//set the text of the key element to the name property of the dot
				.text(d.name);

				//'this' is a keyword that refers to the object that detected the event
				//select the rolled over dot
				d3.select(this)
				//turn on animation	
				.transition()
				//bounce animation
				.ease(d3.easeBounce)
				//animate over 1 second
				.duration(1000)
				//increase stroke width
				.style('stroke-width',5)
				//increase radius
				.attr('r',20)
				//increase opacity
				.attr('opacity',1);
		
			})
			//this object should respond to mouse moving away from it
			.on('mouseout', function(d) {

				//look for an element with id name key and set its text	back to default
				d3.select('#key').text('district');

				//reverse of the mouseover, without the fancy animation
				d3.select(this)
				.transition()
				.style('stroke-width',0)
				.attr('r',5)
				.attr('opacity',.5);
			})
		;
```

-----

Let's move on to some ([homework](homework.md) to get some practice.

