# Data Preparation

Before you can make a figure, you first need to load your data into R. You may also need to transform it or reorganize it before graphing. In this tutorial, I will not fully teach how to use R (there are plenty of resources available), but I will go through a few key steps. 

## Load your data

Load the tidyverse library into R. The first time you use it, you will need to type install.packages("tidyverse") into the console. Libraries are really the magic of R. They are built by the community and free to use. Many libraries have been made for various types of analyses in the biological sciences. 

```
library(tidyverse)
```

Use read_csv() to load in a csv file. Set your working directory to where your .Rmd file and data are. In this example, the csv I'm loading is in a folder called "data" within my working directory.

```
od600 <- read_csv("data/20260727_od600_invaders_jp.csv")
```

When loading in a csv, you can do things like skip the first line 

```
od600 <- read_csv("data/20260727_od600_invaders_jp.csv", skip=1)
```

or use your own column names.

```
od600 <- read_csv("data/20260727_od600_invaders_jp.csv", col_names= c("time", "od600"))
```

## Getting to know your data

It is important to spend some time getting to know your data before moving on to make your visualization. Knowing things like the rough spread of your data, how many variables you measured and what they are, and how many different species/ BGCs/ etc. are in your dataset can help you interpret your data and answer questions about it from others. 

| Code (df = your data frame)     | What it does |
| --------- | ------- |
| dim(df)     | returns the number of rows and columns your data has        |
| glimpse(df)          | returns the number of rows and columns, all of the column names and their type (date/time/chr/dbl/lgl). Sometimes when you have errors it is due to the variable type so this can be helpful.  |
| head(df, 10)          | returns the first 6 rows of data. Here I overrode that and had it return the first 10. tail(df) would show the last 6 rows.       |
| df %>% select("time", "species", "od600") %>% head()         | If you have a lot of variables, you can select which columns you want to display        |
| names(df)      | returns names of columns         |
| summary(df)          | returns summary statistics like mean/median for numeric variables        |
|           |         |

