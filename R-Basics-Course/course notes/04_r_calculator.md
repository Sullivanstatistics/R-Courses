---
title       : Introduction to R
subtitle    : Using R as a Calculator
author      : Adam J Sullivan
job         : 
license     : by-nc-nd
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : solarized_light
widgets     : [mathjax, quiz, bootstrap, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
logo        : shield_image.png
biglogo     : shield_image_large.png
knit        : slidify::knit2slides
assets      : {assets: ../../assets}
---  .segue bg:grey

# Using R as a Calculator


---  .class #id




## Arithmetic Operators

Operator        |   Description
--------------- | --------------------
`+`             |    Addition 
`-`             |   Subtraction
`*`             |    Multiplication
`/`             |    Division
^ or `**`       |    Exponentiation

---  .class #id

## R as a Calculator

The most simple procedures that we can do in R is using R as a calculator. For example:


```r
# Addition
5+4
```

```
## [1] 9
```

```r
# Subtraction
124 - 26.82 
```

```
## [1] 97.18
```

---  .class #id

## R as a Calculator


```r
# Multiplication
5*4
```

```
## [1] 20
```

```r
# Division
35/8
```

```
## [1] 4.375
```

---  .class #id

## More Math in R

R works simply as a calculator but also can be used for more advanced operations as well. 


```r
# Exponentials
3^(1/2)
```

```
## [1] 1.732051
```

```r
# Exponential Function
exp(1.5)
```

```
## [1] 4.481689
```

---  .class #id

## More Math in R


```r
# Log base e
log(4.481689)
```

```
## [1] 1.5
```

```r
# Log base 10
log10(1000)
```

```
## [1] 3
```

---  .class #id

## Logical Operators

Once we have used some basic arithmetic operators we move into logic. 


 Operator  |  Description
---------- | ------------------------------
  `<`      |  Less Than
  `>`      |    Greater Than
  `<=`     |   Less Than or Equal To
  `>=`     |    Greater Than or Equal To
 `==`     |  Exactly Equal To
 `!=`      |   Not Equal To
 `!a`      |  Not `a`
 `a&b`    |  `a` **AND** `b`


--- .class #id

## Logic in R Example 

We can then see an example of this:


```r
a <- c(1:12)
# a>9 OR a<4
# Gives us 1 2 3 10 11 12

#Having R do this
a
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10 11 12
```

```r
a>9
```

```
##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
## [12]  TRUE
```

--- .class #id

## Logic in R Example


```r
a<4
```

```
##  [1]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [12] FALSE
```

```r
a>9 | a<4
```

```
##  [1]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
## [12]  TRUE
```

```r
a[a>9 | a<4]
```

```
## [1]  1  2  3 10 11 12
```

--- .class #id

## Further Operators

Some other operators we may want to use are listed below


Description                |  R Symbol  |    Example
-------------------------- | ---------- | -----------------------
 Comment                  |    #        |  \# This is a comment
 Assignment               |     `<-`       |   x `<-` 5
 Assignment                |    `->`       |  5 `->` x
 Assigment                |    `=`        |  x `=` 5
 Concatenation operator    |  c          |  c(1,2,4)
 Modular                  |    \%\%     |      25 \%\% 6
 Sequence from a to b by h |   seq       |   seq(a,b,h)
 Sequence Operator          |    :      |     0:3

--- .class #id

## Math Functions in R

We also have access to a wide variety of mathematical functions that are already built into R. 

  Description               |    R Symbol
--------------------------- | ------------------
Square Root                 |    `sqrt`
`floor(x)`                 |    `floor` 
`\ceil(x)`                |   `ceiling`
Logarithm                   |    `log`
Exponential function, `e^x`  |   `exp`
Factorial, `!`                |  `factorial`
