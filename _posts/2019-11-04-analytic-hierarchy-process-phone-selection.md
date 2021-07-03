---
id: 1041
title: Analytic Hierarchy Process
date: 2019-11-04T02:01:55+05:30
author: Achyuthuni Harsha
excerpt: A multi criteria decision of selecting a phone is explained using AHP.
layout: post
guid: https://www.harshaash.com/?p=1041
permalink: /analytic-hierarchy-process-phone-selection/
image: /wp-content/uploads/2019/11/PCM.png
categories:
  - Data Sciences
tags:
  - AHP
  - analytic
  - decision
  - hierarchy
  - multi criteria
  - process
---
The analytic hierarchy process (AHP), developed by Thomas L. Saaty, is designed to solve complex multi-criteria decision problems. AHP requires the decision maker to provide judgments about the relative importance of each criterion and then specify a preference for each decision alternative using each criterion. The output of AHP is a prioritized ranking of the decision alternatives based on the overall preferences expressed by the decision maker.

To introduce AHP I want to consider a purchasing problem I have faced recently. I had to buy a new phone, so I went to a nearby mall. After searching in a lot of stores, I have narrowed down my list to the below 4 phones.<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/Phones.png" alt="" width="1417" height="151" /> The following criteria are relevant in my selection of phone (in the order of importance):

  
1. Battery  
2. Price  
3. Performance  
4. Reviews  
5. Recency  
6. Display  
7. Radiation  
8. Brand  
9. Camera 

Data regarding&nbsp;_reviews_,&nbsp;_price_&nbsp;and&nbsp;_battery_&nbsp;is simple. But some other factors are subjective like&nbsp;_brand_&nbsp;and&nbsp;_display_. The advantage of AHP is that it can handle situations in which the unique subjective judgments of the individual decision maker constitute an important part of the decision-making process.

### Developing the Hierarchy

The first step in AHP is to develop a graphical representation of the problem in terms of the overall goal, the criteria to be used, and the decision alternatives. Such a graph depicts the hierarchy for the problem.

Using AHP, I will specify the relative importance of each of the nine criteria in terms of its contribution to the achievement of the overall goal. At the next level, I will indicate a preference for each decision alternative based on each criterion. Finally the information is synthesized on the relative importance of the criteria and the preferences for the decision alternatives to provide an overall priority ranking of the decision alternatives.<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/AHP-Phone-1.png" alt="AHP for phone" width="1980" height="1921" />

### Establishing priorities using AHP

AHP uses pairwise comparison matrix to show the priorities of a decision. This will measure the relative degree to which each option of the pair accomplishes this specific criterion. It is a square NxN matrix, where N is the number of options that we have, in this case 9. The values of this matrix should be filled using the following scale.<img loading="lazy" src="https://i0.wp.com/upload.wikimedia.org/wikipedia/commons/f/f4/AHPFundamentalScaleModerately.png?zoom=1.25&resize=522%2C332&ssl=1" srcset="https://i0.wp.com/upload.wikimedia.org/wikipedia/commons/f/f4/AHPFundamentalScaleModerately.png?zoom=1.25&resize=495%2C315&ssl=1" alt="Scale of importance" width="495" height="315" />

### Pairwise Comparisons

In establishing the priorities for the nine criteria, I will give a score to each criterion relative to each other criterion when the criteria are compared two at a time (pairwise) using the above scale.<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/PCM.png" alt="PCM" width="717" height="244" />

_Performance_&nbsp;is further divided into&nbsp;_Processor, Max-Speed_&nbsp;and&nbsp;_Storage_. Similarly&nbsp;_Camera_&nbsp;and&nbsp;_Display_&nbsp;are also further divided. The pairwise comparison matrices for&nbsp;_Performance, Camera_&nbsp;and&nbsp;_Display_&nbsp;are as follows:<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/Performance.png" alt="" width="689" height="217" />

### Synthesization

The priorities for each of the criterion are obtained by the eigenvalues of the PCM matrix. The priorities of each of the criterion are as follows:<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/weights.png" alt="" width="590" height="244" />

Combining the above priorities, the priority for the factor&nbsp;_Inches of display_&nbsp;is the priority of display \* priority of Inch = 0.05\*0.666 = 0.033.

### Comparison of each criterion between phones

A Pairwise comparison matrix comparing phones is generated for every criterion. For example, by using&nbsp;_Battery_&nbsp;as a factor to understand the weights, the comparison of battery capacity between phones would be:&nbsp;_Galaxy M30s > Oppo A9 2020> Vivo S1 > Redmi note 7 Pro_. The difference between&nbsp;_Samsung Galaxy M30s_&nbsp;and&nbsp;_Oppo A9_&nbsp;is around 1000MAh but the difference between&nbsp;_Vivo S1_&nbsp;and&nbsp;_RedmiNote7_ Pro is only 500MAh. This is captured in the pairwise comparison matrix:<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/Battery-1.png" alt="" width="766" height="120" />

Similar matrices are created for each of the other metrics.

### Overall Priority Ranking

The procedure used to compute the overall priority is to weight each phone’s weight (shown for factor&nbsp;_Battery_&nbsp;above) by the corresponding criterion priority. For example, the phone&nbsp;_Vivo S1_&nbsp;has a weight of 0.20 for battery while the factor&nbsp;_Battery_&nbsp;has a priority of 0.31. The total priority would be 0.2*0.31 = 0.061 for battery of&nbsp;_Vivo S1_. To obtain the overall priority of the&nbsp;_Vivo S1_, we need to make similar computations for all the other criteria and then add the values for that particular item to obtain the overall priority.

The overall priority ranking of all the phones is:<img loading="lazy" src="https://www.harshaash.com/wp-content/uploads/2019/11/Overall-Weights.png" alt="" width="236" height="123" />

From the overall priority, I will select&nbsp;_Vivo S1_. A different person who might give different weights or priorities would choose a different phone.

AHP is used in many places for taking decisions which have many criterion. It is used extensively in NASA, XEROX, Walmart, US Navy, IBM etc. It can be used for selecting among different choices, prioritization, resource allocation, bench-marking, quality management etc.. Refer&nbsp;[The Analytic Hierarchy Process – An Exposition](https://pubsonline.informs.org/doi/abs/10.1287/opre.49.4.469.11231?journalCode=opre)&nbsp;for more.

### References

  1. An Introduction to Management Science : Quantitative Approach to Decision Making &#8211; Anderson, Sweeney &#8211; [[link](https://www.cengage.co.in/category/higher-education/business-economics/operation-decision-sciences/management-science/an-introduction-to-management-science-quantitative-approach-to-decision-making-wcd-96)]
  2. Business Analytics: The Science of Data-Driven Decision Making _ Dinesh Kumar &#8211; [[link](https://www.wileyindia.com/business-analytics-the-science-of-data-driven-decision-making.html)]
  3. The Analytic Hierarchy Process—An Exposition &#8211; Foreman and Gass &#8211; [[link](https://pubsonline.informs.org/doi/abs/10.1287/opre.49.4.469.11231?journalCode=opre)]

  4. Decision making with the analytic hierarchy process &#8211; Thomas L. Saaty &#8211; [[link](http://www.rafikulislam.com/uploads/resourses/197245512559a37aadea6d.pdf)]

&nbsp;