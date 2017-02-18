---
title       : Introduction to R
subtitle    : Data Objects in R
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

# Data Objects in R

--- .class #id

## Now That we Can Import Data



We begin with a look at different kinds of data

- **Booleans**: Direct binary values: `TRUE` or `FALSE` in R. 
- **Integers**: Whole numbers or number that can be written without fractional component, represented by a fixed-length block of bits.

--- .class #id

## Data Objects

- **Characters**: fixed length block of bits with special coding.
- **Strings**: Sequence of characters.
- **Floating Point Numbers**: a fraction times an exponent, like $1.34x10^7$, however in R you would see `1.34e7`. 
- **Missing**: `Na`, `NaN`, $\ldots$

--- .class #id

## Finding Type of Data

With types of data, R, has a built in way to help one determine the type that a certain piece of data is stored as. these consist of the following functions:


- **typeof()** this function returns the type
- **is.`typ`()** functions return Booleans for whether the argument is of the type ***typ***
- **as.`typ`()** functions try to change the argument to type ***typ***

--- .class #id

## Examples of Type


```r
typeof(7)
```

```
## [1] "double"
```

```r
is.numeric(7)
```

```
## [1] TRUE
```

--- .class #id


## Examples of Type


```r
is.na(7)
```

```
## [1] FALSE
```

```r
is.na(7/0)
```

```
## [1] FALSE
```

--- .class #id

## Examples of Type


```r
is.na(0/0)
```

```
## [1] TRUE
```

```r
7/0
```

```
## [1] Inf
```

```r
0/0
```

```
## [1] NaN
```

--- .class #id


## Examples of Type


```r
is.character(7)
```

```
## [1] FALSE
```

```r
is.character("7")
```

```
## [1] TRUE
```

--- .class #id

## Coercing Data Types


```r
as.character(5/6)
```

```
## [1] "0.833333333333333"
```

```r
as.numeric(as.character(5/6))
```

```
## [1] 0.8333333
```

--- .class #id

## Equality of Data


```r
6*as.numeric(as.character(5/6))
```

```
## [1] 5
```

```r
5/6 == as.numeric(as.character(5/6))
```

```
## [1] FALSE
```

--- .class #id

## What Happened?

>- What we can see happening here is a problem in the precision of what R has stored for a number. 
>- This can also occur when performing arithmetic operations on values as well.

--- .class #id

## A Closer Look


```r
5/6 - as.numeric(as.character(5/6))
```

```
## [1] 3.330669e-16
```



--- .class #id

## Further Tries at Equality


```r
0.45 == 3*0.15
```

```
## [1] FALSE
```

```r
0.45-3*0.15
```

```
## [1] 5.551115e-17
```

```r
0.4 - 0.1 == 0.5 - 0.2
```

```
## [1] FALSE
```

--- .class #id

## `all.equal()` Function

When comparing numbers that we have performed operations on it is better to use the `all.equal()` function.

--- .class #id

## Example


```r
all.equal(0.45, 3*0.15)
```

```
## [1] TRUE
```

```r
all.equal(0.4-0.1, 0.5-0.2)
```

```
## [1] TRUE
```
