
# Preparing and Transforming Data {#datatransformation}

It is a common adage that data analysts spend 80% of their time cleaning data and 
only 20% on value-add analysis. In this chapter we will show the basics of transforming 
data with the tidyverse package **dplyr**. Using these functions are the best way to 
reduce the overall amount of time spent on data cleaning and to create reproducible 
workflows whenever you receive new data.



## Data Pipelines

Before diving into the functions designed to help you transform data, we must introduce 
a perculiar looking operator, the pipe or `%>%`. You will repeatedly see the pipe 
(`%>%`) used in the code examples for this chapter and in other parts of the book. 
This operator takes output from the function on its left side and passes it onto the 
function on its right side. As an example we will look at the `select()` function. 
The first argument in the `select()` function is `.data`. Whenever you use the pipe 
operator it will pass that output into the function's first argument, which in this case, 
is a `tbl_df`. This means that we must put a `tbl_df` object (a dataset) on the 
left side of the pipe operator and then the `select()` function on the right. 


```r
as_tibble(iris) %>% select(Petal.Length, Sepal.Length, Species)
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

The first argument is assumed to be the data, so the remaining argument inside 
the function, according to the documentation, should be one or more unquoted variable 
names or numbers representing the position of columns.

The pipe is the glue for putting together multiple data transformations into a sequence. 
The benefits to using the pipe are that it reduces the amount of code needed to 
perform a sequence of operations and it is easy to read the flow of operations.  

## Selecting

It is common to have a dataset with more columns than you need or have helper columns 
that you would like to remove. In the section above we demonstrated how 
to use the `select()` function with the pipe operator to pull out only the columns 
you want to work with. The `select()` function has the nice feature of also being 
able to rename columns as you select them. In the example below we select out three 
columns while renaming two of them.


```r
as_tibble(iris) %>% 
  select(petal_length=Petal.Length, sepal_lenth=Sepal.Length, Species)
#> # A tibble: 150 x 3
#>   petal_length sepal_lenth Species
#>          <dbl>       <dbl> <fct>  
#> 1          1.4         5.1 setosa 
#> 2          1.4         4.9 setosa 
#> 3          1.3         4.7 setosa 
#> 4          1.5         4.6 setosa 
#> 5          1.4         5   setosa 
#> 6          1.7         5.4 setosa 
#> # ... with 144 more rows
```

Note that there is another function in **dplyr** called `rename()`; however, this 
can conflict with a function in the **plyr** package also named `rename()` if you have 
both packages loaded at the same time. To avoid confusion about which function to use 
you can reference the function you want using the package name and a double colon before 
the function like so, `dplyr::rename()`. This notation specifies the function and 
where to retrieve its definition, in this case, the **dplyr** package. If you would 
like to avoid this package function conflict, using just the `select()` function 
will help you accomplish everything and a little bit more than what the `rename()` 
function can do. The `rename()` function keeps all variables if you specify just one, 
then it will rename that one variable. By default, the `select()` function drops 
all other variables not specified, but you can work around this by supplying the 
`everything()` function into `select()`. The `everything()` select helper is not 
the only one. There are helper functions that match columns by name, numerical 
range, prefix, suffix and more. In the example below we are renaming the ID column, 
then pulling any of columns with "var" in the name, then everything else.


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

Function | Behavior
----------|----------
`starts_with()` |  Starts with a prefix.
`ends_with()` |  Ends with a suffix.
`contains()` |  Contains a literal string.
`matches()` |  Matches a regular expression.
`num_range()` |  Matches a numerical range like x01, x02, x03.
`one_of()` |  Matches variable names in a character vector.
`everything()` |  Matches all variables.
`last_col()` |  Select last variable, possibly with an offset.

## Mutating

Mutating a variable means changing a variable in place or creating a new variable. 
You can think of this as modifying the dataset you provide to the function and 
the variables of the dataset are the part that is changing or "mutating". In the 
following example we'll show in one step how to change an existing variable and 
create a new one. 


```r
as_tibble(iris) %>% 
  mutate(Species = paste(Species, "flower"), 
         above_avg_sep_len = (Sepal.Length > mean(iris$Sepal.Length)))
#> # A tibble: 150 x 6
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa…
#> 2          4.9         3            1.4         0.2 setosa…
#> 3          4.7         3.2          1.3         0.2 setosa…
#> 4          4.6         3.1          1.5         0.2 setosa…
#> 5          5           3.6          1.4         0.2 setosa…
#> 6          5.4         3.9          1.7         0.4 setosa…
#> # ... with 144 more rows, and 1 more variable: above_avg_sep_len <lgl>
```

If you are a frequent user of Excel, the `mutate()` function is how you can implement 
the logic of an `IF` statement. In the example below we create a 0/1 indicator variable 
based on another column. 


```r
as_tibble(iris) %>% 
  mutate(Species = paste(Species, "flower"), 
         above_five_sep_len = ifelse(Sepal.Length > 5, 1, 0))
