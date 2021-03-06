
# Tools at your Disposal {#tools}

***
CHAPTER OVERVIEW NEEDED??

***

## Data

It may seem obvious that having data is a requirement for doing marketing analytics, 
but the interesting point is that you may have access to more data than you first 
realize. There are so many sources of data that are being actively tagged, passively 
logged, freely offered up by customers, and sold by vendors. In this section we will 
cover sources to consider for your own projects and the datasets that we'll further 
introduce throughout the book. 

When thinking about data it is helpful to put some structure around your brainstorm 
of potential sources. At a very high level, you have two sources of data: "Internal" 
data that is created or controlled by you or your organization or "External" data 
that is captured outside your organization. For example, "Internal" data might be 
the tracking of web tags on your website, customer transaction data, or recent survey 
data. It is possible that your organization purchased proprietary data from a vendor 
and controls that dataset in-house. The best way to access your "Internal" data is 
to start talking with the teams that collect and manage it. These could be front-line 
staff or employees in your IT department. If your organization has a customer service 
department and they log information into Salesforce, ZenDesk, or other tracking software 
then you have likely found a rich source of data. 

***
[INSERT A DIAGRAM HERE WITH SAMPLE LISTS]
 - Survey Data - the use of one time
 - Customer Data
 - Basket/Transaction/Scanner Data
 
 ***

When thinking about "External" data your mind may immediately jump to vendors selling 
access to data. These are great resources, but the world around you is full of data. 
Social media data is one that is ubiquitous. The movement for open data in government 
and the sciences has unlocked and shared a massive amount of data. More broadly, this 
type of information is available via a file download or an API. An API typically refers 
to a series of URLs that share data via the web. Organizations make these URL endpoints 
available publically or through a provisioned key to users who are interested. Scraping 
data from the web is an option, but we recommend first checking the terms of the website, 
looking for the site's `robots.txt` file, and seeing if programmatic access via API 
already exists.

In this book we will be using a number of external data sources in hopes that you 
will gain experience with them and be able to access them for your future projects. 
The organization 84.51&deg; has a laser focus on using data science to analyze 
patterns in customer data to drive better outcomes. They generously share a few 
datasets, namely, a dataset called the *Complete Journey* which contains a representative 
set of transactions at Kroger grocery stores for 2,500 households. This data is does 
not contain real transactions, but is a perfect dataset for us to highlight and hone 
skills in analyzing transaction data. Euromonitor...

Continue talking about when to use these sources and why we recommend.

 - Euromonitor
 - Delighted (NPS)
 - comScore
 - Google Trends

## Software

There is no shortage of options when choosing software for analysis. A number of
open source and proprietary tools have been introduced to make analyzing data easier. 
We think of these tools in three different categories:  

  1. Business Intelligence (BI) Tools
  2. Visual Analysis Tools
  3. Programming Languages  

Business intelligence (BI) tools are mainly used for summarizing and visualizing 
data. Some of the most popular tools include: Tableau, Domo, Pentaho, and Looker. 
The audience for these tools are mainly decision-makers of the data, managers and 
executives who need insights quickly. For this reason, these tools usually operate 
with a fixed set of features on top of a standardized data source. Depending on the 
tool there may be functionality to clean and curate data, but they main focus is on 
presenting the insights. These tools are extremely powerful and valuable, but as an 
analyst you will typically need more control and flexibility when handling data.  

In contrast with BI tools, visual analysis tools are designed with the analyst in mind. 
They usually have functions to retrieve and transform data as well as visualize and 
analyze it for insights. Some tools include: Excel, SPSS, RapidMiner, and Minitab. 
The most ubiquitous is of these tools is Excel. In this book we will draw analogies 
of how certain operations in Excel translate into R. These tools are great for ad hoc 
analysis because they are easy to maniupulate and you can literally see the data 
and how it changes throughout your analysis. This is a huge benefit to analysts 
because seeing the data makes it easier to spot anomolies and mistakes. Unfortunately, 
these tools do not make it easy to replicate analyses. Many of these tools are point-and-click 
systems so that whenever an action needs to be repeated it can take time to re-run and 
there is a risk of introducing errors.  

Finally, programming languages have more recently become a viable tool for analysis. 
With the explosion of data programming languages have developed libraries or modules 
specifically for handling data. They typically abstract some of the underlying code so 
that the analyst can focus on working with the data instead of fiddling with obtuse 
bits of code. Some tools include: Java, Python, Julia, Scala, and R. Prior experience 
with one of these languages is a good reason to begin using it for analysis. These 
tools have the steepest learning curve, so the more familiar you are with the syntax 
and structure, the faster you can begin analyzing data. For learners we recommend 
Python or R given they are at the forefront of data analysis and there are a number 
courses and online materials devoted to learning them. The tradeoff for being difficult 
to learn is that writing a script creates an artifact that is stable and lasting. It 
can be executed on demand and extended to have more functionality over time. Of all 
the tools mentioned in this section we recommend using a programming language for 
almost all of your analyses.  

