---
id: 916
title: Part and partial correlation
date: 2019-08-01T10:23:53+05:30
author: Achyuthuni Sri Harsha
excerpt: 'Understanding part (semi partial) and partial correlation coefficients in multiple regression model. Deriving the multiple R-Squared and beta coefficients from basics. Inspired from Business Analytics: The Science of Data-Driven Decision Making by Dinesh Kumar.'
layout: post
guid: https://www.harshaash.com/?p=916
permalink: /part-and-partial-correlation/
categories:
  - Data Sciences
tags:
  - beta
  - correlation
  - linear
  - part
  - partial
  - R-Square
  - regression
---
 

# Part and partial correlation Date: 31-07-2019

  
Author: Achyuthuni Sri Harsha 

## Introduction

The concept of partial correlation and part correlation plays an important role in regression model building. I always had a confusion between the two. In this post, I would like to explore the difference between the two and understand how and where they are used.

The data and the problem statement along with explanation of the different kinds of correlation coefficients can be found from the textbook [Business Analytics: The Science of Data-Driven Decision Making](https://www.wileyindia.com/business-analytics-the-science-of-data-driven-decision-making.html). This post is largely inspired from the Example problem 10.1 found in Multiple linear regression chapter in the book.

The cumulative television ratings(CTRP), money spent on promotions(P) and advertisement revenue for 38 different television programmed are given in the data.

The summary statistics for the data is:

`##       CTRP             P                R          
##  Min.   : 90.0   Min.   : 75600   Min.   : 904776  
##  1st Qu.:117.2   1st Qu.:108000   1st Qu.:1106700  
##  Median :128.0   Median :126000   Median :1202532  
##  Mean   :125.8   Mean   :131779   Mean   :1200763  
##  3rd Qu.:136.0   3rd Qu.:150300   3rd Qu.:1294809  
##  Max.   :156.0   Max.   :208800   Max.   :1457400` 

There are two factors that explain R, namely P and CTRP. I want to see individually how much they will be able to explain the total variance in (y). The total proportion of the variation in (y) explained by (x) is given by R square value of the regression. The R square and (beta) values for both the independent variables when taken individually are as follows:

`## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -229572  -80536   -3601   67967  297182 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   621672     141428   4.396 0.000127 ***
## CTRP            4603       1113   4.135 0.000263 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 113300 on 30 degrees of freedom
## Multiple R-squared:  0.3631, Adjusted R-squared:  0.3418 
## F-statistic:  17.1 on 1 and 30 DF,  p-value: 0.0002629
## 
## [1] "----------------------------------------------------------------------------------------------------"
## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -218735  -88210   12298   63999  185209 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 8.774e+05  8.247e+04   10.64 1.06e-11 ***
## P           2.527e+00  6.208e-01    4.07 0.000315 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 107600 on 30 degrees of freedom
## Multiple R-squared:  0.3558, Adjusted R-squared:  0.3343 
## F-statistic: 16.57 on 1 and 30 DF,  p-value: 0.0003146
## 
## [1] "----------------------------------------------------------------------------------------------------"` 

The outcome is as follows: For CTRP [Y = 677674 + 4175CTRP + epsilon\_{CTRP} qquad Eq(1)] where (epsilon\_{CTRP}) is the unexplained error due to CTRP.

Similarly, for P, [ Y = 87740 + 2.527P + epsilon\_{P} qquad Eq(2)] where (epsilon\_{P}) is the unexplained error due to P From the above outcome, I observe the following:

  
1. The total proportion of variation in (y) explained by CTRP and P individually are 28.15% and 35.58% respectively. (From R-square in the above results)  
2. The (beta) coefficients of CTRP and P are 4175 and 2.527 respectively. That means for every unit change in CTRP, the revenue increases by 4175 units while for every change in P the revenue increases by 2.527 units. If both CTRP and P are independent, then I would think that if I tried to use both the variables in the model, then  
1. The total explainable variation in (y) should be 28.15 + 35.58 = 63.73%. That means the model’s R square should be 0.6373  
2. The (beta) coefficients should be same as before 

Lets build a regression model using both these variables. In this model, the (y) variable (Revenue R) is explained using P (promotions) and CTRP. The output is shown below.

`## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -125839  -25848    5388   26146  180440 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 4.101e+04  9.096e+04   0.451    0.655    
## CTRP        5.932e+03  5.766e+02  10.287 4.02e-12 ***
## P           3.136e+00  3.032e-01  10.344 3.47e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 57550 on 35 degrees of freedom
## Multiple R-squared:  0.8319, Adjusted R-squared:  0.8223 
## F-statistic: 86.62 on 2 and 35 DF,  p-value: 2.793e-14` 

The outcome is as follows: [Y = 41018 + 5932CTRP + 3.136P + epsilon qquad Eq(3) ] where (epsilon) is the unexplained error. The total R-squared is 0.8319 which means that the total proportion of variation in (y) explained is 83.19%. We were expecting a r-squared of 0.6373. Even the (beta) of CTRP is 5932 which was 4175 before. That means that for every one unit change in CTRP, 5932 units of Revenue will change (keeping P constant), instead of 4175 as we thought before.

  
So what is happening here? Consider the following Venn diagram:  
<img src="data:image/png;base64,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" width="672" /> 

In the above diagram, the gold color is Y while the cornflower blue is CTRP and firebrick is Promotion. The area in circles show the variation in the variables. The intersection of 2 circles shows the variation explained in one variable by another variable. I want to understand two things.

  
1. The increase in R squared due to addition of a variable. Assuming that the variable P already exists in the model, I would like to see how adding CTRP will change the R square value  
2. How do I get the (beta) value of CTRP in the combined model (Equation 3). The (beta_{CTRP}) is nothing but the change when all other variables are kept constant, in this case when promotion is kept constant 

### Part or semi partial correlation

Part of semi partial correlation explains how much additional variation is explained by including a new parameter. If Promotion was already existing in the model, and I introduce CTRP, the variance explained by CTRP alone would be C/(A+E+G+C).

To get the same I should remove the ‘G’ part in the above diagram. That can be achieved by removing the influence of promotion in CTRP and then doing a regression of the remaining part (B + C) with (y).

The correlation coefficient when effect of other variables are removed from (x) but not from (y) is called as semi partial or part correlation coefficient.

The result of regression promotion with CTRP is as follows:

`## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -39.131  -6.563   0.545   7.558  26.869 
## 
## Coefficients:
##               Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  1.417e+02  1.156e+01  12.253 2.09e-14 ***
## P           -1.201e-04  8.532e-05  -1.408    0.168    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 16.63 on 36 degrees of freedom
## Multiple R-squared:  0.05219,    Adjusted R-squared:  0.02586 
## F-statistic: 1.982 on 1 and 36 DF,  p-value: 0.1677` 

[ CTRP = 141.7 -0.0001P + epsilon\_{P-CTRP} qquad Eq(4)] where (epsilon\_{P-CTRP}) is the unexplained error in CTRP due to P (B and C part).

The regression R-square of the unexplained error in CTRP with Y should give me the variation explained because of CTRP only.

`## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -218369  -66614  -11444   61728  279858 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 1200762.6    15746.4  76.256  < 2e-16 ***
## e_ctrp_p       5931.9      972.6   6.099 5.13e-07 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 97070 on 36 degrees of freedom
## Multiple R-squared:  0.5082, Adjusted R-squared:  0.4945 
## F-statistic:  37.2 on 1 and 36 DF,  p-value: 5.126e-07` 

[ Y = 1200762.6 +5931.9epsilon_{P-CTRP} + epsilon qquad Eq(5)] where (epsilon) is the unexplained error in Y due to CTRP alone (G, E and A part).

From here I can infer that an additional 50% of the variation in y is explained by adding CTRP variable. This is called as the semi partial or part correlation. The sum of r-squared when p alone is present in the model (variation explained in y due to P (Equation 2) ie: E and G part in the Venn diagram) and the part correlation R-squared when CTRP is added in the model (variation explained only by CTRP removing P ie: C part in Venn diagram) is close to the total R-Squared when both the variables are present in the model(equation 3). (see<sup>i</sup>)

### Partial correlation

I want to understand how much Revenue changes with CTRP keeping Promotions constant ((beta_{CTRP}) in Equation 3), to do this, I should remove the effect of P from both Y(revenue) and promotion. The correlation coefficient I get from removing the effect of all other variables in both (y) and (x) is called partial correlation coefficient. In the above Venn diagram, it is C/(C+A)

`## 
## Call:
## lm(formula = .outcome ~ ., data = dat)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -125839  -25848    5388   26146  180440 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 2.067e-10  9.205e+03    0.00        1    
## e_ctrp_p    5.932e+03  5.686e+02   10.43 1.98e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 56740 on 36 degrees of freedom
## Multiple R-squared:  0.7515, Adjusted R-squared:  0.7446 
## F-statistic: 108.9 on 1 and 36 DF,  p-value: 1.977e-12` 

[ epsilon\_{P} = 2*10^{-10} +5932epsilon\_{P-CTRP} + epsilon qquad Eq(6)] Note that the regression coefficient (beta\_{P-CTRP}) from Equation 6 is nothing but the effect of CTRP keeping P constant. Therefore it is same as the partial regression coefficient (beta\_{CTRP}) in the combined equation Equation 3. References:

  
1. Kumar, U. Dinesh. [Business Analytics: The Science of Data-driven Decision Making](https://www.wileyindia.com/business-analytics-the-science-of-data-driven-decision-making.html). Wiley India, 2017.  
2. Cohen, Patricia, Stephen G. West, and Leona S. Aiken. Applied multiple regression/correlation analysis for the behavioral sciences. Psychology Press, 2014. (and related [notes](https://www3.nd.edu/~rwilliam/stats1/x93b.pdf))  
3. Venn diagrams in R from [scriptsandstatistics.wordpress.com](https://scriptsandstatistics.wordpress.com/2018/04/26/how-to-plot-venn-diagrams-using-r-ggplot2-and-ggforce/) 

* * *

  1. In this example the values are not exactly equal to each other because of [suppresser variable](https://stats.stackexchange.com/questions/9930/does-it-make-sense-for-a-partial-correlation-to-be-larger-than-a-zero-order-corr)