---
id: 729
title: Why are basics important?
date: 2019-01-08T22:36:08+05:30
author: Achyuthuni Sri Harsha
excerpt: Explains why basics are important using a simple example.
layout: post
guid: https://www.harshaash.com/?p=729
permalink: /why-are-basics-important/
categories:
  - Data Sciences
tags:
  - data analytics
  - data science
  - interval
  - nominal
  - ordinal
  - ratio
  - statistics
---
A lot of my fellow data scientists ask me why they should know the statistics and basics behind their data science models. Frankly, one can survive in the data science world with knowing how to code some classification models. This example is of a mistake I recently did which explains why understanding the basics is important.

Consider I have forecasted the temperature of some object to be 102 degrees centigrade. My friend actually checked the temperature and said that my prediction was 2 percent off. What is the actual temperature of the object?

Well, looking at the percentage of error, 2%, from 102 predicted value, I will calculate that the temperature is 100 degrees centigrade.

<div style="width: 329px" class="wp-caption aligncenter">
  <img loading="lazy" src="https://study.com/cimages/multimages/16/percentageerrorformula.png" alt="Percentage error formula" width="319" height="96" />
  
  <p class="wp-caption-text">
    Percentage error formula
  </p>
</div>

But my friend was from a country where they use Fahrenheit instead of Centigrade, and when I said 102 degrees centigrade, he converted to&nbsp;215.6 degrees fahrenheit.

So according to him, the error of 2% means 211.3 degrees fahrenheit ( which is&nbsp;99.65 degrees centigrade)

So what is the actual temperature? 99.65 centigrade or 100 degrees centigrade?

* * *There are four common levels of data measurement.

  
**1. Nominal:&nbsp;**Numbers representing nominal level data can be used only to classify or categorize.

**2. Ordinal:&nbsp;**In addition to the nominal level&nbsp;capabilities, ordinal-level measurement can be used to rank or order objects. The distances between consecutive numbers need not be the same.

**3. Interval:** Data in which the distances between consecutive numbers have meaning and the data are always numerical are called interval data. In addition, for interval data the zero point is a matter of convention or convenience and not a natural or fixed zero point.

**4. Ratio:** Ratio data have the same properties as interval data, but ratio data have an absolute zero, and the ratio of two numbers is meaningful.

<img src="http://2.bp.blogspot.com/-RR2mrBCYA1c/UMHo6OogZHI/AAAAAAAAB9s/MEr5N5TUa0I/s1600/DataMeasurements.GIF" alt="" itemprop="image" /> 

Each higher level of data can not only be analyzed by the techniques used on lower levels of data but, in addition, can also use other statistical techniques.

Therefore, ratio data can be analyzed by any statistical technique applicable to the other three levels of data plus some others.

Nominal data are the most limited data in terms of the types of statistical analysis that can be used with them.

On ordinal data, any analysis that can be done with nominal data can be used along some additional analysis.

With ratio data, ratio comparisons can be made, and any analysis that can be performed on nominal, ordinal, or interval data can be used.

_Reference:&nbsp;Business Statistics for contemporary decision making &#8211; Ken Black_

* * *

Temperature in centigrade scale is interval data as zero degrees centigrade is just a matter of convention. Error in percentage terms, like MAPE, are statistical methods which can be applied only on Ratio data, and not on interval data.

So 2% error in temperature is not the right way to calculate the error of my prediction.  
This blog post is just one of the many instances of scenarios where everyone needs to understand the basics properly and the statistics behind the models while doing any analysis.