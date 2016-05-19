---
title       : Zodiac Signs
subtitle    : Find out some features of your Zodiac Sign
author      : Elisa Peirano
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Introduction

The App I programmed is very simple to figure out. It only takes one input, which is a date, prefferably the birth date of yourself or somebody you know.

The output displayed is the Zodiac Sign corresponding to the indicated date and some basic features of the sign:

1. the element
2. the colors associated
3. the days of the week more suited 
4. the lucky numbers

--- .class #id 

## Some notes

The Zodiac information I used for this App is from the website: [http://www.astrology-zodiac-signs.com/](http://www.astrology-zodiac-signs.com/)

I build 2 data frames, one with the initial and ending dates for each sign (called zodiac) and another one with the features for each sign (called features).
This is done outside the "function" on Server.R because it is not necessary to re-run it every time the submit button is press or if the App refreshes.

For the outputs, since the calculations are performed when you press the Submit button, it's wrapped in an "eventReactive" fuction.
So the outputs are called via the name of the reactive function (text) and by the specific variable needed for each field from the RenderText function.

---

## Calculating the Zodiac Sign

With the inputted day, month and year I generate a date:

```r
date <- as.Date(paste(as.character(input$year), "-", as.character(input$month), 
    "-", as.character(input$day), sep = ""))
```
And then look for that date in one of the intervals created from the zodiac data frame:

```r
for(i in 1:nrow(zodiac)){
      sequence <- seq(as.Date(zodiac$init_date[i]), as.Date(zodiac$end_date[i]), "day")
      if(date %in% sequence){
        break
      }
}
```

---


## Example

For the example, let's use today's date: 2016-05-19.


```
##    init_date   end_date     sign
## 1 2016-01-20 2016-02-18 AQUARIUS
## 2 2016-02-19 2016-03-20   PISCES
```
Then get the Zodiac Sign

```r
for(i in 1:nrow(zodiac)){
      sequence <- seq(as.Date(zodiac$init_date[i]), as.Date(zodiac$end_date[i]), "day")
      if(date %in% sequence){
        break
      }
}
print(as.character(zodiac$sign[i]), quote = FALSE)
```

```
## [1] TAURUS
```
