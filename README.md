# data_visualization

This repository is meant to be a reference about best data visualization practices. Much of the content comes from LIS470: Data Storytelling with Visualization taught by Dr. Emilee Rader in Spring 2026.

# R Markdown

When working in R, I like to use R markdown files (.Rmd). This allows for making many different code chunks, which is a nice way to organize your code into steps. This makes it easier to return to your work and understand it. It also helps when you want to run a subset of your code. Rmd files also can be knit to html, which is a nice way to share your work. You can use headings, write paragraphs explaining your code or topic, and decide what code and figures you want to include in the html file. [Here](https://www.markdownguide.org/basic-syntax/) is a great resource on Rmd syntax. Of particular interest are headings. Be sure to read the best practices sections. 

For knitting your .Rmd file into html, you can decide what you want to show up in the output html file. Put these flags in the chunk label. For example: {r, include=FALSE, echo=FALSE, warning=FALSE, fig.align='center'}
* include=FALSE runs the code but doesn’t show the code or output when you knit
* echo=FALSE runs the code but only shows the output when you knit
* warning=FALSE prevents warnings generated from the code chunk from appearing in the html output (I usually test knit and if there are any warnings, I add this to the code chunk title the warning came from) 
* message=FALSE prevents messages generated from the code chunk from appearing in the html output
* fig.align='center' makes any figure output from that code chunk be centered in the html output





named colors in R: https://r-charts.com/colors/
adding a horizontal line ggplot: https://www.statology.org/ggplot-horizontal-line/
remove gridlines ggplot: https://www.statology.org/ggplot-remove-gridlines/
remove axis labels ggplot: https://www.statology.org/remove-axis-labels-ggplot2/
box plot ggplot: https://www.geeksforgeeks.org/r-language/box-plot-in-r-using-ggplot2/