#> # A tibble: 150 x 6
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa…
#> 2          4.9         3            1.4         0.2 setosa…
#> 3          4.7         3.2          1.3         0.2 setosa…
#> 4          4.6         3.1          1.5         0.2 setosa…
#> 5          5           3.6          1.4         0.2 setosa…
#> 6          5.4         3.9          1.7         0.4 setosa…
#> # ... with 144 more rows, and 1 more variable: above_five_sep_len <dbl>
```

In Excel you would implement this as a formula `IF(A2 > 5, 1, 0)` in Row 2 of a new 
blank column and drag the formula down. 

Another common data transformation activity is recoding data. Instead of creating 
a series of nested `IF` statements in Excel or in R, you can leverage the `recode()` 
function inside of `mutate()`. In this example we are changing the survey response 
choice labels to numbers so that we can calculate summary statistics, like the 
mean and standard deviation of responses.


```r
# mutate(response = recode(response, 
#                          `Strongly Agree` = 6, 
#                          `Agree` = 5, 
#                          `Slightly Agree` = 4,
#                          `Slightly Disagree` = 3,
#                          `Disagree` = 2,
#                          `Strongly Disagree` = 1))
```

If you have many survey questions on this scale and would like to them all in one 
pass, then you can implement with the `mutate_at()` function. It is an extension 
of the `mutate()` function that can apply your logic "at" multiple columns.


```r
# mutate_at(c(), funs(recode(., 
#                          `Strongly Agree` = 6, 
#                          `Agree` = 5, 
#                          `Slightly Agree` = 4,
#                          `Slightly Disagree` = 3,
#                          `Disagree` = 2,
#                          `Strongly Disagree` = 1))
```

*** 
DECIDE IF WE HAVE AN EXAMPLE AND WANT TO SHOW MUTATE_IF()  

***

Aside from the `mutate_at()` function there is a `mutate_if()` function that will 
apply your logic "if" a column meets a certain criteria that you specify. This is a
very handy function if, for example, you want to convert multiple columns that 
are character strings into integers. 


```r
#mutate_if(is.character, as.numeric)
```

## Mutating within Groups

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
data you must first have an idea about how to summarize it. Ask yourself: Do I want 
to count rows? Unique instances? Do I want to calculate the average? Standard deviation? 
Excel users often summarize using a Pivot Table which has the summarizing functions 
`COUNT`, `AVERAGE`, `MAX` to name a few. These are very similar to what exists in 
R and below is a table that translates each of these summary methods to their equivalent 
counterpart in R.

Excel Function | R Function
----------|----------
COUNT | `n()` or `length()`
SUM | `sum()`
AVERAGE | `mean()`
STDEV | `sd()`
MAX | `max()`
MIN | `min()`

Below is an example in R of how to count the number of observations and compute 
the average.


```r
as_tibble(iris) %>%
  summarise(n = n(), mean=mean(Petal.Length))
#> # A tibble: 1 x 2
#>       n  mean
#>   <int> <dbl>
#> 1   150  3.76
```

If you would like to compute this same summary for different groups of the data 
then you can just add the `group_by()` function. As mentioned above, the `group_by()` 
function simply prepares the dataset so that it is segmented. Adding the `summarize()` 
function after the `group_by` means that the operations will be run separately across 
each of the data segments to compute one summary for each.


```r
as_tibble(iris) %>%
  group_by(Species) %>%
  summarise(n = n(), mean=mean(Petal.Length))
#> # A tibble: 3 x 3
#>   Species        n  mean
#>   <fct>      <int> <dbl>
#> 1 setosa        50  1.46
#> 2 versicolor    50  4.26
#> 3 virginica     50  5.55
```

In Excel, the alternative to using a Pivot Table to summarize data for a group might 
be to use the `COUNTIF`, `SUMIF`, `AVERAGEIF` functions. These functions perform 
the same summary methods as mentioned above, but only on rows that meet some 
criteria. This is better represented in an R pipeline by using the `filter()` 
function to only select the observations that meet your criteria and then summarizing. 
In the example below we remove X observations and then calculate Y. 


```r
as_tibble(iris) %>%
  filter(Species == 'setosa') %>%
  summarise(n = n(), mean=mean(Petal.Length))
