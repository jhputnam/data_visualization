# Plotting in R

I almost always use ggplot to make plots in R, though there are other options if you're working with a niche kind of dataset. For heatmaps, there is a ggplot option, but you can also use pheatmap (pretty heatmap). For this tutorial, I will focus on ggplot. 

# Choosing Plot Type

If you're not sure which type of plot would best display your data, see the flowchart on slide 4 of Data_visualization_resources to help you decide. See also [this site](https://datavizproject.com/). 




annotate(geom=”text”, label”Friday the 9th”, x = 2005, y = 13500, hjust=”right”)
    - adds text at specific coordinates in the graph!

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

```
ggplot(mindfulness, aes(x=duration_mins, y=bpm_change, color=activity)) +
  geom_point(size = 4) +
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
*
    - scale_color_manual(values=c(”gray40”, “red”, “gray55”, “gray70”)
    - vischeck.com to check how my visualization would look to someone with colorblindness
    - scale_linetype_manual(values=c(”22”, “solid”, “33”, “44”)
    - use linetypes in addition to color to help cover your bases
    - color evokes emotion, varies by culture! color-meanings.com/color-symbolism-different-cultures/
    - avoid rainbow color palettes. See slide 2 of Data_visualization_examples. 
 
- A process for critiquing and improving your own/others’ graphs and visualizations
    1. make a note of the first few things you see
    2. make a note of the first idea that forms in your mind and then search for more
    3. make notes on likes, dislikes, and wish-I-saws
    4. find 3 things you’d change and say why
    5. sketch/prototype your vision, and critique yourself
 
named colors in R: https://r-charts.com/colors/
adding a horizontal line ggplot: https://www.statology.org/ggplot-horizontal-line/
remove gridlines ggplot: https://www.statology.org/ggplot-remove-gridlines/
remove axis labels ggplot: https://www.statology.org/remove-axis-labels-ggplot2/
box plot ggplot: https://www.geeksforgeeks.org/r-language/box-plot-in-r-using-ggplot2/
 


