
# Data Visualizations {#dataviz}

Good marketing tells a story, it evokes an emotion, and elicits a response. The same 
can be said about good data visualizations. In this chapter we will show you how 
to use the R package **ggplot2** to visualize different types of marketing data. 

## Creating a Canvas

The ggplot2 package is an interesting solution because it does not provide a set of 
chart types that you can pick and choose. For example, Microsoft Excel has always 
provided a limited set of scattercharts, bar charts, and other popular visualizations. 
In contrast, ggplot2 an extensible system of commands that build literally any 
picture you'd like to create. Talented R users have created ggplot masterpieces, 
such as, the picture of Hadley. Every visualization starts with a canvas. You can 
create a blank canvas with ggplot(). This takes argument such as `data` and `mapping`. You 
can think of the data as a pallete of information and the mapping as a plan for 
how to build the visual, but the function stops short of actually implementing it. 

## Geoms and Aesthetics (aes)  

A `geom` is shorthand for a object on your plot. Definition/Derivation of geom? The 
geoms are the heart of the plot because they define whether the plot is a line plot, 
scatterplot, bar plot, etc. In each of these examples, the geom would be a line, a point 
or a bar and ggplot makes that very easy to remember. If you need a list of all the geoms, 
type `geom_` in your console and press TAB. This will trigger the tab-completion feature 
in RStudio and show you the list of geoms that are available for you to use. 

## Facets

A common research question is comparing a response across groups. The best way to 
visualize these relationships is to use the `facet` functions. A facet is a ... 


## Chart Types

Marketing Specific Charts?

## Advanced Plotting

Talk about themes. 

We would be remiss not to mention the amazing collection of open source "extensions" 
that make it easier to produce beautiful plots. These are ggextentions. 

