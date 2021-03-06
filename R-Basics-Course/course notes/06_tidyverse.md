---
title       : Introduction to R
subtitle    : The Tidyverse!
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
--- .quote .segue .nobackground .dark

<q> <span class = 'white'> The tidyverse is a collection of R packages that share common philosophies and are designed to work together. This site is a work-in-progress guide to the tidyverse and its packages. </span></q>
<q> <span class = 'white'> - tidyverse.org </span></q>

--- .class #id

## What is the tidyverse?

- This is a collection of R packages designed to work well together. 
- There are a core set of functions you almost always use
- **ggplot2**, for data visualisation.
- **dplyr**, for data manipulation.
- **tidyr**, for data tidying.
- **readr**, for data import.
- **purrr**, for functional programming.
- **tibble**, for tibbles, a modern re-imagining of data frames.



--- .class #id

## What is the tidyverse?

- It also install packages that you might need as well. 
- These are broken into categories
    - Data Manipulation
    - Data Import
    - Modeling


--- .class #id    

## Data Import Specific

- **DBI**, for databases.
- **haven**, for SPSS, SAS and Stata files.
- **httr**, for web apis.
- **jsonlite** for JSON.
- **readxl**, for .xls and .xlsx files.
- **rvest**, for web scraping.
- **xml2**, for XML.


--- .class #id

## Data Manipulation Specific 

- **hms**, for times.
- **stringr**, for strings.
- **lubridate**, for date/times.
- **forcats**, for factors.


--- .class #id

## Modeling Specific

- **modelr**, for simple modelling within a pipeline
- **broom**, for turning models into tidy data

--- .class #id

## Installing Packages

- The power of R is the many packages that it has available. 
- These packages contain, functions, data, code, examples,...
- We must learn to install and use them

--- .class #id

## Installing Packages

- The easiest way to install packages is to use the command:
```
install.packages()
```
- For example lets run this on tidyverse

```r
install.packages("tidyverse")
```


--- .class #id

## Calling Installed Packages

- Now that we have installed a package, we must call it in order to use it. 
- To call it we use the `library()` function. 

```r
library(tidyverse)
```

--- &twocol

## What happens when we call?


*** =left

>- Information is Displayed
    - What packages are loaded.
    - What packages conflict with this. 
    - Possible warning messages.
    
    

*** =right


```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```



--- &twocol


## Using Multiple Packages



*** =left

- You can use multiple packages at the same time
- Whatever package is called last may override the previous one.

*** =right



```r
library(MASS)
```

```
## 
## Attaching package: 'MASS'
```

```
## The following object is masked from 'package:dplyr':
## 
##     select
```
