
# Preparing and Transforming Data {#datatransformation}

It is a common adage that data analysts spend 80% of their time cleaning data and 
only 20% on value-add analysis. In this chapter we will show the basics of transforming 
data with the tidyverse package **dplyr**. Using these functions are the best way to 
reduce the overall amount of time spent on data cleaning and to create reproducible 
workflows whenever you receive new data.

## Data Pipelines

Before diving into the functions designed to help you transform data, we must cover 
a perculiar looking operator, the pipe or `%>%`. You will repeatedly see the pipe (`%>%`) 
used in the code examples for this chapter and in other parts of the book. This 
operator takes output from the function on its left side and passes it onto the 
function on its right side. As an example we will look at the `select()` function. 
The first argument in the function is `.data`. Whenever you use the pipe operator 
it will pass that output into the function's first argument, which in this case, 
is a `tbl_df`. This means that we must put a `tbl_df` object (a dataset) on the 
left side of the pipe operator and then the `select()` function on the right. 
The first argument is assumed to be the data, so the remaining argument inside 
the function, according to the documentation, should be one or more unquoted variable 
names or numbers representing the position of columns. If we put this together, 
the command looks like this: 


```r
library(tidyverse)
as_tibble(iris) %>% 
  select(Petal.Length, Sepal.Length, Species)
#> # A tibble: 150 x 3
#>   Petal.Length Sepal.Length Species
#>          <dbl>        <dbl> <fct>  
#> 1          1.4          5.1 setosa 
#> 2          1.4          4.9 setosa 
#> 3          1.3          4.7 setosa 
#> 4          1.5          4.6 setosa 
#> 5          1.4          5   setosa 
#> 6          1.7          5.4 setosa 
#> # ... with 144 more rows
```

The pipe is the glue for putting together multiple data transformations into a sequence. 
The benefits to using the pipe are that it reduces the amount of code needed to 
perform a sequence of operations.

## Selecting

It is common to have a dataset with more columns than you need or have helper columns 
that you've created but no longer need. In the section above we used the `select()` 
function allows you to select only the columns that you want. 


```r
as_tibble(iris) %>% 
  select(Petal.Length, Sepal.Length, Species)
#> # A tibble: 150 x 3
#>   Petal.Length Sepal.Length Species
#>          <dbl>        <dbl> <fct>  
#> 1          1.4          5.1 setosa 
#> 2          1.4          4.9 setosa 
#> 3          1.3          4.7 setosa 
#> 4          1.5          4.6 setosa 
#> 5          1.4          5   setosa 
#> 6          1.7          5.4 setosa 
#> # ... with 144 more rows
```

The select function has the nice feature of also being able to rename columns as you 
select them. For example,


```r
as_tibble(iris) %>% 
  select(Petal.Length, Sepal.Length, Species)
#> # A tibble: 150 x 3
#>   Petal.Length Sepal.Length Species
#>          <dbl>        <dbl> <fct>  
#> 1          1.4          5.1 setosa 
#> 2          1.4          4.9 setosa 
#> 3          1.3          4.7 setosa 
#> 4          1.5          4.6 setosa 
#> 5          1.4          5   setosa 
#> 6          1.7          5.4 setosa 
#> # ... with 144 more rows
```

There is another function in **dplyr** called `rename()`, however, this can conflict 
with a function in the **plyr** package also named `rename()` if you have both packages 
loaded at the same time. To avoid any confusion, you can reference the function you want 
using the package name and a double colon before the function like so, `dplyr::rename()`. 
This notation specifies the function and where to retrieve its definition, in this case, 
the **dplyr** package. If you would like to avoid these sorts of package function conflicts, 
using just the `select()` function will do everything and a little bit more than using 
the `rename()` function. For example, `rename()` keeps all variables if you just specify 
one, then it will rename that one variable. The `select()` function will drop all other 
variables, but you can work around this by supplying the `everything()` function into 
`select()`. The `everything()` select helper is not the only one. There are helper 
functions that match columns by name, numerical range, prefix, suffix and more. In 
the example below we are renaming the id column, then pulling any of columns with 
"var" in the name, then everything else.


