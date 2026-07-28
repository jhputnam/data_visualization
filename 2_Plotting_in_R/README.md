# Plotting in R

I almost always use ggplot to make plots in R, though there are other options if you're working with a niche kind of dataset. For heatmaps, there is a ggplot option, but you can also use pheatmap (pretty heatmap). For this tutorial, I will focus on ggplot. 

# Choosing Plot Type

If you're not sure which type of plot would best display your data, see the flowchart on slide 4 of Data_visualization_resources to help you decide. See also [this site](https://datavizproject.com/). 

Here are the main plot types I use, but see the whole list [here](https://ggplot2.tidyverse.org/reference/). 

| Code    | Plot Type |
| --------- | ------- |
| ```geom_point()```    | scatter plot   |
| ```geom_col()```     | bar chart   |
| ```geom_line()```    | line graph   |
| ```geom_boxplot()```    | box plot: see [this resource](https://www.geeksforgeeks.org/r-language/box-plot-in-r-using-ggplot2/) for tips on plotting boxplots in R, but don't leave the background gray like they did   |
| ```geom_violin()```   | violin plot   |



# Plotting Cheat Sheet

First you'll need to use ggplot, then choose your geom (chart type), then choose your overall theme. This takes away the ugly gray background in the standard option. I always use either theme_bw() or theme_minimal(). Then, you can add all sorts of customization using + at the previous line.
For code that goes within theme() or labs(), you can combine them into one theme() or labs(), separating each piece of code with a comma. 

```
df %>% # this is a pipe symbol. There is one other pipe symbol that does the same thing. Alternatively, you can put the df name before the aes in the ggplot argument ggplot(df, aes(...))
  ggplot(aes(x = time, y = od600, color = condition)) +
  geom_point() + # scatterplot
  theme_minimal() +
  # everything else goes here below your ggplot, geom, and the overall theme you're choosing lines of code
  labs(
    x = "Time (h)",
    y = "Optical Density at 600nm"
  ) +
  theme(
    axis.title.x = element_text(size=11),
    axis.text.x = element_text(size=9)
  )
```

| Code    | What it does |
| --------- | ------- |
| ```annotate(geom=”text”, label”Friday the 9th”, x = 2005, y = 13500, hjust=”right”)```     | adds text at specific coordinates in the graph   |
| ```labs(title = "Your Title Here")```      | add title. If it's long, you can use ```label_wrap("Your Title Here")```        |
| ```labs(subtitle = "Your subtitle here")```    | add subtitle        |
| ```labs(x = "Time (h)")```     | add x axis label. If it's long, you can use ```label_wrap("Long x axis label")```       |
| ```labs(y = "Optical Density at 600nm")```    | add y axis label. If it's long, you can use ```label_wrap("Long y axis label")```       |
| ```theme(axis.text.x = element_blank())```          | remove x axis labels. Swap x for y to remove y axis labels        |
| ```theme(axis.title.x = element_blank())```          | remove x axis title. Swap x for y to remove y axis title           |
| ```theme(axis.ticks.x = element_blank())```          | remove x axis tick marks. Swap x for y to remove y axis tick marks      |
| ```theme(legend.position="top")```    | move legend to top of graph (default is on the right)        |
| ```theme(legend.position="none")```     | remove legend     |
| ```theme(legend.title = element_blank())```     | remove legend title   |
| ```labs(color = "Legend title", shape = "Legend title")```          | for everything your variable is mapped to for your legend, put the title you want        |
| ```guides(color = guide_legend(override.aes = list(size = 4)))```           | change size of symbols in legend        |
| ```theme(plot.caption = element_text(size=11, hjust=0))```   | set caption to be left-justified and size 11 font         |
| ```labs(caption = str_wrap("Figure 1. Your caption here.", 110)```  | add caption. str_wrap wraps the text if it gets to long to fit as one line. Only put the number if you use str_wrap. You can play around with the number to make the caption the width you want.   |
| ```scale_x_continuous(breaks = seq(1, 7, by = 1.5))```    | adjust x axis tick marks/ grid lines    |
| ```theme(panel.grid.major = element_line(linewidth = 0.25, color = "gray"))```           | adjust thickness and color of major grid lines        |
| ```theme(panel.grid.minor = element_blank()```          | get rid of minor grid lines        |
| ```geom_hline(yintercept = 20, linetype = "dashed", color = "black", size = 2)```          | add a horizontal line at y = 20. You don't have to include linetype/color/size. If you want to do multiple, do ```geom_hline(yintercept = c(1, 20, 24))```         |
|           |         |
|           |         |
|           |         |


## Example 1

```
comic_characters %>% 
  select(year, name, publisher, sex) %>% 
  filter(year >= 1961, sex %in% c("Female Characters", "Male Characters")) %>% # just focusing on male vs. female and ignoring other genders for now
  group_by(year, sex) %>% 
  summarize(count = n()) %>% 
  mutate(percent = count/sum(count)*100) %>% 
  ggplot(aes(x = year, y = percent, color = sex)) +
  geom_line(size = 0.6) +
  theme_bw() +
  theme(
    axis.title.x = element_blank(),
    legend.position = "none",
    axis.title.y = element_blank(),
    axis.text.x = element_text(size=11),
    axis.text.y = element_text(size=11),
    plot.title = element_text(size=14),
    plot.subtitle = element_text(size=12),
    plot.caption = element_text(size=11, hjust = 0)
        ) +
  scale_color_manual(values = c("#e7298a", "#4daf4a")) +
  geom_hline(yintercept = 50, linetype = "dashed", color = "gray40", size = 0.9) +
  scale_y_continuous(labels = scales::percent_format(scale = 1)) +
  labs(
    title = "Gender Gap Remains Despite Increase in New Female Characters",
    subtitle = "Percentage of new comic book characters by gender",
    caption = str_wrap("Figure 1. Gender distribution of new DC and Marvel comic book characters each year 1961-2013. Characters with an unknown or different gender than male or female were not included in this analysis. Data from the comic_characters dataset from the fivethirtyeightdata R library. Data were scraped by Walt Hickey from the Marvel and DC Wikia databases in 2014.", 100)
  ) +
  annotate(geom = "text", label = "Female Characters", x = 1996, y = 24, hjust = "left", color = "#e7298a") +
  annotate(geom = "text", label = "Male Characters", x = 1998, y = 77, hjust = "left", color = "#4daf4a")
```

## Example 2

```
ggplot(mindfulness, aes(x=duration_mins, y=bpm_change, color=activity)) +
  geom_point(size = 4) + # adjust size of points in scatterplot. You can also choose a different shape besides circles here. Look up the table with the number code for each shape. 
  theme_minimal() +
  geom_hline(yintercept = 0, color = "darkgray") +
  scale_color_manual(values = c("gray", "hotpink")) +
  labs(
    title = "Long yoga sessions most likely to reduce heart rate",
    subtitle = "Short yoga or meditation sessions have a variable effect",
    x = "Session duration (mins)",
    y = "Change in heart rate (bpm)",
    caption = str_wrap("Data collected over a 2-week period from 01-24-2026 to 02-06-2026 by Josephine Putnam. Heart rate determined immediately before and after yoga or meditation.")
  ) +
  theme(legend.position = "top") +
  theme(legend.title = element_blank()) +
  geom_label_repel(aes(label = label), size = 3, data = mindfulness, show.legend = FALSE)
```

## Color

Use color sparingly and consistently. A change in color should convey information about the data (not just make it pretty).

#### Choosing colors

* Avoid rainbow color palettes. See slide 10 of Data_visualization_examples.
* [Here](https://r-charts.com/colors/) is a list of all the named colors in R if you want to use color names like "steelblue" instead of HEX codes.
* Color evokes emotion, which [varies by culture](color-meanings.com/color-symbolism-different-cultures/)
* Use colorblind friendly colors (thank you to Andrés Cumsille for some of these resources!)
  + [Color brewer](https://colorbrewer2.org/#type=diverging&scheme=PuOr&n=3) lets you check the box for "colorblind safe" when choosing color schemes
  + The [Okabe Ito color pallete](https://siegal.bio.nyu.edu/color-palette/) only goes up to 8 colors but is great
  + [Kelly's 22 colors of maximum contrast](https://medium.com/@rjurney/kellys-22-colours-of-maximum-contrast-58edb70c90d1) is another resource
  + Use [vischeck](vischeck.com) or [this simulator](https://www.color-blindness.com/coblis-color-blindness-simulator/) to check how your visualization would look to people with various kinds of color deficiencies


#### Code to adjust colors on your plot

* scale_color_manual(values=c("steelblue", "firebrick")
  + This lets you use your own non-default colors
* scale_linetype_manual(values=c(”22”, “solid”, “33”, “44”)
  + If you're doing a line graph, you can change linetypes in addition to color


#### A process for critiquing and improving your own/others’ graphs and visualizations

1. make a note of the first few things you see
2. make a note of the first idea that forms in your mind and then search for more
3. make notes on likes, dislikes, and wish-I-saws
4. find 3 things you’d change and say why
5. sketch/prototype your vision, and critique yourself
  


