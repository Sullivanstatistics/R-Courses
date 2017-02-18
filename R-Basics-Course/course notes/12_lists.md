---
title       : Introduction to R
subtitle    : Matrices in R
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
---  .segue bg:grey

# Lists

--- .class #id

## Lists

- Within R a list is a structure that can combine objects of different types. 
- We will learn how to create and work with lists in this section. 

--- .class #id

## Creating Lists

- A list is actually a vector but it does differ in comparison to the other types of vectors which we have been using in this class.
    - Other vectors are *atomic vectors*
    - A list is a type of vector called a *recursive vector*.

--- .class #id

## An Example Database

We first consider a patient database where we want to store their

- Name
- Amount of bill due
- A Boolean indicator of whether or not they have insurance. 

--- .class #id

## Types of Information

We then have 3 types of information here: 

- character
- numerical
- logical. 

--- .class #id

## Single Patient

To create a list of one patient we say

```r
a <- list(name="Angela", owed="75", insurance=TRUE)
a
```

```
## $name
## [1] "Angela"
## 
## $owed
## [1] "75"
## 
## $insurance
## [1] TRUE
```

--- .class #id

## Indexing
 
- Notice that unlike a typical vector this prints out in multiple parts. 
- This also allows us to help with indexing as we will see below. 
- There is another easy way to create this same list

--- .class #id

## Creating the Same List
 

```r
 a.alt <- vector(mode="list")
 a.alt[["name"]] <- "Angela"
 a.alt[["owed"]] <- 75
 a.alt[["insurance"]] <- TRUE
 
 a.alt
```

```
## $name
## [1] "Angela"
## 
## $owed
## [1] 75
## 
## $insurance
## [1] TRUE
```

--- .class #id

## Lists of Lists
 
- We could then create a list like this for all of our patients. 
- Our database would then be a list of all of these individual lists.

--- .class #id
 
## List Operations 

 
- With vectors, arrays and matrices, there was really only one way to index them. 
- However with lists there are multiple ways:

--- .class #id

## List Indexing


```r
a[["name"]]
```

```
## [1] "Angela"
```

```r
a[[1]]
```

```
## [1] "Angela"
```

```r
a$name
```

```
## [1] "Angela"
```

--- .class #id

## Double vs Single Brackets

- All of the previous are ways to index data in a list. 
- Notice that in two of the above we used double brackets. 
- Next we see the difference between double and single brackets.

--- .class #id

## Double vs Single Brackets


```r
a[1]
```

```
## $name
## [1] "Angela"
```

```r
class(a[1])
```

```
## [1] "list"
```

```r
a[[1]]
```

```
## [1] "Angela"
```

```r
class(a[[1]])
```

```
## [1] "character"
```

--- .class #id

## Double vs Single Brackets

- With the single bracket we are  returned another list.
- With the double bracket we are returned an element in the original class of what kind of data we entered. 
- Depending on your goals you may want to use single or double brackets. 

--- .class #id

## Adding and Subtracting Elements

With a list we can always add more information to it. 

```r
a$age <- 27 
a
```

```
## $name
## [1] "Angela"
## 
## $owed
## [1] "75"
## 
## $insurance
## [1] TRUE
## 
## $age
## [1] 27
```

--- .class #id

## Adding and Subtracting Elements

In order to delete an element from a list we set it to NULL. 


```r
a$owed <- NULL
a
```

```
## $name
## [1] "Angela"
## 
## $insurance
## [1] TRUE
## 
## $age
## [1] 27
```

--- .class #id


## List Components and Values

In order to know what kind of information is included in a list we can look at the ***names()*** function

```r
names(a)
```

```
## [1] "name"      "insurance" "age"
```

--- .class #id

## Unlisting

To find the values of things we could go ahead and unlist them

```r
a.un <- unlist(a)

a.un
```

```
##      name insurance       age 
##  "Angela"    "TRUE"      "27"
```

```r
class(a.un)
```

```
## [1] "character"
```

--- .class #id

## Unlisting

- If There is Character data in the original list that unlisted everything will be in character format. 
- If your list contained all numerical elements than the class would be numerical. 

--- .class #id

## Applying Functions to Lists

