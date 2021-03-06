
# Preparing and Transforming Data {#transformation}

It is a common adage that data analysts spend 80% of their time cleaning data and 
only 20% on value-add analysis. In this chapter we will show the basics of transforming 
data with the tidyverse package **dplyr**. Using these functions are the best way to 
reduce the overall amount of time spent on data cleaning and create reproducible 
workflows whenever you receive new data.

## Selecting

It is common to have a dataset with more columns than you need or have helper columns 
that you've created but no longer need. Intuitively, the `select` function 
allows you to select only the columns that you want. 

[EXAMPLE HERE]

The select function has the nice feature of also being able to rename columns as you 
select them. For example,

[EXAMPLE HERE]

There is another function in **dplyr** called `rename()`, however, this can conflict 
with a function in the **plyr** package also named `rename()` if you have both packages 
loaded at the same time. To avoid any confusion, reference the function you want 
using the package name and a double colon before the function like so, `dplyr::rename()`. 
This notation specifies the function and where to retrieve its definition, in this case, 
the **dplyr** package.

## Mutating

Mutating a variable means changing a variable in place or creating a new variable. 
You can think of it as modifying the dataset you provide to the function and the variables 
of the dataset are the part that is changing or "mutating".

Excel Conversion
IF -> `ifelse()`

Be careful not to use the `transmute()` function unless you intend to keep only 
the variables that the function creates, while dropping the rest from your dataset.

Grouped Mutates

Recode
Mutating can also be part of recoding data.
VLOOKUP -> `left_join()`

We will discuss relational data and joins in more detail in Chapter 5

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

## Functions

In some cases
