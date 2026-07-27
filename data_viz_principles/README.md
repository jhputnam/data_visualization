# Data Visualization Principles

The world is full of more and more data, while at the same time our brains are becoming more and more saturated with information and demands on our attention. One of the most powerful ways of sharing our data and results is effectively visualizing them. When we create data visualizations, we must keep our audience and their limited attention in mind. 

### What makes a good data visualization?

* Truthful: don't withhold information or design a figure in a way that leaves out data or warps it
* Functional: accurately displays the data and allows the audience to make meaningful operations on it
* Beautiful: aesthetically pleasing (though this does not mean using colors just for colors' sake). Reduce visual clutter to reduce cognitive load. 
* Insightful: reveals something we would have had a hard time understanding without the visualization. If it could've been clear as a table, leave it as a table
* Enlightening: focuses on questions that matter

When we look at figures, we don't go "in order"; we see what first stands out. We can only see a few things at once, and we rely on conventions to help us quickly make sense of the visualization. Change and contrast stand out; be sure that those parts of your graph are what you want your audience to look at.

When we see a pattern (humans are very good at detecting them!), we naturally try to come up with an explanation. That explanation then might make it harder for us to see evidence to the contrary. Stay skeptical and think about alternative explanations. 

### Understanding our audience

Our audience will have limited time with our visualization. We need to help them make sense of it as quickly as possible with the least mental effort possible. Make it easy for them! Your audience will never spend as much time as you will to understand the point(s) you're trying to make.
* Reduce cognitive load by reducing visual clutter. Always remove the gray background that automatically comes with R plots. Use color sparingly and consistently. A change in color should convey information about the data, and not just be used to make the figure pretty. Make the important aspect/ pattern of the data stand out.
* Take advantage of **preattentive attributes**, the aspects of images that our brains automatically process. 
  + Form: length (bar graphs are often the easiest type of figure for people to understand), width (wider/darker/more bold), orientation, shape, size, enclosure (draw a circle around the data point you want the audience's attention drawn to)
  + Color: hue, intensity (gray out controls and leave conditions of interest darker/colored, for example)
  + Spatial position
* Also take advantage of the **Gestalt Principles**
  + Proximity: things close together appear more related than things spaces farther apart
  + Similarity: when things have similar color/shape/position, we group them together. If you have an orange group, a yellow group, and a blue group, the audience will automatically assume the orange and yellow groups have more in common with each other than with the blue group. Be careful about assigning colors and shapes.
  + Closure: when looking at a complex arrangement, we tend to look for a single, recognizable pattern. We fill in the blanks until we can make a pattern.
  + Enclosure: when objects are in the same closed region (for example, within a border), we perceive them as being grouped together. If there is a visual barrier between objects, we perceive separation.
  + Continuity: elements arranged on a line/curve are perceived to be more related than elements not on the line/curve.
 









AI can help with coding in R if you run into errors. However, I have found that resources like stackoverflow, ggplot website, and my class notes can be much more helpful at helping me understand what my code is doing and why it didn't work. There are often many different ways to code something to get the same result, and I prefer to use the tools I was taught instead of an alternative generative AI way that is confusing to me. Either way, be sure that you can explain what each line of your code does. Importantly, generative AI is pretty bad at critiquing or making visualizations, so the principles herein are important to learn and follow yourself. 

We must do the work to get to know our data well before making the most effective visualizations we can to communicate our main point. 
