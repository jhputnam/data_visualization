# Data Preparation

Before you can make a figure, you first need to load your data into R. You may also need to transform it or reorganize it before graphing. In this tutorial, I will not fully teach how to use R (there are plenty of resources available), but I will go through a few key steps. 

As you write code, I like to separate it into separate code chunks in an R Markdown (.Rmd) file. Be sure to add lots of comments to your code so that others and future you can understand your thought processes and what each line does. 

# Keyboard shortcuts in R

These are for Windows but there are similar equivalents for Mac.

| Action      | Keyboard shortcut      |
| ------------ | ------------- |
| Insert new code chunk | ctrl + alt + i |
| Insert the pipe symbol | ctrl + shift + m (%>% and |> are both pipe symbols that mean the same thing)|
| Run whole code chunk | ctrl + shift + enter |
| Run the line your cursor is on/ selected code | ctrl + enter |

# Load your data

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

or choose only some of the columns

```
od600 <- read_csv("data/20260727_od600_invaders_jp.csv", col_select=c(2, 3, 17, 18, 19)
```

or use your own column names.

```
od600 <- read_csv("data/20260727_od600_invaders_jp.csv", col_names= c("time", "od600"))
```

# Getting to know your data

It is important to spend some time getting to know your data before moving on to make your visualization. Knowing things like the rough spread of your data, how many variables you measured and what they are, and how many different species/ BGCs/ etc. are in your dataset can help you interpret your data and answer questions about it from others. 

| Code (df = your data frame)     | What it does |
| --------- | ------- |
| ```dim(df)```     | returns the number of rows and columns your data has        |
| ```glimpse(df)```    | returns the number of rows and columns, all of the column names and their type (date/time/chr/dbl/lgl). Sometimes when you have errors it is due to the variable type so this can be helpful.  |
| ```head(df, 10)```          | returns the first 6 rows of data. Here I overrode that and had it return the first 10. tail(df) would show the last 6 rows.       |
| ```df %>% select("time", "species", "od600") %>% head()```         | If you have a lot of variables, you can select which columns you want to display        |
| ```names(df)```      | returns names of columns         |
| ```summary(df)```          | returns summary statistics like mean/median for numeric variables        |
| ```distinct(categorical_variable)``` | lists what the different levels (options) for that categorical variable are |

# Transforming your data

- dplyr is part of tidyverse, so as long as you loaded the tidyverse library, you can use these commands
    - ```select()``` - choose a subset of columns
        - ```df %>% select(name, od600, category, strain)``` select columns by name
        - ```df %>% select(name:strain)``` select all columns between name and calories
        - ```df %>% select(-(name:strain))``` select all columns except those from name to calories (inclusive)
        - ```df %>% select(starts_with(”s”))``` select columns that start with the letter s
        - ```df %>% select(contains("o"))``` select columns that contain "o" in their name
        - ```df %>% select(name, od600, replicate, everything())``` move name, od600, and replicate columns to the far left while keeping the rest of the columns. ```everything()``` selects the rest of the columns. This can be helpful if you have a lot of variables in your data frame and are sick of scrolling around to see what you want
        - ```df %>% select(1:6, -contains("rep"))``` select first six columns except for the columns with the word “rep” in the column name
    - ```filter()``` - choose a subset of rows (below are two different ways to do the same thing) 
        - ```df %>% filter(strain == Bc | strain == Fj | strain == Pk)``` 
        - ```df %>% filter(strain %in% c(Bc, Pk, Fj))``` 
    - ```mutate()``` - create new variables (columns) based on existing ones
        - ```df %>% mutate(new_variable = old_variable / 60)```
        - ```
          df %>% mutate(category = case_when( # make a new variable named category
           strain == "Bc" ~ "THOR", # when strain is Bc, set category to THOR
           strain == "CI01" ~ "Invader" # when strain is CI01, set category to Invader
           )
          ```
        - ```df %>% mutate(log_cfu = log10(cfu))``` - make a new column, log_cfu, that is the log10 of the existing column cfu
    - ```group_by()``` - divide up the data into subsets. Usually this is done before performing another transformation
       - ``` df <- df %>% group_by(category) %>% summarize(avg_genome_size = mean(genome_size)) ``` group by category, then calculate the average genome size for each category
    - ```summarize()``` - perform calculations that summarize a variable over a group of rows (eg. calculating average)
        - ```df %>% summarize(total_bgcs = sum(bgc_count))``` - total the values in a column. If you have a column with bgc_count with every row being a genome, you could sum them all to get the total number of bgcs in all of your genomes
        - ```df %>% summarize(num_samples = n())``` - count the number of rows (this can be helpful if you do this after grouping your data frame to see how many samples you have for each group or something)
    - ```arrange()``` - sort a data object according to the columns specified
       - ```df %>% group_by(category) %>% summarize(num_genomes = n()) % arrange(desc(num_genomes))``` - this will list all of your categories from the highest number of genomes to the least
    - ```count()``` - count the number of rows that have each unique value in the specified column. This can be helpful when you want to see what the possible values are for a certain categorical variable. 
    - ```rename()``` - an easy way to rename the columns of a data object
       - ``` df %>% rename(new_column_name = old_column_name) ``` 
 
When performing any of these transformations, you can just pipe it, in which case what you do will only stay within that section of code. When you call that object somewhere else, it will still be the "old" version without your transformations.
```
df %>%
  select(od600, strain, time) # select only the od600, strain, and time columns of df
  # can do further analyses if you put the %>% symbol at the end of the previous line
# this won't save your changes to the df object
```
Another option is to save your changes to a new object.
```
new_df <- df %>% # save df with the following changes to a new object called new_df
    mutate(
      time_hr = time / 60, # make new column called time_hr that is the old column time that already exists in df divided by 60
      log_od600 = log(od600) # make a new column called log_od600 that is the log of the column od600 that already exists in df 
   )
```
Lastly, you can save your changes back to the same object, which overwrites your df object. Be careful!
```
df <- df %>% # make changes to df and save them back to df (overwrites your df object- be careful! But sometimes this is useful if you make a change you'll never want to undo)
    mutate(
      time_hr = time / 60, # make new column called time_hr that is the old column time that already exists in df divided by 60
      log_od600 = log(od600) # make a new column called log_od600 that is the log of the column od600 that already exists in df 
   )
```
It's helpful to make several intermediate variables as you transform your data. If you want to do a slightly different analysis or make changes, it's nice to not have to go all the way back to the beginning. 

You may want to use relational or logical operators when you are transforming or selecting data. 

| Relational Operator | Meaning |
| ------ | ------ |
| ==      | Equal to (when evaluating if two things are equal. = is used to assign, not to check equality) |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

| Logical Operator | Meaning |
| ----- | ---- |
| & | And |
| \| | Or |
| ! | Not |

If you are working with a data set that has dates or times, I recommend using the ```lubridate``` library. 


 
