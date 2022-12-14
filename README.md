# Top Food Reactions by FDA 
These are the step that I took to create my plot in R for the Data Analytics Capstone Project.

---
title: Top Reactions By Food FDA

author: Tilly Wright

date: 2022-11-17

Analysis tools include SQL for BigQuery dataset, Tableau for visualization and R Studio for more analysis and plotting.

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

```
You can find the [gplot graph via my Portfolio generated by R Markdown from R Studio - click here.](https://tillywright.com/images/top_reactions_by_food_fda_rmarkdown.html)

To view slide deck for the Google Data Analytics Capstone Project with this gplot embedded, [go to this Google Slides link.](https://docs.google.com/presentation/d/1bAmWur7bIPNSrVIV5aIlh5wk0WmRkIOCUIAI8PK-wTU/edit?usp=sharing)

To view my JavaScript Web Portfolio, [go to this Portfolio link.](https://tillywright.com)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
