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

# Matrices in R


--- .class #id


## Matrices

- A **Matrix** is a vector that also contains information on the number of rows and number of columns. 
- However vectors are not matrices.

--- .class #id

## Creating Matrices

- An important first step with matrices is to learn how to create them. 
- One of the easiest ways to do this is with the ***matrix()*** function.

--- .class #id


## Creating Matrices


```r
x <- c(1,2,3,4)
#Creating it by start with filling rows first
x.mat <- matrix(x, nrow=2, ncol=2, byrow=TRUE)
x.mat
```

```
##      [,1] [,2]
## [1,]    1    2
## [2,]    3    4
```

--- .class #id

## Creating Matrices


```r
#Creating it by start with filling columns first
x.mat2 <- matrix(x, nrow=2, ncol=2, byrow=FALSE)
x.mat2
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```


--- .class #id

## Creating Matrices


```r
y <- c(1,2,3,4,5,6,7)
y.mat <- matrix(y, ncol=2)
```

```
## Warning in matrix(y, ncol = 2): data length [7] is not a sub-multiple or
## multiple of the number of rows [4]
```

```r
y.mat
```

```
##      [,1] [,2]
## [1,]    1    5
## [2,]    2    6
## [3,]    3    7
## [4,]    4    1
```

--- .class #id

## Recycling

- Notice in the above example that we did not have enough elements in our vector to full fill out the matrix so we have recycled back to the first element to fill in the final cell. 


--- .class #id

## Diagonal Matrices

We can also create diagonal matrices from a vector

```r
x.mat3 <- diag(x)
x.mat3
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    0    0    0
## [2,]    0    2    0    0
## [3,]    0    0    3    0
## [4,]    0    0    0    4
```

--- .class #id

## Matrix Operations

- R can be a great tool for working with matrices. 
- Many operations we need to do with linear algebra can be done in R. 
- A small selection of these follows:

--- .class #id

## Matrix Operations


```r
#element-wise multiplication
x.mat * x.mat2
```

```
##      [,1] [,2]
## [1,]    1    6
## [2,]    6   16
```

```r
# Matrix multiplication
x.mat %*% x.mat2
```

```
##      [,1] [,2]
## [1,]    5   11
## [2,]   11   25
```

--- .class #id


## Matrix Operations



```r
# Matrix Transpose
t(x.mat)
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
#Extract diagonal
diag(x.mat3)
```

```
## [1] 1 2 3 4
```

--- .class #id


## Matrix Operations


```r
#Inverse Function
solve(x.mat)
```

```
##      [,1] [,2]
## [1,] -2.0  1.0
## [2,]  1.5 -0.5
```

```r
#check inverse
x.mat %*% solve(x.mat)
```

```
##      [,1]         [,2]
## [1,]    1 1.110223e-16
## [2,]    0 1.000000e+00
```

--- .class #id

## The ***apply()** Function

- Many times we wish to use our own function over the elements of a matrix. 
- The ***apply()*** function allows someone to use an R function or user-defined function with a matrix. 
- This function is

***apply(m, dimcode, f, arguments)***

--- .class #id

## The ***apply()** Function


- ***m***: matrix you wish to use.
- ***dimcode*** 
    - 1 if you want to apply function to rows
    - 2 if you want to apply to columns
- ***f***: function you wish to use
- ***arguments***: specific arguments for function being used. 

--- .class #id

## Apply Example

- We begin with our matrix ***y.mat***. 
- We can use the apply function to get means of either the columns or the rows. 


```r
apply(y.mat, 1, mean)
```

```
## [1] 3.0 4.0 5.0 2.5
```

```r
apply(y.mat,2,mean)
```

```
## [1] 2.50 4.75
```

--- .class #id

## Naming Rows and Columns of Matrices

Consider the following matrices where we have recorded both weight(lbs) and height(inches) of subjects at time point 1. 


```r
time1 <- matrix( c(115, 63, 175, 69, 259, 57, 325, 70), ncol=2, byrow=TRUE)
time1
```

```
##      [,1] [,2]
## [1,]  115   63
## [2,]  175   69
## [3,]  259   57
## [4,]  325   70
```

--- .class #id

## Second Measurement

We then have another measurement at time point 2. 


```r
time2 <- matrix( c(120, 63, 175, 69, 224, 57, 350, 70), ncol=2, byrow=TRUE)
time2
```

```
##      [,1] [,2]
## [1,]  120   63
## [2,]  175   69
## [3,]  224   57
## [4,]  350   70
```

--- .class #id

## Why the need for names?


- Without the story behind these we do not know what kind of data we have here or what is being measured. 
- This is where it can be very important to name both the columns and the rows of data. 

--- .class #id


## Naming in Matrices


```r
#Names for Time 1
colnames(time1) <- c("weight1", "height1")
rownames(time1) <- c("Subject 1", "Subject 2", "Subject 3", "Subject 4")
time1
```

```
##           weight1 height1
## Subject 1     115      63
## Subject 2     175      69
## Subject 3     259      57
## Subject 4     325      70
```

--- .class #id

## Naming in Matrices


```r
#Names for Time 2
colnames(time2) <- c("weight2", "height2")
rownames(time2) <- c("Subject 1", "Subject 2", "Subject 3", "Subject 4")
time2
```

```
##           weight2 height2
## Subject 1     120      63
## Subject 2     175      69
## Subject 3     224      57
## Subject 4     350      70
```
