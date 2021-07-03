---
id: 999
title: Customer Lifetime Value
date: 2019-10-15T11:13:38+05:30
author: Achyuthuni Harsha
excerpt: Customer Lifetime value and steady state retention probability using Markov chains. Markov chains, steady state, homogeneity and Anderson− Goodman test and CLT explained. Used data from UCI m/c learning repository.
layout: post
guid: https://www.harshaash.com/?p=999
permalink: /customer-lifetime-value/
categories:
  - Data Sciences
tags:
  - CLT
  - Customer Lifetime
  - homogeneity
  - Markov
  - Markov chains
  - Retention
  - Steady state
  - UCL
---
 

# Customer Lifetime Value

#### Harsha Achyuthuni

#### 12/10/2019

In this blog, I want to introduce Markov chains and find out the customer lifetime value. Customer Lifetime Value is the net present value (NPV) of the future margin generated from a customer or a customer segment.

## Concept

**Markov Chains**  
In probability theory and statistics, a sequence or other collection of random variables is independent and identically distributed (i.i.d. or iid or IID) if each random variable has the same probability distribution as the others and all are mutually independent.  
We have a set of states, S = {s1, s2,…,sr}. The process starts in one of these states and moves successively from one state to another. Each move is called a step. If the chain is currently in state (s\_i), then it moves to state (s\_j) at the next step with a probability denoted by (p_{ij}) , and this probability does not depend upon which states the chain was in before the current state. 

That is the probability to be present in state j at time _t+1_ is only dependent on the state at time _t_. [ P\_{ij} = P(X\_{t+1} = j | X_{t} = i) ]

**Customer Lifetime Value**  
Customer lifetime value is important because, the higher the number, the greater the profits. You’ll always have to spend money to acquire new customers and to retain existing ones, but the former costs five times as much. When you know your customer lifetime value, you can improve it. 

The customer segments can be represented as states of the Markov chain. Let {0, 1, 2, …, m} be the states of a Markov chain in which states {1, 2,…, m} denote different customer segments and state 0 denotes non-customer state.

