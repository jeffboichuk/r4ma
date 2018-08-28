
--- 
title: "R for Marketing Analytics"
author: ["Jeffrey Boichuk", "Steven Mortimer"]
url: 'https\://jeffboichuk.github.io/r4ma'
knit: "bookdown::render_book"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
colorlinks: yes
lot: yes
lof: yes
fontsize: 12pt
monofont: "Source Code Pro"
monofontoptions: "Scale=0.7"
github-repo: jeffboichuk/r4ma
description: "This is a minimal example of using the bookdown package to write a book. The output format for this example is bookdown::gitbook."
---



# Preface {-}

This is the front page of the book. Probably include a cover image here and abstract/summary.



![Creative Commons License](images/by-nc-sa.png)  
This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/). 

<!--chapter:end:index.rmd-->


# Preface {-}

Outline the structure of the book, introduce ourselves, etc.

Jeffrey Boichuk (<link>) is ... 

Steven Mortimer (<link>) is ... 

<!--chapter:end:00-preface.Rmd-->


# What is Marketing? {#marketing}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

You can label chapter and section titles using `{#label}` after them, e.g., we can reference Chapter \@ref(intro). If you do not manually label them, there will be automatic labels anyway, e.g., Chapter \@ref(methods).

Figures and tables with captions will be placed in `figure` and `table` environments, respectively.


```r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{01-marketing_files/figure-latex/nice-fig-1} 

}

\caption{Here is a nice figure!}(\#fig:nice-fig)
\end{figure}

Reference a figure by its code chunk label with the `fig:` prefix, e.g., see Figure \@ref(fig:nice-fig). Similarly, you can reference tables generated from `knitr::kable()`, e.g., see Table \@ref(tab:nice-tab).


```r
knitr::kable(
  head(iris, 20), caption = 'Here is a nice table!',
  booktabs = TRUE
)
```

\begin{table}

\caption{(\#tab:nice-tab)Here is a nice table!}
\centering
\begin{tabular}[t]{rrrrl}
\toprule
Sepal.Length & Sepal.Width & Petal.Length & Petal.Width & Species\\
\midrule
5.1 & 3.5 & 1.4 & 0.2 & setosa\\
4.9 & 3.0 & 1.4 & 0.2 & setosa\\
4.7 & 3.2 & 1.3 & 0.2 & setosa\\
4.6 & 3.1 & 1.5 & 0.2 & setosa\\
5.0 & 3.6 & 1.4 & 0.2 & setosa\\
\addlinespace
5.4 & 3.9 & 1.7 & 0.4 & setosa\\
4.6 & 3.4 & 1.4 & 0.3 & setosa\\
5.0 & 3.4 & 1.5 & 0.2 & setosa\\
4.4 & 2.9 & 1.4 & 0.2 & setosa\\
4.9 & 3.1 & 1.5 & 0.1 & setosa\\
\addlinespace
5.4 & 3.7 & 1.5 & 0.2 & setosa\\
4.8 & 3.4 & 1.6 & 0.2 & setosa\\
4.8 & 3.0 & 1.4 & 0.1 & setosa\\
4.3 & 3.0 & 1.1 & 0.1 & setosa\\
5.8 & 4.0 & 1.2 & 0.2 & setosa\\
\addlinespace
5.7 & 4.4 & 1.5 & 0.4 & setosa\\
5.4 & 3.9 & 1.3 & 0.4 & setosa\\
5.1 & 3.5 & 1.4 & 0.3 & setosa\\
5.7 & 3.8 & 1.7 & 0.3 & setosa\\
5.1 & 3.8 & 1.5 & 0.3 & setosa\\
\bottomrule
\end{tabular}
\end{table}

You can write citations, too. For example, we are using the **bookdown** package [@R-bookdown] in this sample book, which was built on top of R Markdown and **knitr** [@xie2015].

<!--chapter:end:01-marketing.Rmd-->


# Tools at your Disposal {#tools}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

Here is a review of existing methods.

<!--chapter:end:02-tools.Rmd-->


# Marketing Data Visualizations {#dataviz}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We describe our methods in this chapter.

<!--chapter:end:03-dataviz.Rmd-->


# Preparing and Transforming Data {#transformation}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

Some _significant_ applications are demonstrated in this chapter.

## Example one

## Example two

<!--chapter:end:04-transformation.Rmd-->


# Relational Data {#relational}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

Test

<!--chapter:end:05-relational.Rmd-->


# Measures in Marketing {#measures}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

Test

<!--chapter:end:06-measures.Rmd-->


# Conducting Marketing Field Experiment {#fieldexp}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We have finished a nice book.

<!--chapter:end:07-fieldexp.Rmd-->


# Understanding Marketing Mix {#mix}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We have finished a nice book.

<!--chapter:end:08-mix.Rmd-->


# Pricing and Merchandising {#trade}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We have finished a nice book.

<!--chapter:end:09-trade.Rmd-->


# Machine Learning in Marketing {#machinelearning}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We have finished a nice book.

<!--chapter:end:10-machinelearning.Rmd-->


# Moving from Data to Action {#action}


THINGS PROVIDED BELOW THIS LINE ARE FOR EXAMPLE ONLY. NOT REAL CONTENT

***

We have finished a nice book.

<!--chapter:end:11-action.Rmd-->

