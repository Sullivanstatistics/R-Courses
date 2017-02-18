---
title       : Introduction to R
subtitle    : Getting Help in R
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

# Getting Help in R


--- class $id

## The `help()` Function

- To get online help within an R session we use the `help()` function. 
- For example if we want to create a sequence and know that we can use the function `seq()` but are unsure of the arguments


--- class $id

## Help Function Example


```r
# help() function with seq as argument
help(seq)

# Shortcut for help() is ?
?seq
```

--- class $id

## Further Help Funcion Use

We can also get help on characters and words by placing them in quotations


```r
#Special characters < (all of these display the same information)
help("<")
help('<')
?"<"
?'<'

# Help for words (same use of quotations above work
?"for"
```

--- class $id

## The `example()` Function

- Many times we just need to see some examples rather than read the entire documentation of a function or command.
- In this situation we would use the `example()` function


```r
example(seq)
```

--- class $id

## The `example()` Function

- We can then see numerous examples that R has run for us. 
- The benefit of this command comes when you are interested in seeing examples of graphics, where just seeing the command and not the final product may not be as intuitive for us


```r
#Example of Perspective Plots
example(persp)
```

--- class $id


## The `help.search()` Function

The other help items are great if you know what function you are looking for. Many times we do not know exactly what we are looking for and need to do a more comprehensive search to find a proper function. 


```r
#Search for information about normal
help.search("normal")
```

--- class $id

## Internet Help
Aside from these areas of help another method is to search the internet for further help. Here are some other resources:
  
- [The Comprehensive R Archive Network](https://cran.r-project.org/)
- [UCLA Statistical Computing Help Site](http://www.ats.ucla.edu/stat/r/)
- [Google Search Site](www.google.com)
- [Github](www.github.com)