The steady-state retention probability is given by [ R\_t = 1 &#8211; frac{pi\_0(1-P\_{00})}{1-pi\_0}] Where (P\_{00}) is the transition probability of State 0, and (pi\_0) is the steady-state distribution for State 0.

Similarly, Customer lifetime value for N periods is given by: [ CLV = sum\_{t=0}^{N} frac{P\_I×P^t×R}{(1+i)^t} ] where PI is the initial distribution of customers in different states, P is the transition probability matrix, R is the reward vector (margin generated in each customer segment). The interest rate is i (discount rate), (d = 1 + frac{1}{1+i}) is the discount factor.

## Data

The data is obtained from the [UCI machine learning repository](http://archive.ics.uci.edu/ml/datasets/online+retail). It is an Online Retail Data Set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers. A sample data is shown below 

<table>
  <caption> raw_data </caption> <tr>
    <th>
      InvoiceNo
    </th>
    
    <th>
      StockCode
    </th>
    
    <th>
      Description
    </th>
    
    <th>
      Quantity
    </th>
    
    <th>
      InvoiceDate
    </th>
    
    <th>
      UnitPrice
    </th>
    
    <th>
      CustomerID
    </th>
    
    <th>
      Country
    </th>
  </tr>
  
  <tr>
    <td>
      566486
    </td>
    
    <td>
      22729
    </td>
    
    <td>
      ALARM CLOCK BAKELIKE ORANGE
    </td>
    
    <td>
      3
    </td>
    
    <td>
      2011-09-13 09:59:00
    </td>
    
    <td>
      3.75
    </td>
    
    <td>
      16098
    </td>
    
    <td>
      United Kingdom
    </td>
  </tr>
  
  <tr>
    <td>
      539337
    </td>
    
    <td>
      21790
    </td>
    
    <td>
      VINTAGE SNAP CARDS
    </td>
    
    <td>
      12
    </td>
    
    <td>
      2010-12-17 10:46:00
    </td>
    
    <td>
      0.85
    </td>
    
    <td>
      NA
    </td>
    
    <td>
      EIRE
    </td>
  </tr>
  
  <tr>
    <td>
      550513
    </td>
    
    <td>
      22969
    </td>
    
    <td>
      HOMEMADE JAM SCENTED CANDLES
    </td>
    
    <td>
      12
    </td>
    
    <td>
      2011-04-18 16:37:00
    </td>
    
    <td>
      1.45
    </td>
    
    <td>
      16928
    </td>
    
    <td>
      United Kingdom
    </td>
  </tr>
  
  <tr>
    <td>
      580736
    </td>
    
    <td>
      22326
    </td>
    
    <td>
      ROUND SNACK BOXES SET OF4 WOODLAND
    </td>
    
    <td>
      6
    </td>
    
    <td>
      2011-12-06 08:55:00
    </td>
    
    <td>
      2.95
    </td>
    
    <td>
      12716
    </td>
    
    <td>
      France
    </td>
  </tr>
  
  <tr>
    <td>
      562339
    </td>
    
    <td>
      23306
    </td>
    
    <td>
      SET OF 36 DOILIES PANTRY DESIGN
    </td>
    
    <td>
      4
    </td>
    
    <td>
      2011-08-04 11:59:00
    </td>
    
    <td>
      1.45
    </td>
    
    <td>
      13571
    </td>
    
    <td>
      United Kingdom
    </td>
  </tr>
</table>

`##   InvoiceNo          StockCode         Description       
##  Length:541909      Length:541909      Length:541909     
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##     Quantity          InvoiceDate                    UnitPrice        
##  Min.   :-80995.00   Min.   :2010-12-01 08:26:00   Min.   :-11062.06  
##  1st Qu.:     1.00   1st Qu.:2011-03-28 11:34:00   1st Qu.:     1.25  
##  Median :     3.00   Median :2011-07-19 17:17:00   Median :     2.08  
##  Mean   :     9.55   Mean   :2011-07-04 13:34:57   Mean   :     4.61  
##  3rd Qu.:    10.00   3rd Qu.:2011-10-19 11:27:00   3rd Qu.:     4.13  
##  Max.   : 80995.00   Max.   :2011-12-09 12:50:00   Max.   : 38970.00  
##                                                                       
##    CustomerID       Country         
##  Min.   :12346    Length:541909     
##  1st Qu.:13953    Class :character  
##  Median :15152    Mode  :character  
##  Mean   :15288                      
##  3rd Qu.:16791                      
##  Max.   :18287                      
##  NA's   :135080` 

As I want to calculate CLV, I want to filter for customers that have done a transaction in Dec 2010 (only they will have enough representation in all states).

Filter for customers that have done a transaction in Dec 2010

`cust_name <- (raw_data %>% 
                filter(month(InvoiceDate) == 12, year(InvoiceDate) == 2010, !is.na(CustomerID) ) %>% 
  dplyr::select(CustomerID) %>% 
  unique())$CustomerID
filtered_data <- raw_data %>% filter(CustomerID %in% cust_name) %>% group_by(InvoiceDate, CustomerID, Country) %>% 
  summarise(no_trans = n(), total_sales = sum(UnitPrice), mean_sales = mean(UnitPrice), total_quantity = sum(Quantity))` For random 10 customers, the total sales and number of items sold across time are shown in a bubble plot.  
<img src="data:image/png;base64,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" width="672" /> 

You can observe that there are gaps between purchases for different customers. ‘Gap’ is the difference in months between two successive purchases or the difference between the current month (despite no purchase) and the last purchase month. The frequency distribution of all the purchases at different gaps is shown below:

<table>
  <caption> Cumulative frequency </caption> <tr>
    <th>
      gap_month
    </th>
    
    <th>
      Count
    </th>
    
    <th>
      cumsum
    </th>
  </tr>
  
  <tr>
    <td>
      0
    </td>
    
    <td>
      489
    </td>
    
    <td>
      51.58228
    </td>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td>
      108
    </td>
    
    <td>
      62.97468
    </td>
  </tr>
  
  <tr>
    <td>
      2
    </td>
    
    <td>
      50
    </td>
    
    <td>
      68.24895
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <td>
      33
    </td>
    
    <td>
      71.72996
    </td>
  </tr>
  
  <tr>
    <td>
      4
    </td>
    
    <td>
      20
    </td>
    
    <td>
      73.83966
    </td>
  </tr>
  
  <tr>
    <td>
      5
    </td>
    
    <td>
      30
    </td>
    
    <td>
      77.00422
    </td>
  </tr>
  
  <tr>
    <td>
      6
    </td>
    
    <td>
      18
    </td>
    
    <td>
      78.90295
    </td>
  </tr>
  
  <tr>
    <td>
      7
    </td>
    
    <td>
      18
    </td>
    
    <td>
      80.80169
    </td>
  </tr>
  
  <tr>
    <td>
      8
    </td>
    
    <td>
      21
    </td>
    
    <td>
      83.01688
    </td>
  </tr>
  
  <tr>
    <td>
      9
    </td>
    
    <td>
      6
    </td>
    
    <td>
      83.64979
    </td>
  </tr>
  
  <tr>
    <td>
      10
    </td>
    
    <td>
      20
    </td>
    
    <td>
      85.75949
    </td>
  </tr>
  
  <tr>
    <td>
      11
    </td>
    
    <td>
      38
    </td>
    
    <td>
      89.76793
    </td>
  </tr>
  
  <tr>
    <td>
      12
    </td>
    
    <td>
      97
    </td>
    
    <td>
      100.00000
    </td>
  </tr>
</table>

From the above distribution, I am assuming that a customer who has not transacted for greater than 6 months is inactive.

## Creating a Markov chain

Loading the libraries required in this section

At 2011-06-01, the state of each customer is given by:

`elapsed_months <- function(end_date, start_date) {
    ed <- as.POSIXlt(end_date)
    sd <- as.POSIXlt(start_date)
    12 * (ed$year - sd$year) + (ed$mon - sd$mon)
}
final_classes <- filtered_data %>% filter(InvoiceDate < date('2011-07-01')) %>%
  group_by(CustomerID) %>% 
  summarise(recent_purchase_date = max(InvoiceDate)) %>% 
  mutate(Class1 = elapsed_months(date('2011-07-01'), date(recent_purchase_date))) %>% 
  mutate(Class1 = as.integer(Class1))
kable(final_classes %>% sample_n(10), align = 'c', caption = 'Initial state') %>% 
   kable_styling(full_width = F)` 

<table>
  <caption> Initial state </caption> <tr>
    <th>
      CustomerID
    </th>
    
    <th>
      recent_purchase_date
    </th>
    
    <th>
      Class1
    </th>
  </tr>
  
  <tr>
    <td>
      14735
    </td>
    
    <td>
      2011-06-16 12:11:00
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      17524
    </td>
    
    <td>
      2010-12-13 14:32:00
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      16385
    </td>
    
    <td>
      2010-12-08 12:56:00
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      18011
    </td>
    
    <td>
      2010-12-01 17:35:00
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      17228
    </td>
    
    <td>
      2011-05-16 10:40:00
    </td>
    
    <td>
      2
    </td>
  </tr>
  
  <tr>
    <td>
      14388
    </td>
    
    <td>
      2011-05-20 16:25:00
    </td>
    
    <td>
      2
    </td>
  </tr>
  
  <tr>
    <td>
      13178
    </td>
    
    <td>
      2011-06-21 14:53:00
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      14533
    </td>
    
    <td>
      2010-12-22 11:07:00
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      16858
    </td>
    
    <td>
      2010-12-08 14:52:00
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      16244
    </td>
    
    <td>
      2011-05-12 10:18:00
    </td>
    
    <td>
      2
    </td>
  </tr>
</table>

Here the states are defined as:

| State | Recency Level | Explanation                                    |
| ----- | ------------- | ---------------------------------------------- |
| 1     | 1             | Last purchase made this month                  |
| 2     | 2             | Last purchase made last month                  |
| 3     | 3             | Last purchase made 2 months ago                |
| 4     | 4             | Last purchase made 3 months ago                |
| 5     | 5             | Last purchase made 4 months ago                |
| 6     | 6             | Last purchase made 5 months ago                |
| 7     | 7-12          | Purchase made 6 months or before (Churn state) |

Similarly the state of the customer at the start of each month is:

<table>
  <caption> States after every month </caption> <tr>
    <th>
      CustomerID
    </th>
    
    <th>
      recent_purchase_date
    </th>
    
    <th>
      Class1
    </th>
    
    <th>
      Class2
    </th>
    
    <th>
      Class3
    </th>
    
    <th>
      Class4
    </th>
    
    <th>
      Class5
    </th>
    
    <th>
      Class6
    </th>
  </tr>
  
  <tr>
    <td>
      14299
    </td>
    
    <td>
      2011-01-27 14:26:00
    </td>
    
    <td>
      6
    </td>
    
    <td>
      7
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      16086
    </td>
    
    <td>
      2011-05-24 12:44:00
    </td>
    
    <td>
      2
    </td>
    
    <td>
      3
    </td>
    
    <td>
      4
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
  </tr>
  
  <tr>
    <td>
      13495
    </td>
    
    <td>
      2011-04-21 15:15:00
    </td>
    
    <td>
      3
    </td>
    
    <td>
      4
    </td>
    
    <td>
      5
    </td>
    
    <td>
      6
    </td>
    
    <td>
      7
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      17581
    </td>
    
    <td>
      2011-06-15 12:50:00
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      18071
    </td>
    
    <td>
      2011-03-27 11:59:00
    </td>
    
    <td>
      4
    </td>
    
    <td>
      5
    </td>
    
    <td>
      6
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      17238
    </td>
    
    <td>
      2011-06-08 10:43:00
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      17525
    </td>
    
    <td>
      2010-12-15 12:05:00
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      16752
    </td>
    
    <td>
      2010-12-02 12:18:00
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      17580
    </td>
    
    <td>
      2011-04-01 12:41:00
    </td>
    
    <td>
      3
    </td>
    
    <td>
      4
    </td>
    
    <td>
      5
    </td>
    
    <td>
      6
    </td>
    
    <td>
      7
    </td>
    
    <td>
      7
    </td>
  </tr>
  
  <tr>
    <td>
      12682
    </td>
    
    <td>
      2011-06-15 10:22:00
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
</table>

I can observe that every customer moves from one class (state) to another state every month (step). According to Markov, the probability of a customer to move to state **j** at any step is only given by the previous state **i**. [ P\_{ij} = P(X\_{t+1} = j | X_{t} = i) ] For each interaction (Class1 to Class 2, month 2 to month 3, Step 3 to step 4), a transaction matrix can be created which has the probability of moving from **i** the state to **j** state. But before I can create the one-step transition probabilities, I need to check whether the sequence of random variables can be approximated to a Markov chain. This is carried out using Anderson− Goodman test which is a chi-square test of independence.

  
The null and alternative hypotheses to check whether the sequence of random variables follows a Markov chain is stated below:  
H0: The sequences of transitions (X1, X2, …, Xn) are independent (zero-order Markov chain)  
HA: The sequences of transitions (X1, X2, …, Xn) are dependent (first-order Markov chain)  
The corresponding test statistic is [ chi^2 = sum\_{i} sum\_{j} (frac{(O\_{ij} -E\_{ij})^2}{E_{jj}}) ] 

The transition probability matrix for the transition form State 1 to 2 is:

`seq_matr <- markovchainFit(final_classes[3:4], method = "mle", name = 'CLT')
seq_matr$estimate` `## CLT 
##  A  7 - dimensional discrete Markov Chain defined by the following states: 
##  1, 2, 3, 4, 5, 6, 7 
##  The transition matrix  (by rows)  is defined as follows: 
##            1         2         3    4         5         6         7
## 1 0.57777778 0.4222222 0.0000000 0.00 0.0000000 0.0000000 0.0000000
## 2 0.42957746 0.0000000 0.5704225 0.00 0.0000000 0.0000000 0.0000000
## 3 0.32000000 0.0000000 0.0000000 0.68 0.0000000 0.0000000 0.0000000
## 4 0.13461538 0.0000000 0.0000000 0.00 0.8653846 0.0000000 0.0000000
## 5 0.18181818 0.0000000 0.0000000 0.00 0.0000000 0.8181818 0.0000000
## 6 0.08333333 0.0000000 0.0000000 0.00 0.0000000 0.0000000 0.9166667
## 7 0.10800000 0.0000000 0.0000000 0.00 0.0000000 0.0000000 0.8920000` 

From the above matrix, P(4,5) = 0.8684211 means that the probability of moving from State 4 to State 5 is 86%. That means that a customer who has not purchased any item in 3 months has a 86% probability of not purchasing any item the next month also.

Similarly the Transition matrix for all the steps is:

`sequenceMatr = list()
for(i in 1:5){
  sequenceMatr[[i]] <- markovchainFit(final_classes[(2+i):(3+i)], method = "map")$estimate@transitionMatrix
}
sequenceMatr` `## [[1]]
##            1         2         3    4         5         6         7
## 1 0.57777778 0.4222222 0.0000000 0.00 0.0000000 0.0000000 0.0000000
## 2 0.42957746 0.0000000 0.5704225 0.00 0.0000000 0.0000000 0.0000000
## 3 0.32000000 0.0000000 0.0000000 0.68 0.0000000 0.0000000 0.0000000
## 4 0.13461538 0.0000000 0.0000000 0.00 0.8653846 0.0000000 0.0000000
## 5 0.18181818 0.0000000 0.0000000 0.00 0.0000000 0.8181818 0.0000000
## 6 0.08333333 0.0000000 0.0000000 0.00 0.0000000 0.0000000 0.9166667
## 7 0.10800000 0.0000000 0.0000000 0.00 0.0000000 0.0000000 0.8920000
## 
## [[2]]
##            1         2         3         4         5         6         7
## 1 0.61309524 0.3869048 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
## 2 0.36184211 0.0000000 0.6381579 0.0000000 0.0000000 0.0000000 0.0000000
## 3 0.39506173 0.0000000 0.0000000 0.6049383 0.0000000 0.0000000 0.0000000
## 4 0.13725490 0.0000000 0.0000000 0.0000000 0.8627451 0.0000000 0.0000000
## 5 0.22222222 0.0000000 0.0000000 0.0000000 0.0000000 0.7777778 0.0000000
## 6 0.11111111 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.8888889
## 7 0.08984375 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.9101562
## 
## [[3]]
##           1         2         3         4         5         6         7
## 1 0.6220238 0.3779762 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
## 2 0.4769231 0.0000000 0.5230769 0.0000000 0.0000000 0.0000000 0.0000000
## 3 0.4020619 0.0000000 0.0000000 0.5979381 0.0000000 0.0000000 0.0000000
## 4 0.3877551 0.0000000 0.0000000 0.0000000 0.6122449 0.0000000 0.0000000
## 5 0.2727273 0.0000000 0.0000000 0.0000000 0.0000000 0.7272727 0.0000000
## 6 0.2000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.8000000
## 7 0.1011673 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.8988327
## 
## [[4]]
##           1         2         3         4         5         6         7
## 1 0.5828877 0.4171123 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
## 2 0.4566929 0.0000000 0.5433071 0.0000000 0.0000000 0.0000000 0.0000000
## 3 0.3823529 0.0000000 0.0000000 0.6176471 0.0000000 0.0000000 0.0000000
## 4 0.2586207 0.0000000 0.0000000 0.0000000 0.7413793 0.0000000 0.0000000
## 5 0.1333333 0.0000000 0.0000000 0.0000000 0.0000000 0.8666667 0.0000000
## 6 0.1875000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.8125000
## 7 0.1042471 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.8957529
## 
## [[5]]
##           1         2         3         4         5         6         7
## 1 0.7118644 0.2881356 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
## 2 0.6666667 0.0000000 0.3333333 0.0000000 0.0000000 0.0000000 0.0000000
## 3 0.4492754 0.0000000 0.0000000 0.5507246 0.0000000 0.0000000 0.0000000
## 4 0.3095238 0.0000000 0.0000000 0.0000000 0.6904762 0.0000000 0.0000000
## 5 0.2790698 0.0000000 0.0000000 0.0000000 0.0000000 0.7209302 0.0000000
## 6 0.2307692 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.7692308
## 7 0.2170543 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.7829457` The Transition Probabilities at various steps seem to follow a pattern. I can do a likelihood ratio test to test the homogeneity of transition matrices. That means I want to find out if the changes in TP across time are random and I can take a constant TP to describe the different TP;s or not.  
The Null and alternative hypothesis is:  
(H\_0 : P\_{ij} (t) = P_{ij})  
(H\_1 : P\_{ij} (t) neq P_{ij}) 

The test statistic for a likelihood ratio test (Chi-square test) is given by [ chi^2 = sum\_{t} sum\_{i} sum\_{j} frac{n(t)[hat P\_{ij}(t)-hat P\_{ij}]^2}{hat P\_{ij}} ] where n(t) is the number of customers in state i at time t. The test statistic follows a (chi^2) distribution with (t − 1) × m × (m − 1) degrees of freedom.

`verifyHomogeneity(sequenceMatr)` `## Testing homogeneity of DTMC underlying input list 
## ChiSq statistic is 0.8694698 d.o.f are 192 corresponding p-value is 1` `## $statistic
## [1] 0.8694698
## 
## $dof
## [1] 192
## 
## $pvalue
## [1] 1` 

As the p-value is greater than the (alpha = 0.05), I am retaining the Null hypothesis that the transition probabilities are homogeneous.

The final TP will be as follows:

`finalTP <- sequenceMatr[[1]]
for(i in 2:5){
  finalTP <- finalTP+sequenceMatr[[i]]
}
finalTP <- finalTP/5
CLT.mc <- new('markovchain', 
                  # states = colnames(finalTP),
                  transitionMatrix = finalTP,
                  name = 'CLT')
CLT.mc` `## CLT 
##  A  7 - dimensional discrete Markov Chain defined by the following states: 
##  1, 2, 3, 4, 5, 6, 7 
##  The transition matrix  (by rows)  is defined as follows: 
##           1         2         3         4        5         6         7
## 1 0.6215298 0.3784702 0.0000000 0.0000000 0.000000 0.0000000 0.0000000
## 2 0.4783404 0.0000000 0.5216596 0.0000000 0.000000 0.0000000 0.0000000
## 3 0.3897504 0.0000000 0.0000000 0.6102496 0.000000 0.0000000 0.0000000
## 4 0.2455540 0.0000000 0.0000000 0.0000000 0.754446 0.0000000 0.0000000
## 5 0.2178342 0.0000000 0.0000000 0.0000000 0.000000 0.7821658 0.0000000
## 6 0.1625427 0.0000000 0.0000000 0.0000000 0.000000 0.0000000 0.8374573
## 7 0.1240625 0.0000000 0.0000000 0.0000000 0.000000 0.0000000 0.8759375` 

The Markov chain can be visualized as follows:

`plotmat(t(CLT.mc@transitionMatrix), box.size = 0.05)` 

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABUAAAAPACAMAAADDuCPrAAAAmVBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrY6AAA6OgA6Ojo6OmY6ZpA6ZrY6kNtmAABmOgBmOjpmZjpmZmZmkLZmkNtmtttmtv+QOgCQOjqQZjqQkDqQttuQ2/+2ZgC2Zjq2kGa229u22/+2//++vr7bkDrbkGbbtmbbtpDb25Db27bb2//b////tmb/25D/27b/29v//7b//9v///9uinb9AAAACXBIWXMAAB2HAAAdhwGP5fFlAAAgAElEQVR4nO2de4Octvlw2di14/iaN7XTtN04yU6dX+L12jvf/8O9A8NFQuL2IAldzvmjdRiQkPTorAAhqjMAAIiojj4BAIBUQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIECAAhBoAAAQhAoAIAQBAoAIASBAgAIQaAAAEIQKACAEAQKACAEgQIACEGgAABCECgAgBAECgAgBIEC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" width="672" /> 

The initial frequency of the classes are:

`initial_freq <- (final_classes %>% group_by(Class1) %>% summarise(frequency = n()/nrow(final_classes)))$frequency
initial_freq` `## [1] 0.37974684 0.14978903 0.07911392 0.05485232 0.03481013 0.03797468
## [7] 0.26371308` 

As TP is the transition probability between states, I can find the number of people in each state at any time _t_ using the following formula:

[u^{(n)} = uP^{(n)}]

From the TP, the frequency in the first stage is compared with the actual frequency at the 1st stage.

`## # A tibble: 7 x 3
##   Class2 actual_frequency predicted_frequency
##    <dbl>            <dbl>               <dbl>
## 1      1           0.354               0.236 
## 2      2           0.160               0.0567
## 3      3           0.0854              0     
## 4      4           0.0538              0     
## 5      5           0.0475              0     
## 6      6           0.0285              0     
## 7      7           0.270               0` 

Similarly for 3rd stage

`## # A tibble: 7 x 3
##   Class4 actual_frequency predicted_frequency
##    <dbl>            <dbl>               <dbl>
## 1      1           0.395               0.409 
## 2      2           0.134               0.153 
## 3      3           0.0717              0.0787
## 4      4           0.0612              0.0458
## 5      5           0.0316              0.0360
## 6      6           0.0338              0.0285
## 7      7           0.273               0.249` 

I can observe that a Markov chain can be used to find the number of people in each state after each stage. So the probability of people in each class after n steps is given below:

`## [1] "n = 1"
##              1         2          3          4          5          6
## [1,] 0.3984503 0.1437229 0.07813888 0.04827924 0.04138312 0.02722729
##              7
## [1,] 0.2627984
## [1] "n = 14"
##              1         2          3          4         5          6
## [1,] 0.4260002 0.1610742 0.08392567 0.05113945 0.0385104 0.03005181
##              7
## [1,] 0.2092984
## [1] "n = 34"
##             1         2          3          4          5          6
## [1,] 0.427639 0.1618467 0.08442764 0.05152099 0.03886892 0.03040108
##              7
## [1,] 0.2052957
## [1] "n = 39"
##              1         2          3          4          5        6
## [1,] 0.4276527 0.1618532 0.08443183 0.05152418 0.03887192 0.030404
##              7
## [1,] 0.2052623
## [1] "n = 43"
##              1        2          3          4          5          6
## [1,] 0.4276567 0.161855 0.08443306 0.05152511 0.03887279 0.03040485
##              7
## [1,] 0.2052525
## [1] "n = 51"
##             1         2          3          4          5          6
## [1,] 0.427659 0.1618562 0.08443378 0.05152566 0.03887331 0.03040535
##              7
## [1,] 0.2052467
## [1] "n = 59"
##              1         2         3          4         5          6
## [1,] 0.4276594 0.1618563 0.0844339 0.05152575 0.0388734 0.03040544
##              7
## [1,] 0.2052457
## [1] "n = 68"
##              1         2          3          4          5          6
## [1,] 0.4276595 0.1618564 0.08443393 0.05152577 0.03887341 0.03040545
##              7
## [1,] 0.2052456
## [1] "n = 82"
##              1         2          3          4          5          6
## [1,] 0.4276595 0.1618564 0.08443393 0.05152577 0.03887341 0.03040546
##              7
## [1,] 0.2052455
## [1] "n = 87"
##              1         2          3          4          5          6
## [1,] 0.4276595 0.1618564 0.08443393 0.05152577 0.03887341 0.03040546
##              7
## [1,] 0.2052455` 

I can observe that as ‘n’ is increasing, the frequency of customers is tending towards constant. This constant is called steady state frequency. The steady state probability is :

`steady.state.prob <- steadyStates(CLT.mc)
steady.state.prob` `##              1         2          3          4          5          6
## [1,] 0.4276595 0.1618564 0.08443393 0.05152577 0.03887341 0.03040546
##              7
## [1,] 0.2052455` 

The probability change with steps can be visualized as below:<img src="data:image/png;base64,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" width="672" /> 

## Customer Lifetime value Now that I established that the customer segments can be represented as a Marcov chain, I can compute the customer lifetime value.

  
The monetary value at each state is `revenue_in_states <- filtered_data %>% left_join(final_classes, by = 'CustomerID') %>%
  filter(InvoiceDate < date('2011-07-01')) %>%
  dplyr::select(Class1, total_sales) %>%
  group_by(Class1) %>%
  summarise(avg_revenue = mean(total_sales))
kable(revenue_in_states, align = 'c', caption = 'States after steps') %>% 
   kable_styling(full_width = F)` 

<table>
  <caption> States after steps </caption> <tr>
    <th>
      Class1
    </th>
    
    <th>
      avg_revenue
    </th>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td>
      56.51656
    </td>
  </tr>
  
  <tr>
    <td>
      2
    </td>
    
    <td>
      56.17425
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <td>
      56.45380
    </td>
  </tr>
  
  <tr>
    <td>
      4
    </td>
    
    <td>
      44.33256
    </td>
  </tr>
  
  <tr>
    <td>
      5
    </td>
    
    <td>
      46.58667
    </td>
  </tr>
  
  <tr>
    <td>
      6
    </td>
    
    <td>
      49.00257
    </td>
  </tr>
  
  <tr>
    <td>
      7
    </td>
    
    <td>
      52.82802
    </td>
  </tr>
</table>

The steady-state retention probability is given by [ R\_t = 1 &#8211; frac{pi\_0(1-P\_0)}{1-pi\_0}] Where (P\_{00}) is the transition probability of the null state (State 7), and (pi\_0) is the steady state distribution of the Null state (State 7). Substituting I get:

`## [1] 0.9679608` Similarly Customer lifetime value for 5 periods is given by: [ CLV = sum\_{t=0}^{5} frac{P\_I×P^t×R}{(1+i)^t} ] where PI is the initial distribution of customers in different states, P is the transition probability matrix, R is the reward vector (margin generated in each customer segment). The interest rate is i (discount rate), (d = 1 + frac{1}{1+i}=0.95) is the discount factor.  
Substituting, I get: `CLT <- 0
for(k in 0:5){
  CLT = CLT + (0.95^k)*(initial_freq %*% (CLT.mc@transitionMatrix^k) %*% revenue_in_states$avg_revenue)
}
CLT` `##          [,1]
## [1,] 484.3484` 

Therefore the customer lifetime value is 484.34.

* * *Created by Achyuthuni Sri Harsha

  
References:  
1. Business Analytics: The Science of Data-Driven Decision Making [Available](https://www.wileyindia.com/business-analytics-the-science-of-data-driven-decision-making.html)  
2. Introduction to probability, Charles M. Grinstead and J. Laurie Snell, [Available](http://www.dartmouth.edu/~chance/teaching_aids/books_articles/probability_book/book.html)  
3. CS294 Markov Chain Monte Carlo: Foundations & Applications (lecture by Prof. Alistair Sinclair in Fall 2009) [Available](https://people.eecs.berkeley.edu/~sinclair/cs294/n2.pdf)  
4. Computer Science Theory for the Information Age, Spring 2012 (course material) [Available](https://www.cs.cmu.edu/~venkatg/teaching/CStheory-infoage/)  
6. Customer Analytics at Flipkart.com [Available](https://hbsp.harvard.edu/product/IMB555-PDF-ENG)  
5. IIMB BAI Class notes and practice problems