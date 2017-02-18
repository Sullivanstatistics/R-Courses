---
title       : Introduction to R
subtitle    : Arrays in R
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

# Arrays in R


--- .class #id

##  Arrays

- Arrays are still a vector in R but they have added extra options to them. 
- We can essentially call them "vector structure". 

--- .class #id


## Array vs Vector

- With a vector we have a list of objects in one dimension. 
- With an array we can have any number of dimensions to our data. 
- *In the Future 2-dimensional array called a matrix.*

--- .class #id

##  Arrays

We can consider a simple vector to start with


```r
x <- c(1,2,3,4)
```

--- .class #id

## Vector into an Array

This means that ***x*** is a vector with 4 elements. This simple vector can be turned into an array by specifying some dimensions on it. 


```r
x.array <- array(x, dim=c(2,2))
x.array
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

--- .class #id

## Big Arrays

- With arrays we have a vector that can then have a vector of dimensional constraints on it. 
- A regular vector has a single dimension. 
- A matrix has 2 dimensions 
- An array can have up to ***n*** dimensions.

--- .class #id


## Characteristics of Arrays


```r
dim(x.array)
```

```
## [1] 2 2
```

```r
is.vector(x.array)
```

```
## [1] FALSE
```

```r
is.array(x.array)
```

```
## [1] TRUE
```

--- .class #id

## Properties of Arrays

We can also have R tell us: 

- Type of elements does our array contain with the ***typeof()*** function.
- The structure of the array with the ***str()*** function. 
- Other attributes with the ***attributes()*** function. 

--- .class #id

## Properties of Arrays


```r
typeof(x.array)
```

```
## [1] "double"
```

```r
str(x.array)
```

```
##  num [1:2, 1:2] 1 2 3 4
```

```r
attributes(x.array)
```

```
## $dim
## [1] 2 2
```


--- .class #id

##  Working with Arrays

- As statisticians it is important to know how to work with arrays. 
- Much of our data will be represented by vectors and arrays.

--- .class #id

##  Indexing Arrays

- Previously we learned how to extract or remove information from vectors. 
- We can also index arrays but our index takes into account all the dimensions of our array

--- .class #id

## Indexing Arrays


```r
#Pulling out an element in the cell in the 1st row and 1st column
x.array[1,1]
```

```
## [1] 1
```

```r
# replacing values in an array

x.array[1,1] <- 5
x.array
```

```
##      [,1] [,2]
## [1,]    5    3
## [2,]    2    4
```

--- .class #id

## Indexing Arrays


```r
#indexing a row
x.array[2,]
```

```
## [1] 2 4
```

```r
#indexing a column
x.array[,1]
```

```
## [1] 5 2
```

--- .class #id

## What Happened?


- We notice here that we lose the array and now it is just a vector. 
- If we wanted to maintain the original array we could go ahead and do the following:

--- .class #id

## Maintaining Arrays


```r
x.array[,1, drop=FALSE]
```

```
##      [,1]
## [1,]    5
## [2,]    2
```

--- .class #id

##  Functions on Arrays

Many functions that are run on an array do not preserve the structure of the array but will take it back down to a vector


```r
which(x.array >= 4)
```

```
## [1] 1 4
```

--- .class #id

## Functions on Arrays

Other functions are designed to work with arrays and preserve the structure of it


```r
y.array <- -x.array
x.array + y.array
```

```
##      [,1] [,2]
## [1,]    0    0
## [2,]    0    0
```

--- .class #id

## Dimensional Functions

Other functions can can act on either the row or the column

```r
rowSums(x.array)
```

```
## [1] 8 6
```

```r
colSums(x.array)
```

```
## [1] 7 7
```


