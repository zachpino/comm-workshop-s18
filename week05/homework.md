### Homework for 2/22/18

In addition to continuing to refine your [dataset and story](../week03/dataset.md)...

Pull down several datasets from the Census API that are related to your chosen topic space(s). In addition, find a static dataset (.csv file or equivalent) that you can work with from your chosen plus space. Best to just paste that into your file as an array, and address it as we did datasets previously. 

Then, draw a parameterized matrix with the plus data plotted against the census datapoints. 

Ensure that this matrix is well designed by intentionally setting `.attr` and `.style` on your elements. Think about typography! They should look at least as considered as this week's example (a low bar to clear). Think about how your data content might influence the aesthetics of your matrix.

Try to imagine which ACS datapoints (in combination) might be a good match to a parameterized matrix presentation. Before visualizing anything, write down a hypothesis about how the data will interrelate. After visualizing, reflect on that hypothesis! Include this information somewhere in the web page `<body>`. 

Make sure you `parseInt(value)` to ensure anything that should be an integer is treated as an integer during addition. Use `parseFloat(value)` for handling the equivalent situation for numbers with trailing decimals.

-----

Here are some other challenges to add sophistication to your chart.

- Bonus: Can you use `d3.text(){ }` inside of another `d3.text(){ }` to request your census+ dataset?
- Bonus: Can you add rgb color so that all the plotted points map within a gradient?
- Bonus: Can you add another data point, encoded in the radius of your plotted points?
