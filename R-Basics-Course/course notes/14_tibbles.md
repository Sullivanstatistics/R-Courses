---
title       : Introduction to R
subtitle    : Tibbles in R
author      : Adam J Sullivan
job         : 
license     : by-nc-nd
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
logo        : shield_image.png
biglogo     : shield_image_large.png
knit        : slidify::knit2slides
assets      : {assets: ../../assets}
--- .segue bg:grey

# Tibbles in R



--- .class #id







## Tibbles

Previosly we have worked with data in the form of

- Vectors
- Lists
- Arrays
- Dataframes

--- .class #id


## Tibbles

- *"Tibbles"* are a new modern data frame.  
- It keeps many important features of the original data frame. 
- It removes many of the outdated features. 

--- .class #id

## Compared to Data Frames

- A *tibble* never changes the input type. 
    - No more worry of characters being automatically turned into strings. 
- A tibble can have columns that are lists.
- A tibble can have non-standard variable names.
    - can start with a number or contain spaces. 
    - To use this refer to these in a backtick.
- It only recyles vectors of length 1. 
- It never creates row names.

--- .class #id


## Column-Lists


```r
library(tidyverse)
## Warning: package 'tidyverse' was built under R version 3.3.2
## Warning: package 'ggplot2' was built under R version 3.3.2
## Warning: package 'tidyr' was built under R version 3.3.2
try <- tibble(x = 1:3, y = list(1:5, 1:10, 1:20))
try 
## # A tibble: 3 × 2
##       x          y
##   <int>     <list>
## 1     1  <int [5]>
## 2     2 <int [10]>
## 3     3 <int [20]>


#try <- as_data_frame(c(x = 1:3, y = list(1:5, 1:10, 1:20)))
#try
# Leads to error
```

--- .class #id


## Non-Standard Names


```r
names(data.frame(`crazy name` = 1))
## [1] "crazy.name"
names(tibble(`crazy name` = 1))
## [1] "crazy name"
```

--- .class #id

## Coercing into Tibbles

- A tibble can be made by coercing `as_tibble()`. 
- This works similar to `as.data.frame()`.
- It works efficiently.

--- .class #id


## Coercing into Tibbles



```r
l <- replicate(26, sample(100), simplify = FALSE)
names(l) <- letters

microbenchmark::microbenchmark(
  as_tibble(l),
  as.data.frame(l)
)
## Unit: microseconds
##              expr      min       lq     mean    median        uq      max
##      as_tibble(l)  299.879  337.363  385.665  368.3775  411.6635  775.132
##  as.data.frame(l) 1357.485 1504.300 1747.447 1578.1535 1826.2675 3112.575
##  neval cld
##    100  a 
##    100   b
```

--- .class #id

## Tibbles vs Data Frames

There are a couple key differences between tibbles and data frames. 

- Printing.
- Subsetting. 

--- .class #id

## Printing

- Tibbles only print the first 10 rows and all the columns that fit on a screen. - Each column displays its data type. 
- You will not accidently print too much. 



```r
tibble(
  a = lubridate::now() + runif(1e3) * 86400,
  b = lubridate::today() + runif(1e3) * 30,
  c = 1:1e3,
  d = runif(1e3),
  e = sample(letters, 1e3, replace = TRUE)
)
## # A tibble: 1,000 × 5
##                      a          b     c          d     e
##                 <dttm>     <date> <int>      <dbl> <chr>
## 1  2017-02-18 05:28:37 2017-03-08     1 0.02150370     f
## 2  2017-02-17 22:08:24 2017-03-08     2 0.08031493     k
## 3  2017-02-18 02:03:13 2017-03-07     3 0.11670172     u
## 4  2017-02-18 15:16:10 2017-03-08     4 0.24552337     h
## 5  2017-02-18 00:41:20 2017-03-04     5 0.11232662     b
## 6  2017-02-18 06:26:41 2017-03-08     6 0.52834632     m
## 7  2017-02-18 10:08:57 2017-03-15     7 0.78928491     v
## 8  2017-02-18 13:28:41 2017-03-15     8 0.80388276     h
## 9  2017-02-18 11:35:47 2017-03-18     9 0.45767339     d
## 10 2017-02-18 05:40:18 2017-02-24    10 0.18177950     t
## # ... with 990 more rows
```

--- .class #id



## Subsetting



- We can index a tibble in the manners we are used to
    - `df$x`
    - `df[["x"]]`
    - `df[[1]]`
- We can also use a `pipe` which we will learn about later.
    - `df %>% .$x`
    - `df %>% .[["x"]]`

--- .class #id

## Subsetting


```r
df <- tibble(
  x = runif(5),
  y = rnorm(5)
)

df$x
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
df[["x"]]
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
df[[1]]
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
```

--- .class #id

## Subsetting


```r
df %>% .$x
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
df %>% .[["x"]]
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
df %>% .[[1]]
## [1] 0.6227033 0.7363213 0.8551199 0.9173554 0.5542486
```