```r
as_tibble(iris) %>% 
  select(flower=Species, contains("Petal"), everything())
#> # A tibble: 150 x 5
#>   flower Petal.Length Petal.Width Sepal.Length Sepal.Width
#>   <fct>         <dbl>       <dbl>        <dbl>       <dbl>
#> 1 setosa          1.4         0.2          5.1         3.5
#> 2 setosa          1.4         0.2          4.9         3  
#> 3 setosa          1.3         0.2          4.7         3.2
#> 4 setosa          1.5         0.2          4.6         3.1
#> 5 setosa          1.4         0.2          5           3.6
#> 6 setosa          1.7         0.4          5.4         3.9
#> # ... with 144 more rows
```
**FIND EXAMPLE THAT MATCHES TEXT ABOVE IT**

## Mutating

Mutating a variable means changing a variable in place or creating a new variable. 
You can think of this as modifying the dataset you provide to the function and 
the variables of the dataset are the part that is changing or "mutating". In the 
following example we'll show in one step how to change an existing variable and 
create a new one. 



If you are a frequent user of Excel, the `mutate()` function is how you can implement 
the logic of an `IF` statement. In the example below we create a 0/1 indicator variable 
based on another column. 



In Excel you would implement this as `IF(A2="Yes", 1, 0)`. Another common data 
transformation exercise is recoding data. Instead of creating a series of nested 
IFs in Excel or in R, you can leverage the `recode()` function inside of `mutate()`. 
In this example we are changing the survey response choice labels to numbers so 
that we can calculate summary statistics, like the mean and standard deviation of 
responses.


```r
# mutate(response = recode(response, 
#                          `Strongly Agree` = 6, 
#                          `Agree` = 5, 
#                          `Slightly Agree` = 4,
#                          `Slightly Disagree` = 3,
#                          `Disagree` = 2,
#                          `Strongly Disagree` = 1))
```

If you have many questions and would like to them all in one pass, then you can 
implement it like this... [WHAT IS THE TRICK HERE?]

VLOOKUP -> `left_join()`

We will discuss relational data and joins in more detail in Chapter 5

As a final note on mutating variables, be careful not to use the `transmute()` 
function unless you intend to keep only the variables that the function creates, 
while dropping the rest from your dataset.

## Grouped Mutates

A particularly challenging type of transformation in Excel is creating variables 
based on a group of records and applying it across all rows for the group. For example, 
calculating the difference between an individual's maximum value compared to all other 
values. This requires finding the maximum for the group, then comparing it with each 
observation for the group. Typically, you might accomplish this through the creation 
of a Pivot Table and then using `VLOOKUP` to reference the maximum per individual. This 
gets unwieldly (sp) when then data changes. In R you can take the observations in a 
dataset and put them into groups based on a variable. In the example below, we have 
simply taken the dataset and modified it to remember that operations should be 
done in their respective group. Nothing has actually been changed on the data yet, 
but it is ready for an operation that acts upon the grouped data. The next step is 
to create that variable we mentioned above that represents the difference between 
the maximum value for the individual and each of their corresponding observations. 
In this example, we'll also create another variable indicating `TRUE/FALSE` whether 
the row is the maximum to provide a visual cue and filtering mechanism to throw out 
those specific observations if desired.


```r
# dat %>%
#   group_by()
```

## Summarizing

In the spirit of transforming data we will talk about summarizing it. A summary 
is just a transformation of underlying source data to a new form. Before summarizing 
data you must have an idea about HOW to summarize it first. Do you want to count 
rows, unique instances, calculate the 

COUNTIF/SUMIF/PIVOT -> `group_by()` + `summarize()`

In continuing with the references with Excel there is the capability to filter data 
in your summarizes, just how a Pivot Table allows you to identify variables to 
filter on. In a general sense, filtering just means that you remove any rows from a 
dataset that meet a certain criteria. 

## Spread and Gather

One particular type of transformation is moving the data between a long format and 
a wide format. In the long format you have one row per value where the values may 
be a different group or metric as indicated by another column in the data. For example, 

[INCLUDE LONG EXAMPLE]

This is the preferred 

## Functions

In some cases
