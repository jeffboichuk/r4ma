
# Data Visualizations {#dataviz}

Good marketing tells a story, it evokes an emotion, and elicits a response. The same 
can be said about good data visualizations. In this chapter we will show you how 
to use the R package **ggplot2** to visualize different types of marketing data to 
tell your story.

## Creating a Canvas

The **ggplot2** package is an interesting solution because it does not provide a set of 
chart types that you can pick and choose. Microsoft Excel has always provided a 
fixed set of scattercharts, bar charts, and other popular visualizations. 
In contrast, ggplot2 an extensible system of commands that build literally any 
picture you'd like to create. Talented R users have created ggplot masterpieces, 
such as, the picture of Hadley. 

![](images/ch3-hadley-plot.jpg)  
***
ADD CREDIT TO GARRETT GROLEMUND AND DAVID KAHLE
***

Every ggplot visualization starts with a canvas. You can create a blank canvas using the 
function `ggplot()`. This function takes two arguments: 1) `data` and 2) `mapping`. 
You can think of the `data` argument as a pallete of information from which to construct 
the plot and and the `mapping` as the plan for how to structure that information (e.g. 
as the x-axis, y-axis, size, shape or color). Supplying these argument still stop 
short of actually creating a plot


```r
library(tidyverse)
#library(completejourney)
#ggplot(data=iris, mapping=aes())
```

## Adding Layers of Geoms

Now that you've created a blank canvas, you need to add layers to it. In the canvas example 
above we used the `aes()` function, which is short for aesthetics. When you define the 
aesthetics in the top level `ggplot()` function call, it applies those aesthetics to 
every layer that subsequently gets applied to the plot. Layers is the core idea of 
constructing a plot. Every new layer gets added to the canvas via the plus sign 
(`+`). As an example, let's add a set of points to the canvas. You can do this 
using the `geom_point()` function. 


```r
# ggplot(data=iris, mapping=aes()) + 
#   geom_point()
```

A "geom" is shorthand for adding a layer to your plot of a specific geometric shape. 
Geoms are the heart of the plot because they define whether the plot is a line plot, 
scatterplot, or bar plot. In each of these examples, the geom would be `geom_line()`, 
`geom_point()` or `geom_bar()` and there are many more geom types to consider. The 
**ggplot2** package tries to makes things intuitive and easy to remember. However, 
if you need a list of all the geoms you can find them using tab completion in RStudio. 
Just type `geom_` in your RStudio console window , then press `TAB`. This will 
trigger the tab-completion feature in RStudio and show you the list of geoms that 
are available for you to use. 

![](images/ch3-geom-tab-completion.png)

## Adding Labels, Axes, and Legends

With plots it is important to pay attention to the details. These details make an 
effective plot and just like Microsoft Excel allows you to add and customize each 
element, so does ggplot. The trick is knowing which functions to use so in this 
section we will introduce a laundry list of them and then present all of them 
together to create a single polished plot. 

scale_x_continuous, scale_x_discrete
scale_y_continuous, scale_y_continuous

We highly recommend using the **scales** package when plotting. It comes with a variety 
of functions to make the scale of axes easier to read.

labs()

guide()

## Faceting Data by Group

A common research question is comparing a response across groups. The best way to 
visualize these relationships is to use the `facet_grid()` function. A facet 
creates a panel of plots with one for each value in the grouping variable. In the 
example below we have created a histogram for each Species in the iris dataset (**NOTE: 
REPLACE WITH MKTING EXAMPLE**).



One important aspect to remember when creating facet charts is the scale of the 
axes. You can accidentally, and purposefully, mislead readers by having the same 
metric plotted on two different axis scales. **IS THIS THE default behavior for the 
`facet_grid()`**

The syntax for facetting data has changed over time, from formula notation to a newer 
style. You may see examples online that use this older notation like so `facet_grid(.~var)`. This is equivalent to `facet_grid(cols=vars(var))`.

## Chart Types

Marketing Specific Charts?
pie chart? a critique on pie charts

## Advanced Plotting

theme_blank()
ggthemes
annotating?
typically needing long format? gather?

extentions?
We would be remiss not to mention the amazing collection of open source "extensions" 
that make it easier to produce beautiful plots. These are ggextentions. 