- Just like arrays and matrices we can use an ***apply()*** function. 
- Specifically we have ***lapply()*** and ***sapply()*** functions for lists. 
- With the original ***apply()*** function we could specify whether the function was applied to either the rows or the columns. 
- With the case of lists both functions are applied to elements of the list.

--- .class #id

## Applying Functions to Lists


```r
#Number list
n <- list(1:5, 6:37)
n
```

```
## [[1]]
## [1] 1 2 3 4 5
## 
## [[2]]
##  [1]  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28
## [24] 29 30 31 32 33 34 35 36 37
```

--- .class #id

## Applying Functions to Lists

- With this list we see that we have two separate vectors of numbers included. 
- Then let us see the results of either using ***lapply()*** and ***sapply()***

--- .class #id

## Applying Functions to Lists


```r
lapply(n, median)
```

```
## [[1]]
## [1] 3
## 
## [[2]]
## [1] 21.5
```

```r
sapply(n, median)
```

```
## [1]  3.0 21.5
```

--- .class #id

## Apply Functions an Lists


- The ***lapply()*** function returns a list with the median of each of the original lists. 
- While the ***sapply()*** function returns a vector of the medians. 

--- .class #id

## Recursive Lists

- Before it was mentioned that a list is a recursive vector. 
- This is because we can actually have lists within lists. 

--- .class #id

## Recursive Lists

For example let us go back to our patient data. 

```r
s <- list(name="Chandra", insurance="TRUE", age=36)

patients <- list(a,s)
patients
```

```
## [[1]]
## [[1]]$name
## [1] "Angela"
## 
## [[1]]$insurance
## [1] TRUE
## 
## [[1]]$age
## [1] 27
## 
## 
## [[2]]
## [[2]]$name
## [1] "Chandra"
## 
## [[2]]$insurance
## [1] "TRUE"
## 
## [[2]]$age
## [1] 36
```

--- .class #id


## Final Notes on Lists

- It is important to remember how we can call these features of lists. 
- Many of you will want to use R for model building and regressions. 
- You almost never want to use the generated output from R. 
- For example R does not automatically return the confidence intervals with a regression. 

--- .class #id

## Final Notes on Lists

- The output from most regression functions in R is actually a list. 
- What this means is I can extract the elements from the list that I want in order to build tables that display the exact information that I want it to. 
- This is why we take the time to discuss how to search what is in a list and how to access it. 

--- .class #id

##  Example with Output of a List


```r
x <- rnorm(500,10, 3)
y <- 3*x + rnorm(500, 0, 2)
```

--- .class #id

##  Example with Output of a List


```r
fit <- lm(y~x)
fit
```

```
## 
## Call:
## lm(formula = y ~ x)
## 
## Coefficients:
## (Intercept)            x  
##     -0.1676       3.0231
```

--- .class #id

##  Example with Output of a List

- So R just gave me the coefficients back but no other information. 
- This means my knowledge of accessing lists is key. 


```r
names(fit)
```

```
##  [1] "coefficients"  "residuals"     "effects"       "rank"         
##  [5] "fitted.values" "assign"        "qr"            "df.residual"  
##  [9] "xlevels"       "call"          "terms"         "model"
```

--- .class #id

##  Example with Output of a List

- I can see that R actually has a lot more information that they did not display for me. 
- Next I consider a function where it summarizes the information from this model

--- .class #id

##  Example with Output of a List


```r
summary <- summary(fit)
summary
```

```
## 
## Call:
## lm(formula = y ~ x)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -6.2378 -1.3566 -0.1404  1.1708  5.2600 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -0.16761    0.31605   -0.53    0.596    
## x            3.02309    0.03017  100.20   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.982 on 498 degrees of freedom
## Multiple R-squared:  0.9527,	Adjusted R-squared:  0.9526 
## F-statistic: 1.004e+04 on 1 and 498 DF,  p-value: < 2.2e-16
```

--- .class #id

##  Example with Output of a List


```r
names(summary)
```

```
##  [1] "call"          "terms"         "residuals"     "coefficients" 
##  [5] "aliased"       "sigma"         "df"            "r.squared"    
##  [9] "adj.r.squared" "fstatistic"    "cov.unscaled"
```

--- .class #id

## Conclusion of Lists

- R has so much information about regression that is never even displayed unless I dig deeper. 
- Understanding lists and accessing information means you can output custom tables that look much more professional than what R gives you. 
