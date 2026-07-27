# data_visualization

This repository is meant to be a reference about best data visualization practices. Much of the content comes from LIS407: Data Storytelling with Visualization taught by Dr. Emilee Rader in Spring 2026.

#### A note on AI use

AI can help with coding in R if you run into errors. However, I have found that resources like stackoverflow, ggplot website, and my class notes can be much more helpful at helping me understand what my code is doing and why it didn't work. There are often many different ways to code something to get the same result, and I prefer to use the tools I was taught instead of an alternative generative AI way that is confusing to me. Either way, be sure that you can explain what each line of your code does. Importantly, generative AI is pretty bad at critiquing or making visualizations, so the principles herein are important to learn and follow yourself. 

# R Markdown

When working in R, I like to use R markdown files (.Rmd). This allows separation of your code into many code chunks, which is a nice way to organize your code. This makes it easier to return to your work and understand it. Outside of code chunks, you can add headings and paragraphs related to the code or its output. Separating your code into chunks also helps when you want to run a subset of your code. Rmd files also can be knit to html, which is a nice way to share your work. You can use headings, write paragraphs explaining your code or topic, and decide what code and figures you want to include in the html file. [Here](https://www.markdownguide.org/basic-syntax/) is a great resource on Rmd syntax. Of particular interest are headings (# outside of code chunks indicate headings, whereas # within code chunks indicates a comment). Be sure to read the best practices sections. 

For knitting your .Rmd file into html, you can decide what you want to show up in the output html file. Put these flags in the chunk label. For example: {r, include=FALSE, echo=FALSE, warning=FALSE, fig.align='center'}
* include=FALSE runs the code but doesn’t show the code or output when you knit
* echo=FALSE runs the code but only shows the output when you knit
* warning=FALSE prevents warnings generated from the code chunk from appearing in the html output (I usually test knit and if there are any warnings, I add this to the code chunk title the warning came from) 
* message=FALSE prevents messages generated from the code chunk from appearing in the html output
* fig.align='center' makes any figure output from that code chunk be centered in the html output
* fig.show='hide' hides plots from that code chunk in the html output