#> # A tibble: 1 x 2
#>       n  mean
#>   <int> <dbl>
#> 1    50  1.46
```

In Excel you would implement this as a formula `AVERAGEIF(E2:E150, "setosa", A2:A150)`. 
To reiterate, in R filtering just means that you remove any rows from a dataset 
that meet a certain criteria. This is helpful in a pipeline because it will remove 
the observations while performing that pipeline calculation without removing them 
from the original dataset you placed at the top of the pipeline. The symbols for 
doing comparisons, also called "logical operators", are pretty much the same in Excel 
as they are in R. One key difference is that if you are checking whether two things 
are equal to each other in R, then you will need to use double equal signs (`A2==B2`) 
rather than the single equals sign that Excel uses `A2=B2`. Below is a table that 
shows where these operators are different in R compared to Excel.

Behavior | Excel Function | R Function
----------|----------|----------
Equal | `=` | `==`
Not Equal | `<>` | `!=`
Or | `OR()` | `|`
And | `AND()` | `&`

The operators such as `<`, `>`, `<=`, `>=` are the same in R as they are in Excel. In the 
example below we show multiple of these operators in action to show how they can 
be used together to select a very small subset of observations from a data set. 


```r
as_tibble(iris) %>%
  filter(Species == 'setosa',
         !(Petal.Length == 1.4 | Petal.Length == 1.5),
         Petal.Width < 0.2) %>%
  summarise(n = n())
#> # A tibble: 1 x 1
#>       n
#>   <int>
#> 1     1
```

## Spread and Gather

One particular type of transformation is moving the data between a "long" format and 
a "wide" format. In the "wide" format each metric might be in its own column. If you 
have 20 metrics then the dataset will have at least 20 columns and it starts to 
become wider than it is long, hence the name. The alternative is to take each of 
the 20 columns per observation and rearrange them longways where each column becomes 
a row. The data becomes much longer than it is wide, hence the name "long" format.  

The long format is usually more preferable because functions like `filter()`, 
`group_by()`, and `summarize()` can operate quickly across rows rather than columns. 
In addition, the long format is more compatible with the `ggplot()` plotting function 
to specify multiple series, colors, and facets. 

***
FIGURE OUT AN EXAMPLE THAT IS REALLY REPRESENTATIVE OF THIS
[INCLUDE LONG EXAMPLE]  

SHOULD WE SHOW AN EXAMPLE OF GGPLOT HERE? OTHER IDEAS/REASONS  

***

## Functions

Functions are powerful. They encapsulate a specific piece of logic that can be 
executed on-demand. Functions are the core component to almost every R package. 
The **dplyr** package has a few functions that make it efficient to call your own 
functions. For this reason we will discuss the basic of writing a function and using 
it in a data pipeline. Let's consider a made up function called `version2()` that 
appends the string " - V2" at the end of other character strings.


```r
version2 <- function(x){
  paste(x, "- V2")
}
```

In other examples we have used the assignment operator (`<-`) to save results or 
data into an object. In this case we are assigning some logic defined by the `function()` 
function to the object `version2`. We provide the `x` arugment as a placeholder 
for what users of the function should provide and then write the logic for how to 
handle `x`. In this case, the function should take `x` from the user's input to the 
function and paste `"- V2"` onto it. When writing functions it is helpful to assign 
a value to the argument (`x` in this case) and see how it works. When you are done 
testing the logic, then place everything inside the curly braces of `function(){}`. 
If the code does not work on its own, then it will not work inside the function. 
Here is a small example of how our function should behave: 


```r
x <- "name"
paste(x, "- V2")
#> [1] "name - V2"
```

You can see that the function performs the exact same operation: 


```r
x <- "name"
version2(x)
#> [1] "name - V2"
```

Now the interesting part is if you want to rename all of the column names in a dataset, 
according to this logic. The `rename_all()` function takes a list of functions as 
an input (`.funs = list()`). In this case we can supply the `version2()` function 
that we have created.


```r
as_tibble(iris) %>% 
  rename_all(version2)
#> # A tibble: 150 x 5
#>   `Sepal.Length -… `Sepal.Width - … `Petal.Length -… `Petal.Width - …
#>              <dbl>            <dbl>            <dbl>            <dbl>
#> 1              5.1              3.5              1.4              0.2
#> 2              4.9              3                1.4              0.2
#> 3              4.7              3.2              1.3              0.2
#> 4              4.6              3.1              1.5              0.2
#> 5              5                3.6              1.4              0.2
#> 6              5.4              3.9              1.7              0.4
#> # ... with 144 more rows, and 1 more variable: `Species - V2` <fct>
```

This is a simple example of having a custom function to define the column names of 
a dataset. A more common example is to perform an operation on some data and combine 
it all back together in a dataset. The **dplyr** package has a function called 
`map_df()`, which runs a function against every element in an object and ensures 
that the result of the function for each element is combined back into a single 
dataset.


```r
#map_df EXAMPLE HERE
```

If you are copy/pasting the same piece of code to run in multiple places, then it 
is probably a good sign that a function should be written to contain that logic 
and execute it in a consistent way. Functions make code easier to maintain and they 
typically run faster than loops or other programming structures. 

## Putting it all together

In this section we will show an example that utilizes many of the different methods 
described in this chapter so that readers can have a complete example