## Getting Started with R

In this book we will further detail how the R programming language can be used for 
marketing analytics. We recommend the R language for a few reasons. First, it is 
an open source, cross-platform tool. This means that the software is free to download 
and use for academic and commercial purposes. It also runs on a variety of computer 
operating systems such as Windows, Mac, and Linux. This means that it is accessible 
to almost anyone. Second, the R language was designed specifically for analysis. 
Java, Python, and other programming languages have robust libraries to do analysis, 
but these are not the origin of the languge, so their documentation is often hard to 
read or unclear. In addition, examples on the internet are out of date or no longer 
work due to changes in versions. One reason why R is easier to learn and extend is 
that its development in recent years has been driven by the vision of Hadley Wickham. 
Hadley is a rockstar in the analytics community for his contributions to advancing 
the R programming language. He has created and introduced a style of programming and 
analysis based on "tidy" data principles in the seminal paper *Tidy Data* [@wickham2014]. 
The **tidyverse** [@R-tidyverse] is a collection of multiple packages (libraries) designed 
or influenced by Hadley's approach to analysis. These packages build upon each other 
so that it is easy to wrangle data into a tidy format and then proceed to analyze it. 
In order to get started you should install RStudio. This is the preferred application 
to write R code. After installing, open up RStudio and type the following into the 
bottom left pane entitled "Console":


```r
install.packages('tidyverse')
```

![](images/ch2-installing-tidyverse.png)

Pressing enter will run this command and a long stream of text and red messages 
will appear in the Console window. This is okay and usually a good thing. It means 
the messages indicate that the code library has been downloaded and unpackaged to 
your computer. Installing an R package is an important the first skill to learn. 
Note that the words "package" and "library" are interchangeable and both reference 
a collection of functions and code that you can download, install, and use in R. 
You will need to repeat the step of installing every new package that you want to use. 
You must install it, but only once. After it is installed, it will be available for 
you to use. However, you must "load" the library every time you start a new R session 
(e.g. open up RStudio). This step will make all the functions available in your session. 
In the Console window type `library(tidyverse)` to load the library. There will 
be a few messages that indicate the status of the library as you have loaded it. 
One way to check that the package is loaded is by ... The other way is to click 
on the "Packages" tab in the bottom right pane in RStudio. There will be a list 
of every package you have installed, including the Base R packages, with a check 
mark next to each one that you have loaded in the current session.

![](images/ch2-package-loaded.png)

We have created a companion package with data for this book. You can install and 
load that package by running the following code: 


```r
install.packages('completejourney')
library(completejourney)
```

We have instructed you to copy/paste or type this code into the Console window 
and press `ENTER` to execute it. This is okay for running a few small commands, 
but we recommend putting all of your commands into the top left pane, the Script Editor 
window of RStudio. This will be a self-contained reference of commands that you can 
run again whenever they are needed. You can send commands from the Script Editor 
window to the Console window by pressing `CTRL+ENTER` on Windows or `CMD+ENTER` 
on a Mac. The reason that there are two different panes in RStudio is that one 
is for composing your scripts and the other is for executing them. You can type 
as much as you would like in the Script Editor, but the variables and functions 
you write are created only when you execute the code. Again, we recommend writing 
your code in the editor pane and then executing it.

Now that you are familiar with installing and loading libraries you know how to 
set up your R session. The next step is writing and executing your analysis. With 
programming langauges the flow is to execute functions and save their result into 
a variable to inspect it or re-use it in another way. In programming this is called 
"assignment". You are assigning the result to an object in the session. We want to 
mention this now because R has a peculiar assignment operator that looks like this `<-`. 
Quite literally this means take the object on the right and push it to an object 
on the left. For example, if we want to assign the average of numbers 1 through 10 
to an object called "x" the code would look like this: 


```r
x <- mean(1:10)
```

You will see most operations in R having this flow where a command is performed 
and the result is assigned to an object using `<-`. Throughout the book we will 
introduce more functions with the assumption that you have a basic understanding 
of how to read the documentation for functions, run them, and assign the result 
to an object. For a more comprehensive guide to learning the basics of writing R 
code we recommend *R for Data Science* [@wickham2017] which is the inspiration for 
this book. In addition, we recommend *The Book of R* [@davies2016], *R in Action* 
[@kabacoff2015], and *R for Excel Users* [@taveras2016].

**** 
OTHER IMPORTANT CONSIDERATIONS TO TEACH BEFORE DIVING INTO DATA VIZ???  

****
