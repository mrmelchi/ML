---
title       : Developing Data Products Course
subtitle    : Course Project  
author      : Mario Melchiori
job         : 25/12/2015
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]     # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
output: 
  html_document: 
    keep_md: yes
---

## Introduction

As part of the Coursera Specialization, it is mandatory first, to create a Shiny application and deploy it on Rstudio server. Second, to use Slidify or Rstudio Presenter to prepare a reproducible pitch presentation about your application. This document accomplishes the second part and contains supporting documentation for  users can start with the application created.

--- .class #id 

## Predict WHITE MALE systolic blood pressure (SBP)

<style>
strong {
  font-weight: bold;
}
</style>

We use a **hypothetical sample**, of 32 **white males** over 40 years old  from the town of **Angina**, to create the model. The dataset is available from [here](https://d396qusza40orc.cloudfront.net/appliedregression/Homeworks/week2-HW-data.csv) 
### Variables
1. **SBP** stand for systolic blood pressure, in mmHg;
2. **QUET** equal to: **$$\ 100 * weight (kgs)/ height (meters)^2 / 703.1$$**
3. **AGE** (Age in years) and;
4. **SMK** = 0 if nonsmoker, **SMK** = 1 if a current or previous smoker.  

The Quetelet Index **QUET** is a historical metric for body mass index **BMI**. 
**BMI = QUET/100 * 703.1 links** **QUET** to **BMI**.   

--- .class #id 

## The prediction algorithm

The prediction algorithm is based on a multivariate linear regression model of the data in dataset using the AGE, SMK and QUET variables.




```r
# fitting linear model
summary(model <- lm(SBP ~ AGE + SMK + QUET,  data= data))$coef
```

```
##              Estimate Std. Error  t value     Pr(>|t|)
## (Intercept) 45.103192 10.7648751 4.189848 0.0002520770
## AGE          1.212715  0.3238192 3.745036 0.0008288266
## SMK          9.945568  2.6560565 3.744486 0.0008300320
## QUET         8.592449  4.4986812 1.909993 0.0664267764
```

--- .class #id 

## Example
New data given by the user, for instance:

```r
Weight <- 86
Height <- 1.73
AGE <- 56
SMK <- 0
QUET <- Weight/Height^2/703.1*100
```

```r
 predict(model,newdata=data.frame(AGE=AGE,SMK=SMK,QUET=QUET),interval = "conf")
```

```
##        fit      lwr     upr
## 1 148.1313 141.9856 154.277
```
We can get the predicted value and lower and upper confidence interval for the predicted value.
### ***Caution:*** We use a hypothetical white male over 40 years old dataset.


