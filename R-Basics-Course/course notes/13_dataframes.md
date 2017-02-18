---
title       : Introduction to R
subtitle    : Dataframes in R
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

# DataFrames in R



--- .class #id



## Dataframe

- With statistics we are most likely to use the data structure called a data frame. 
- This is similar to a matrix in appearance however we can have multiple types of data in it like a list.
- Each column must contain the same type of data or R will most likely default to character for that column. 
- It is very important that you become proficient in working with data frames in order to fully understand data analysis.

--- .class #id

## Creating Data Frames
We usually create a data frame with vectors. 


```r
names <- c("Angela", "Shondra")
ages <- c(27,36)
insurance <- c(TRUE, T)
patients <- data.frame(names, ages, insurance)
patients
```

```
##     names ages insurance
## 1  Angela   27      TRUE
## 2 Shondra   36      TRUE
```

--- .class #id




## Adding Rows or Columns

- We may wish to add rows or columns to our data. 
- We can do this with:
  - ***rbind()*** 
  - ***cbind()*** 

--- .class #id

## Adding Rows or Columns

For example we can go back to our patient data and say we wish to add another patient we could just do the following

```r
l <- c(names="Liu Jie", age=45, insurance=TRUE)
rbind(patients, l)
```

```
## Warning in `[<-.factor`(`*tmp*`, ri, value = "Liu Jie"): invalid factor
## level, NA generated
```

```
##     names ages insurance
## 1  Angela   27      TRUE
## 2 Shondra   36      TRUE
## 3    <NA>   45      TRUE
```

>- This warning serves as a reminder to always know what your data type is.
>- R has read our data in as a factor when we want it as a character. 

--- .class #id

## Adding Rows or Columns


```r
patients$names <- as.character(patients$names)
patients <- rbind(patients, l)
patients
```

```
##     names ages insurance
## 1  Angela   27      TRUE
## 2 Shondra   36      TRUE
## 3 Liu Jie   45      TRUE
```

--- .class #id

## Adding Rows or Columns

Finally if we decided to then place another column of data in we could

```r
# Next appointments
next.appt <- c("09/23/2016", "04/14/2016", "02/25/2016")

#Lets R know these are dates
next.appt <- as.Date(next.appt, "%m/%d/%Y")
next.appt
```

```
## [1] "2016-09-23" "2016-04-14" "2016-02-25"
```

--- .class #id


```r
patients <- cbind(patients, next.appt)
patients
```

```
##     names ages insurance  next.appt
## 1  Angela   27      TRUE 2016-09-23
## 2 Shondra   36      TRUE 2016-04-14
## 3 Liu Jie   45      TRUE 2016-02-25
```

--- .class #id

## Accessing Data Frames

In order to best consider accessing of data frames we will use some built in data from R. 


```r
library(datasets)
titanic <- data.frame(Titanic)
```

--- .class #id

## Variables Included in Titanic


```r
colnames(titanic)
```

```
## [1] "Class"    "Sex"      "Age"      "Survived" "Freq"
```

--- .class #id

## Preview Into Data



```r
titanic[1:2,]
```

```
##   Class  Sex   Age Survived Freq
## 1   1st Male Child       No    0
## 2   2nd Male Child       No    0
```

```r
head(titanic)
```

```
##   Class    Sex   Age Survived Freq
## 1   1st   Male Child       No    0
## 2   2nd   Male Child       No    0
## 3   3rd   Male Child       No   35
## 4  Crew   Male Child       No    0
## 5   1st Female Child       No    0
## 6   2nd Female Child       No    0
```


--- .class #id

## Indexing 

- Indexing is the same as that for matrices. 
- ***head()*** function allows us to access the first rows of the data frame. 
- We can also access data by using both column and row information

--- .class #id

## Indexing


```r
# accessing age information
titanic[,3]
```

```
##  [1] Child Child Child Child Child Child Child Child Adult Adult Adult
## [12] Adult Adult Adult Adult Adult Child Child Child Child Child Child
## [23] Child Child Adult Adult Adult Adult Adult Adult Adult Adult
## Levels: Child Adult
```

```r
#accessing age information using column name
titanic[, "Age"]
```

```
##  [1] Child Child Child Child Child Child Child Child Adult Adult Adult
## [12] Adult Adult Adult Adult Adult Child Child Child Child Child Child
## [23] Child Child Adult Adult Adult Adult Adult Adult Adult Adult
## Levels: Child Adult
```


--- .class #id

## Indexing and Naming

- This means we can access data with a column or row number
- More importantly we can use the name. 
- For large data frames accessing by a name is key.

--- .class #id


## Further Indexing 

Say we want to know information about a particular class

```r
titanic["1st", ]
```

```
##    Class  Sex  Age Survived Freq
## NA  <NA> <NA> <NA>     <NA>   NA
```

--- .class #id

## Further Indexing

We could also ask for information by using the factors that we have as well


```r
first.class.freq <- titanic[titanic$Class=="1st", "Freq"]
first.class.freq
```

```
## [1]   0   0 118   4   5   1  57 140
```

```r
male.freq <- titanic[titanic$Sex=="Male", "Freq"]
male.freq
```

```
##  [1]   0   0  35   0 118 154 387 670   5  11  13   0  57  14  75 192
```

--- .class #id

## Our New Variables


```r
sum(first.class.freq)
```

```
## [1] 325
```

```r
sum(male.freq)
```

```
## [1] 1731
```

--- .class #id

## Adding New Variables 

- Suppose we not only want to know the frequency of survival but the proportion 
- We can ask R to calculate this and add it to our data. 


```r
titanic$surv_p <- titanic$Freq/sum(titanic$Freq)
head(titanic,4)
```

```
##   Class  Sex   Age Survived Freq     surv_p
## 1   1st Male Child       No    0 0.00000000
## 2   2nd Male Child       No    0 0.00000000
## 3   3rd Male Child       No   35 0.01590186
## 4  Crew Male Child       No    0 0.00000000
```

--- .class #id

## Replacing Values 

- Perhaps we were not pleased the decimal places and want to have this as a percentage. 
- We can overwrite the values and change this. 


```r
titanic$surv_p <- titanic$surv_p*100
head(titanic,4)
```

```
##   Class  Sex   Age Survived Freq   surv_p
## 1   1st Male Child       No    0 0.000000
## 2   2nd Male Child       No    0 0.000000
## 3   3rd Male Child       No   35 1.590186
## 4  Crew Male Child       No    0 0.000000
```

