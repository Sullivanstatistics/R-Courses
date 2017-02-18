---
title       : Introduction to R
subtitle    : Importing Data into R
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

# Importing Data into R

--- .class #id

## Ways to get Data into R?

We use

- Built in Data
- .csv, .txt. .xls, ....
- SPSS, SAS, Stata
- Web Scraping
- Databases


--- .class #id

## Built in Data

- R has a wealth of data built in.
- We can use `data()` function to find it


--- .class #id

## Built in Data

- List all Datasets

```r
data()
```
- Specific packages data

```r
data(package="tidyr")
```


--- .class #id

## Delimited Files

- There are many packages out there which handle all of these things. 
- We will stick to using the tidyverse packages. 
- This will provide consistency with all we do. 

--- .class #id

## `readr` in Tidyverse

- `readr` is a collection of many functions
    - `read_csv()`: comma separated (CSV) files
    - `read_tsv()`: tab separated files
    - `read_delim()`: general delimited files
    - `read_fwf()`: fixed width files
    - `read_table()`: tabular files where columns are separated by white-space.
    - `read_log()`: web log files
- `readxl` reads in Excel files. 

--- .class#id





## Example of `readr`

- If we want to read a csv file we could do the following:
- First we will create a simple csv file
- Consider `data`

```r
data
```

```
##   subject sex size
## 1       1   M    7
## 2       2   F   NA
## 3       3   F    9
## 4       4   M   11
```

--- .class #id

## Writing a CSV

- We can write this as a csv


```r
# Write to a file, suppress row names
write.csv(data, "data1.csv", row.names=FALSE)

# Same, except that instead of "NA", output blank cells
write.csv(data, "data2.csv", row.names=FALSE, na="")

# Use tabs, suppress row names and column names
write.table(data, "data3.tab", sep="\t", row.names=FALSE, col.names=FALSE)
```

--- .class #id


## Displaying files


```r
readLines("data1.csv")
```

```
## [1] "\"subject\",\"sex\",\"size\"" "1,\"M\",7"                   
## [3] "2,\"F\",NA"                   "3,\"F\",9"                   
## [5] "4,\"M\",11"
```


--- .class #id


## Displaying files


```r
readLines("data2.csv")
```

```
## [1] "\"subject\",\"sex\",\"size\"" "1,\"M\",7"                   
## [3] "2,\"F\","                     "3,\"F\",9"                   
## [5] "4,\"M\",11"
```



--- .class #id


## Displaying files


```r
readLines("data3.tab")
```

```
## [1] "1\t\"M\"\t7"  "2\t\"F\"\tNA" "3\t\"F\"\t9"  "4\t\"M\"\t11"
```


--- .class #id

## Reading the Data


```r
data1 <- read.csv("data1.csv")
data1
```

```
##   subject sex size
## 1       1   M    7
## 2       2   F   NA
## 3       3   F    9
## 4       4   M   11
```

--- .class #id

## Reading the Data


```r
data2 <- read.csv("data2.csv")
data2
```

```
##   subject sex size
## 1       1   M    7
## 2       2   F   NA
## 3       3   F    9
## 4       4   M   11
```

--- .class #id

## Reading the Data


```r
data3 <- read.delim("data3.tab", sep="\t", header=F)
data3
```

```
##   V1 V2 V3
## 1  1  M  7
## 2  2  F NA
## 3  3  F  9
## 4  4  M 11
```


--- .class #id

## Importing From Other Software

- R can read files from many other software types.
    - SAS
    - Stata
    - SPSS




--- .class #id

## Enter Haven Package

- `haven` is part of tidyverse.
- It contains the functions to read many different files.
- It can also write to those same data types. 

--- .class #id

## For SAS

```
read_sas(data_file, catalog_file = NULL, encoding = NULL)

write_sas(data, path)
```

--- .class #id

## For Stata

```
read_dta(file, encoding = NULL)

read_stata(file, encoding = NULL)

write_dta(data, path, version = 14)
```

--- .class #id

## For SPSS

```
read_sav(file, user_na = FALSE)

read_por(file, user_na = FALSE)

write_sav(data, path)

read_spss(file, user_na = FALSE)
```

--- .class #id

## Other Data Sources

- We will cover other data sources in another course
