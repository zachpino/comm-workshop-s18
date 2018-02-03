### Homework for 2/7/18

In addition to looking for your [dataset and story](dataset.md)...

Pull down a dataset from the Census API to answer this question:

#### How many people walk to work, circa 2015, in each state?

Use the lessons from this week to draw a horizontal barchart to answer this question. Post to Blackboard, along with your scavenger hunt examples.

	> Hint: You will need to divide the numbers in the dataset when drawing, as otherwise, the bars will be thousands of pixels tall! For instance `(d[i][1] / 2000`
	> Hint: Your svg container needs to be really wide to accomodate all the states! 

![census bar chart](homework.png)

-----

Here are some other challenges to add sophistication and legibility to your chart.

- Bonus: Can you use Javascript mathematical manipulation to draw population percentages rather than the number of people? (not pictured below)	
- Bonus: Can you use Javascript mathematical manipulation to color the bars with their data too?
- Bonus: The color format `rgb(#,#,#)` requires integers. If you try to combine the above two goals (percentage bars and data-inferred color), your bars will be black because the percentages are really small floats (numbers with trailing decimals). Use `Math.round()` to convert your percentages into integers, something like... 
```Math.round( 1000 * (dataset[i][1]/dataset[i][2]) )``` 
Google `Math.round()` for more info. Thanks to Sam for catching this! 
- Bonus: Can you use label the bars with the abbreviated names of the states? Google `javascript substring` for the necessary code. 

![bonus version](bonus.png)
