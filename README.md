# top_food_fda_reactions
This is how I created my plot in R for the Data Analytics Capstone Project

---
title: "Top Reactions By Food FDA"
author: "Tilly Wright"
date: "2022-11-17"
output:
  html_document: default
  word_document: default
  pdf_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown

The Top 3 FDA Food Reactions By Year plot was created via R Studio. First, sort and then use the reduce method to find the top 3 reactions for every year.


```{r plotting}
foodFdaFoodIndustry <- read.csv('top_products_industry_name_by_year.csv')

data_sorted <- foodFdaFoodIndustry[order(foodFdaFoodIndustry$count_by_industry_name,
                                         decreasing = TRUE), ]

data_mod <- Reduce(rbind,
                   by(data_sorted,
                      data_sorted["YEAR"],
                      head,
                      n = 3))


```

## Including Plots

Then plot, using the ggplot2 package:

```{r ggplot2, echo=FALSE}
library(ggplot2)

ggplot(data=data_mod) + geom_point(mapping= aes(x=products_industry_name,
                                                y=count_by_industry_name,
                                                color=YEAR)) + theme(axis.text.x = element_text(angle=45)) + labs(title="Top Reactions by Food Industry Products Reported to Food FDA",y = "# of Reactions", x = "Products Industry Name")

install.packages('rmarkdown')
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
