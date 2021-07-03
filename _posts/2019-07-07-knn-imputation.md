---
id: 879
title: KNN imputation
date: 2019-07-07T19:47:21+05:30
author: Achyuthuni Harsha
excerpt: Handling missing values in original mtcars data set by imputation using KNN algorithm.
layout: post
guid: https://www.harshaash.com/?p=879
permalink: /knn-imputation/
categories:
  - Data Sciences
tags:
  - cars
  - imputation
  - knn
  - mtcars
  - 'null'
  - R
  - R language
  - StatLib
  - UCI Machine learning
---
# Missing value imputation using KNN

#### Harsha Achyuthuni

#### 07/07/2019

## Problem

Real world data is not always clean. Its often messy and contains unexpected/missing values. In this post I will use a non-parametric algorithm called k-nearest-neighbors (KNN) to replace missing values.

### Data

The data is technical spec of cars. I have taken this data set from [UCI Machine learning repository](https://archive.ics.uci.edu/ml/datasets/auto+mpg) which in turn took it form StatLib library which is maintained at Carnegie Mellon University. The data set was used in the 1983 American Statistical Association Exposition.

<table>
  <caption> Sample Data </caption> <tr>
    <th>
      mpg
    </th>
    
    <th>
      cylinders
    </th>
    
    <th>
      displacement
    </th>
    
    <th>
      horsepower
    </th>
    
    <th>
      weight
    </th>
    
    <th>
      acceleration
    </th>
    
    <th>
      year
    </th>
    
    <th>
      origin
    </th>
    
    <th>
      name
    </th>
  </tr>
  
  <tr>
    <td>
      12.0
    </td>
    
    <td>
      8
    </td>
    
    <td>
      429
    </td>
    
    <td>
      198
    </td>
    
    <td>
      4952
    </td>
    
    <td>
      11.5
    </td>
    
    <td>
      73
    </td>
    
    <td>
      1
    </td>
    
    <td>
      mercury marquis brougham
    </td>
  </tr>
  
  <tr>
    <td>
      19.0
    </td>
    
    <td>
      6
    </td>
    
    <td>
      225
    </td>
    
    <td>
      95
    </td>
    
    <td>
      3264
    </td>
    
    <td>
      16.0
    </td>
    
    <td>
      75
    </td>
    
    <td>
      1
    </td>
    
    <td>
      plymouth valiant custom
    </td>
  </tr>
  
  <tr>
    <td>
      26.4
    </td>
    
    <td rowspan="2">
      4
    </td>
    
    <td>
      140
    </td>
    
    <td>
      88
    </td>
    
    <td>
      2870
    </td>
    
    <td>
      18.1
    </td>
    
    <td>
      80
    </td>
    
    <td>
      1
    </td>
    
    <td>
      ford fairmont
    </td>
  </tr>
  
  <tr>
    <td>
      18.0
    </td>
    
    <td>
      121
    </td>
    
    <td>
      112
    </td>
    
    <td>
      2933
    </td>
    
    <td>
      14.5
    </td>
    
    <td>
      72
    </td>
    
    <td>
      2
    </td>
    
    <td>
      volvo 145e (sw)
    </td>
  </tr>
  
  <tr>
    <td>
      19.8
    </td>
    
    <td>
      6
    </td>
    
    <td>
      200
    </td>
    
    <td>
      85
    </td>
    
    <td>
      2990
    </td>
    
    <td>
      18.2
    </td>
    
    <td>
      79
    </td>
    
    <td>
      1
    </td>
    
    <td>
      mercury zephyr 6
    </td>
  </tr>
</table> The data set contains the following columns:

  
1. mpg: continuous (miles per gallon)  
2. cylinders: multi-valued discrete 3. displacement: continuous (cu. inches)  
4. horsepower: continuous  
5. weight: continuous(lbs.)  
6. acceleration: continuous (sec.)  
7. model year: multi-valued discrete (modulo 100)  
8. origin: multi-valued discrete (1. American, 2. European, 3. Japanese)  
9. car name: string (unique for each instance) 

Now I want to find if this data set contains any abnormal values.

`summary(cars_info)` `##       mpg          cylinders      displacement     horsepower   
##  Min.   : 9.00   Min.   :3.000   Min.   : 68.0   Min.   : 46.0  
##  1st Qu.:17.50   1st Qu.:4.000   1st Qu.:104.0   1st Qu.: 75.0  
##  Median :23.00   Median :4.000   Median :146.0   Median : 93.5  
##  Mean   :23.52   Mean   :5.458   Mean   :193.5   Mean   :104.5  
##  3rd Qu.:29.00   3rd Qu.:8.000   3rd Qu.:262.0   3rd Qu.:126.0  
##  Max.   :46.60   Max.   :8.000   Max.   :455.0   Max.   :230.0  
##                                                  NA's   :5      
##      weight      acceleration        year       origin 
##  Min.   :1613   Min.   : 8.00   Min.   :70.00   1:248  
##  1st Qu.:2223   1st Qu.:13.80   1st Qu.:73.00   2: 70  
##  Median :2800   Median :15.50   Median :76.00   3: 79  
##  Mean   :2970   Mean   :15.56   Mean   :75.99          
##  3rd Qu.:3609   3rd Qu.:17.10   3rd Qu.:79.00          
##  Max.   :5140   Max.   :24.80   Max.   :82.00          
##                                                        
##              name    
##  ford pinto    :  6  
##  amc matador   :  5  
##  ford maverick :  5  
##  toyota corolla:  5  
##  amc gremlin   :  4  
##  amc hornet    :  4  
##  (Other)       :368` I find that horsepower contains 5 NA values. I can ignore the data points with horsepower NA, or I could impute the NA values using KNN or other methods. Before imputing, I want to make a strong case that my imputation would be right.  


<table>
  <caption> Cars with missing horsepower </caption> <tr>
    <th>
      mpg
    </th>
    
    <th>
      cylinders
    </th>
    
    <th>
      displacement
    </th>
    
    <th>
      weight
    </th>
    
    <th>
      acceleration
    </th>
    
    <th>
      year
    </th>
    
    <th>
      origin
    </th>
    
    <th>
      name
    </th>
  </tr>
  
  <tr>
    <td>
      25.0
    </td>
    
    <td>
      4
    </td>
    
    <td>
      98
    </td>
    
    <td>
      2046
    </td>
    
    <td>
      19.0
    </td>
    
    <td>
      71
    </td>
    
    <td>
      1
    </td>
    
    <td>
      ford pinto
    </td>
  </tr>
  
  <tr>
    <td>
      21.0
    </td>
    
    <td>
      6
    </td>
    
    <td>
      200
    </td>
    
    <td>
      2875
    </td>
    
    <td>
      17.0
    </td>
    
    <td>
      74
    </td>
    
    <td>
      1
    </td>
    
    <td>
      ford maverick
    </td>
  </tr>
  
  <tr>
    <td>
      40.9
    </td>
    
    <td>
      4
    </td>
    
    <td>
      85
    </td>
    
    <td>
      1835
    </td>
    
    <td>
      17.3
    </td>
    
    <td>
      80
    </td>
    
    <td>
      2
    </td>
    
    <td>
      renault lecar deluxe
    </td>
  </tr>
  
  <tr>
    <td>
      23.6
    </td>
    
    <td>
      4
    </td>
    
    <td>
      140
    </td>
    
    <td>
      2905
    </td>
    
    <td>
      14.3
    </td>
    
    <td>
      80
    </td>
    
    <td>
      1
    </td>
    
    <td>
      ford mustang cobra
    </td>
  </tr>
  
  <tr>
    <td>
      34.5
    </td>
    
    <td>
      4
    </td>
    
    <td>
      100
    </td>
    
    <td>
      2320
    </td>
    
    <td>
      15.8
    </td>
    
    <td>
      81
    </td>
    
    <td>
      2
    </td>
    
    <td>
      renault 18i
    </td>
  </tr>
</table> The assumption behind using KNN for missing values is that a point value can be approximated by the values of the points that are closest to it, based on other variables.

  
Let me take three variables from the above data set, mpg, acceleration and horsepower. Intuitively, these variables seem to be related. `ggplot(cars_info, aes(x = mpg, y = acceleration, color = horsepower)) + 
  geom_point(show.legend = TRUE) +
  labs(x = 'Mpg', y='Acceleration',  title = "Auto MPG",
       color = 'Horsepower') + 
  scale_color_gradient(low = "green", high = "red",
                       na.value = "blue", guide = "legend") +
  theme_minimal()+theme(legend.position="bottom")` 

<img src="data:image/png;base64,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u4esJD6Xcq5NSA8+nx4vxtTOpUjsPD3LmBUC7R6yktQX6Km1nECHr6aLg360leNPdl4dljErBNo9ZCVhRfoQmKxqKbNiEqlzyEqCQENgsqrlzIo2pq7pKKutCa7HEagGBrqeJc2KRvqO6SarrVsrDIpANTDQ9ZCVHrLS00lWW7dWGRSBamCg6yErPWSlp4ustm6tNCgC1cBA10NWeshKDwKVINAQmKyKrPSQlR4EKkGgITBZFVnpISs9CFSCQENgsiqy0kNWephEkiDQEJisiqz0kJUe2pgkCDQEJqsiKz1kpYdGegkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npaSWrcxPqPQOBamCg6yErPWSlp42szj23tkERqAYGuh6y0kNWelrI6txz6xsUgWpgoOshKz1kpSd+Vuee62FQBKqBga6HrPSQlR4EKkGgITBZFVnpISs9CFSCQENgsiqy0kNWehCoBIGGwGRVZKWHrPQwiSRBoCEwWVW0rN6e4P/s1cqqGSaroo1JgkBDYLKqWFm9/e2NDLpSWTXEZFU00ksQaAhMVhUpq7e/vZlBVymrppisiqwkCDQEJquKk9Xb397QoCuUVWNMVkVWEgQaApNVIVA9jCs9ZCVBoCEwWRUC1cO40kNWEgQaApNVIVA9jCs9ZCVBoCEwWRWTSHoYV3rISoJAQ2CyKtqY9DCu9JCVBIGGwGRVNNLrYVzpISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npIStJPIGeAABYMloTaBT4108PWekhKz1kJUGgITBZFVnpISs9ZCVBoCEwWRVZ6SErPWQlQaAhMFkVWekhKz1kJUGgITBZFVnpISs9ZCVBoCEwWVUXWe1PqPiVbrLamuB4mHGlh6wkCDQEJqvqIKv9+6sN2klWW7e6Dcq40kNWEgQaApNVtZ/V/v0Kg3aR1datFQZlXOkhKwkCDYHJqlrPav9+jUE7yGrr1iqDMq70kJUEgYbAZFU2BLotIfdbCFSPyarISoJAQ2CyKhMC3bZt3qAIVI/JqshKgkBDYLIqCwLdtm3BoAhUj8mqyEqCQENgsioDk0jbti0alEkkPSarIisJAg2ByaoMtDFZEShtTAEhKwkCDYHJqgw00psRKI304SArCQINgcmqDGRlR6AVGMiqCJNVkZUEgYbAZFUWsrIxiVSNhawKMFkVWUkQaAi6qerWBMfDJrIy0cZUjYmsFjFZFVlJEGgIOqnq1lvdBrWRlYVG+mpsZLWAyarISoJAQ9BFVbfeWmFQstJDVnrISoJAQ9BBVbfeWmVQstJDVnrISoJAQ4BA9VisakdC1zUUYTErxlUOBBoCBKrHYFU7dhg1qMGsGFd5EGgIEKgee1Xt2GHVoPayGjKu8iDQEDCJpMdcVTt2mDWouaxSuh5X5yYU/BiBauh655VAG5Mec1Uh0Hp0PK7OPbfYoAhUA1IQ9KGRfhFzVSHQenQ7rs49t8SgCFQDUtBDVjoQaD06HVfnnltmUASqASnoISslZv1pMKshAs2DQENgsiqy0mLVnxazQqB5EGgITFZFVmqM+tNkVgg0BwINgcmqyEoPWelhEkmCQENgsiqy0kNWemJmVdLjOf8rtDH5wkDXQ1Z6yEpPxKzK5LjwSwU/RqAaGOh6yEoPWemJl1Xp6bkGBKqBga6HrPSQlZ5oWZVPEGlAoBoY6HrISg9Z6UGgEgQaApNVkZUestKDQCUINAQmqyIrPWSlB4FKEGgITFZFVnrISg+TSBIEGgKTVZGVHrLS03UbUwkIVAMDXQ9Z6SErPR030peBQDUw0PWQlR6y0kNWEgQaApNVkZUestJDVhIEGgKTVZGVHrLSQ1YSBBoCk1WRlR6y0kNWEgQaApNVkZUestJDVhIEGgKTVZGVHrLSQ1YSBBoCk1WRlR6y0kNWEgQaApNVkZUestJDVhIEGgKTVZGVHrLSQ1YSBNqc3Qm+zz2UUP7ovgTfLdvMyj3Q35DQWiGSBlltTwhYSQ6Te7CH4yoiCLQxu3f7G/TQIZdB9+1rYlCLWQ2dA/0Nb+jKoP5Zbd8e0aAm92D/xlVMEGhTdu/2N+ihQy6D7tvXyKAGs0opr+oNb+jMoN5Zbd8e06Am92DvxlVUEGhDdu/2N+ihQy6D7tvXzKD2ssooreoNb+jOoL5Zbd8e1aAm92DfxlVcEGhDEGhNEKgek3uwb+MqLgi0IQi0JghUj8k92LdxFRcE2hAEWhMEqsfkHuzbuIoLAm0Kk0j1YBJJj8k92LtxFRUE2hjamGpBG5Mek3uwf+MqJgi0OTTS14FGej0m92APx1VEEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUkQaAhMVkVWOtJzcLLSQ1YSBBoCk1WRlYrRLJC1qkaYrIpxJUGgITBZFVlpiNuH1BBjWY1gXEkQaAhMVkVWCiJ3wjfEVlZjGFcSBBoCk1WRlQIEWhvGlQSBhsBkVWSlAIHWhnElQaAhMFkVWSlAoLVhXEkQaAhMVtXDrNYTWitkhGV/Mq5qgEA1sPP09C+r9fXODNq7rLqjf+MqJgg0BCar6l1W6+udGbR3WXUIWUkQaAhMVtW3rNbXOzLosH9ZdQlZSRBoCExW1besmgv0ugTPonqWVZeQlQSBhsBkVX3LqrFAr7vO26B9y6pLyEqCQENgsqq+ZdVUoNdd52/QvmXVJWQlQaAhMFlV77IK408vg/Yuqw4hKwkCDYHJqvqXVYATeAQaHbKSINAQmKyqh1k1nUFCoC1AVhIEGgKTVa1YVgi0JchKgkBDYLKqVcuKSaR2ICsJAg2ByapWLivamFqBrCQINAQmq1q9rGikbwOykiDQEJisiqz0kJUespIg0BCYrIqs9JCVHrKSINAQmKyq66z2JxT8eFbVxxPaK8dJ11mVYLIqspIg0BCYrKrjrPbvLzbotKqPf9yOQRlXeshK4iXQ3//12trFH/np6JvT39i5tjb5JjbsPD3dZrV/f4lBJ1V9/OOGDMq40kNWEh+B/ngt4+Jvpd+8fkP2zTt+FriwYth5ejrNav/+MoOOq/r4xy0ZlHGlh6wkHgI9tXbx3wyHr941kubRtUt+mn5zyR+C11YAO08PAtXDuNJDVpL6Aj1919pn0/8nh57J/1/ZmWn09RtGx6OxYefpQaB6GFd6yEpSX6Cv3zA+XT+69rHh8Om1d2XfPJ1+Ex92nh4EqodxpYesJA1m4TOBHh0djibn9e8KVJETdp4eJpH09Hxc7UiIWoik51kFxl+g2Vn76bvGp+6v7Jz/EPQErDQjfzp+YeTP1upZYnZkdF3FihBMoNnJOwKFMir8OTJoS7UsNTt2YND2CCXQU1kbkxBoK41MnD7oISs9fc5qx5TY5Yzoc1bh8RXoqZ0Xpx9+Oo5Ao8DO00NWevqcFQLN6JdAnx630SPQDJNVkZWePmeFQDN6JdAfr03aPpmFTzFZFVnp6XNWCDSjRwI9fXTtnZMPPCf9n/SBmoOs9PQ6q3b92e+sguMj0KPiuk2uREoxWRVZ6el3Vq36s+dZhcZDoE/L695P37X2Tq6FN1kVWenpeVY00vdIoOPll1LSjz1fZTUmpFAHk1WRlR6yktQX6Km1nECHr34j+eojrRx/svPqQFZ6yEoPWUlYkT4EJqtasaxuTfB+clFWexMa1BMCk3twxcZVBQg0BCarWq2sbr21iUELstq7t3uDmtyDqzWuqkCgITBZ1UpldeutjQy6mNXevQYManIPrtS4qgSBhsBkVauU1a23NjPoQlZ791owqMk9uErjqhoE2pzdCV3XsEjJXYXHdFdzNwJ9Y0L509cT8j9BoKWYfA8iUB0Wd97u3RYNWnZX4REd1tyJQN/4RpdB19cXDIpAS7H4HhwiUB0Gd97u3RYNWrogfEaXNXch0De+0WXQ9fVFgyLQUgy+B1MQqAZ7O2/3bosGLb8lUUqnNXcwifTGN7oMur7uMmiEWvWYG+0p9t6DGQhUg72dh0Br0kEbk49ARRvTJxPqF7Q1of6z8vhntT2h6auXYO89mIFANdjbeQi0Jh000nsJdCj9Wd+gW7cGMKh3Vtu3xzOovfdgBgLVYG/nIdCadLAH/QQ65pOf9DHo1q0hDOqb1fbtEQ1q7z2YgUA1GNx5Fv25cpNIFdSfRJryyU/6GHTr1iAG9cxq+/aYBjX4HkxBoBos7jyL/ly1NqYqarcxTUGg81h8Dw4RqA6TO8+iP1eskb6Suo30UxDoPCbfgwhUBztPD1npKc8Kgc7DuJIg0BB0WdWdCYUPkJUeR1bl/nQZavUmkSI2TqlAoBqQwjx33llmULLS48rK5c8qgzYty/eJ7bcxxXxFFQhUA1KY4847Sw1KVnqcWbn86TZo47K8n9l2I33UY14VCFQDUshz553lBiUrPfWzivs545jeZNVKGm4QqAakkAeBhgGB6kGgEgQaAgSqx2RVCFQPApUg0BAgUD0mq0KgehCoBIGGgEkkPSar8siqDWP0J6vO/YlAVZiUwqGEOM+9PUF8+9WE+V8p9WeTm1TGu05pc0Kd35d/3LaE8BVlOMfVjoSCH4+N8e6ESFX1SKC0MfUDiwI9dMjfoO7n3n57zqBf/WqZQQue2+QWa/GulN+8uZ5B5T8P27bFM6hrXO3Y4TBo5s9oBjU42mmkz4NAm3LokL9B3c+9/facQb/61WKDFtLkJpXx1mravLmeQeUHFNu2RTSoY1zt2FFq0IR3vzumQe2N9qHJ92AKAtVgb+cdOuRvUPdzb789Z9CvfrWGQZvc5jfeaqGbN9czqJwi27YtpkHLx9WOHS6DvvvdUQ1qbrSn2HsPZiBQDfZ2HgLVg0DrlhVlqw2x9x7MQKAa7O08BKoHgdYtK8pWG2LvPZiBQDXY23kIVA8CrVtWlK02xN57MAOBajC485hE0sMkUs2y4mw2xT9Kg+/BFASqweLO67iNqQTamOrg1caU0dM2pgZhWnwPDhGoDpM7r9NG+lJopK+BTyP9mF420jc5nDf5HkSgOth5eshKz4pl1egD5RXLqgIEGoL2qpo7YnXdOW7ls6rBimWFQIOBQEPQWlVzn5k671286lnVYcWyQqDBQKAhaKuquVn7/ftdBl3xrGqxYlkh0GAg0BC0VNVc3+j+/U6DrnZW9Vi1rJhECgUCDQEC1eNflbuv4NoE7033MKtLE/y3rPXnesJ8Uf3LKiIINAQIVI93Ve7O1muvbWLQ/mV16aXNDVr9W+vriwbtX1YxQaAhQKB6fKtyX1t17bWNDNq7rC69tKlBNayvFxi0d1lFBYGGgEkkPZ5Vua/uv/baZgbtW1aXXtqGQdfXiwzat6ziYk2g/5LgeLiHO69kxXg/cv789Ke7aWPal+D/7N4L9KoEv1epDQLVg0BT/uVf3Abt384rvWeRHzl/jgxaWlSkrPbta2TQvgv0qqvaMygC1YNAhxN/Ogzau53nuGtmQz49pryoOFnt29fMoD0X6FVXtWhQBKoHgc78WW7Qvu08133bm/HpT1cZNE5W+/Y1NGi/J5GuuqpNgzKJpAeBItA6rJxAbbQxWRFo4zYmHbQxVYFAQ4BA9fS7kd6MQBs20muhkb4CBBoCBKrH5B7soUA7o2/vwbi4BPpPE37XVjVMIulZsUmkuPRtEqlLevcejEqZQF+6eTDjjO+3VQ5tTHoq/LlkbUxxqdnGtCchYjVT+p5Vm9gS6GtXDDoRKI30NXD7c8ka6eNSr5F+z56WDNr7rFrElkCPDwZnffD/mvDvH2+3qHLYeXrISk+trPbsacug/c+qPUwJdOOmwTktF6KDnadgfGSaZTW9VGnu/nTd4crqmoTWCpHUGVd79rRmUP9xFfFjWt6DkmKBvnbFps+3XIgOdl41k89G06ymF8vP3SG5QxxZXXNNVwZdNoHGnOjiPSgpE2iLH3vWgZ1XyXR2PslqulzT7bebMWh5Vtdc05lBl0ygUVsFeA9Kyk7hOQKtg6GqZv2hJ07MFgy93Y5BS7O65pruDLpcAo3brMp7UFI6iXRRu3UoYedVsTQCdV93FLqopZpEQqDtUSLQ5BD0w+0WooOdV8WyCNR95XvwomrtQettTAi0PUpO4T/3/sFg0wUfGPOvaWNyY6iqJRGoe+2l8EXV24PGG+kRaHuUTSINOmqkr4CdV8lSTCK5V/+MUJSlPTiDSSQ9CFRDD3eeWEO+HQK0Me1NiFWeqo2pUKCu5febFtX2uNqRUPU579UJnpunjaktTK3GVE3/dl7uLkbt0LiRfu/eiAZ1ZHV16s/MGUUCdd4AqmlRLY+rHRnuY+yrr25oUM+nVtG/92BMEGgIyquau49mm3hntXdvTIOWV3X11VNnFAjUfQvSpkW1O66kP8sMKtKwRe/eg1FBoCEorWruTu6t4pvV3r1RDVpa1dVXFxh0+uhsQixKUa2Oq7w/iw2aS8MUfXsPxqVcoC/fe95gsOm8D7W2GKiGvu08BLqATqALbUwI1Ap9ew8Wsj0hyMuWCvT4dArJUkt933YeAl1AKdD5CRYEaoW+vQeL2L49lEHLBJr688wLPvD+N9syaN92HgJdQCvQORCoFfr2Hixg+/ZgBi0R6ItbBmffl3310k0DQ9fF927nMYk0j2oSqQAmkYzQu/fgAtu3hzNoiUAPD86eXH1kam3Q/u28ev4M2ezun1VnbUxOY1hvYxq1dup/N2obU0T69x6cJ75Ac6sxvbjlbC7ldBOqkT7o5UINsuqokb6iddx2I/3IiXV+O2IjfUx6+B6cI75Ac+uBWloctP87z0XYCy6XO6uwNM9qx456BlWxpFlFAYFq6P/Oc3B72CU/ljqrwDTOaseOGAZdzqziYGoSaeOmwZXTb04OOIWvoBuBHkzwfbQ7XFldm9BaIRIEqmcZ3oPR25iYRKpFJwI9eNDlSPejHeLI6tpruzIoAtWzFO/B2I30L24ZnPW97Kvfvpc2pkq6EOjBgy5Huh/tkvKsrr22M4MiUD1L/R6sjauRfnDeeecZuxRpuXeejz+LHel+tC7K6e/RKlCfSHD9VmlW117bnUGd40q1shGTSB1jTKDDR7eMr+Q0dW+PJd95tU/gWxGosgFztA7pJz5RYdDeCVS5tmYEfyLQGlgT6HDjsfcnR6AX3GJmAill2XdevRmkdgSqvARoshJ+lUH7JlD16u7h/YlAa2BOoCZh501oTaDKi9Bn92KqMGjPBBr3/kIVmBztvAclCDQEXVTV1iRSWIG6DrFNTiJJgXrcs/5tCQ3K8n9qPHgPSuYFuvG59B6cyX8l3JWzgk6qaqmNKahA3R/yWmxjEgIVN63X8ra3NTKoydHOe1AyL9DXrkhvIXLZP3QAACAASURBVMdN5erRTVXtNNKHFGhVm4HBRvqZQOVd65W87W3NDGpytPMelCDQEJisKlRW4SaRAl+rGhDFJFLutvU63va2hgZd6nEVGCMCNQ47T0+wrOb9eX9Cwa9pT+B7JtBh7gQegfIezBFPoCdgWUj9Ofvu/oyCX0v9eeJE6s+S7cwEGqPKaKT+PHFiJlD1E2cCjVgdtItKoBufE/NGL77/v2ASyY3JqiJldf8Yj6f28wh0DEegY3gPSljOLgQmq4qT1f33BzBo8Kqaosmq/iQSAm0RuwJ9cQsCrcBkVSGyWlwyvZFAmy253/WK9N6T8FEEup5Qc3OXJXhWIijPanNC8+17YkWgcxPwGawHWoHJqgJkVXDTnmYCbXLTp+7viVS3DTSmQNfXaxv0ssuCGLQ0q82buzSoFYEOTy4K9MqCJ3YDAtXTPKui20Y2FKh/Vj28K2dEga6v1zboZZeFMWhZVps3d2pQMwLd+D8+8IH3b9l0wfQ6pA9+r4O6SkCgehpnVXzj8ob+9M2ql/eFj9ZIv75e26CXXRbIoCVZbd7crUHNCDTF0rxRDgRaQoFZ8ll5XJhULNBhM3+ulECjXcqJQBcwJdBcG5MlEGgxRWrJZeVzaXyJQMsa6ZWslEBjLSaCQBcwJVCzINBCCt0is/JanKlMoM1YLYE2A4HqsSfQjX8a89h/ZeZ8vm8DvR2K5SKy8lweNIY/V2kSqTFMIukxJtCXbmYxET12BTryn+/6yhH86Z9V921MrUMbkx5bAs13g56NQN2YFejYgN4L1If3Z4Osum6kbx8a6fXYEujxwWDTBWkz0/u3mLqrXA8HeguUCnRyDh72Jp3NMLkHGVd6yEpSMgt/U3r1UfLfK1OX2rkQyebOa2dh40VmxiyZRJrNAi34s8nBgvuw9EBC+aMed8VQcluC95Pz4+ryBPVT5ZHg7gTvGgqINdpHN6D2xOR70JhAX7ti0+eHqTvTW8If5kokJy3dWmMB6cziNiYxjV7gT1+Duj8YPXDAZVCPu2Ioue22JgbNjavLL69hUPlZ5O7dgQ0aabSPVm71fbbF9+DQnECzeaOTg3Om/7WBwZ3X1s3d5skfdRY20ss+pAJ/+hnUPTV/4IDLoB53xVBy222NDCrH1eWX1zConA3fvTu0QeOM9sm9AzyfbvA9mGJToOnZ+2tX2DmHt7fzWru98BzVfZF5gUqatOy5m0MPHHAZ1GNJTSW33dbMoGJcXX55DYPKfszdu4MbNMpon929yu/59t6DGaYEunFTdgo/WsjO0nWd9naeZYHKo8U7EyaPdCjQdL16BCqf7ixLvaUaaAR6aULZY/begxmmBDo8nH36OfoolPVAXZgW6DDnz6lBuxPo6I5JCFQ+21WWdkt1UAj00ksdBrX3HsywJdAXtwwuvC+dhr8olSmn8OXYFugw58+JQTsT6CfGIFD5ZEdZyi3Volqgl17qMqi992CGLYEm1kyvPzo5GGzaMsiORm1gcOfZmEQqQGR1553FBvV53QaTSJ+Y4vPCTno4iaS4nr2bSaRLL3Ua1OB7MMWYQIf/mJ64bxy2tSC9yZ1noY2pCIdAO2pjiihQG21M6fyY059Sl50JtKqNCYHWwLGYyP+TeHPj0fPO+5Adf9rced030hfiEmg3jfQxBWqhkb6ywyDny+4EWtFIj0BrwHJ2ITBZlVOgnRBVoI0IMq4qe7TywuxQoG4QaA3KZuEvvK/dOpSw8/TIrEz4c2bQjstYJMS4quxynTdmR5NI1TCJpKeskd7Q5ZuS/u+8IwnxCpHkspr5s9F10HNbrP0ko/7sRqAdtTEpoI1JDfdECoG+qiNHWjNoPivpzxAG9TyitenPjgTaTSO9BhrptTivRLJH33fekSPtGbQwq4bXQU/x/0zA5B7sSKCVZTWvKjx9fw+GpXQ90LNNfgja85135EiLBi3Kqul10BMazEqZ3INdTCJpygpQVXB6/h4MTIlAX/67weDM6a3h7dyis+c7TyPQUJ9RLmZ1KAGBZlyVIL8PM67qtTEpMJHVPD1/DwamdBJpwD2R9AQUaKjPKBezOnRIGrTZtnsu0KuumjNooHFVudBUPX+ayGqBnr8HA4NAQxBOoKE+oxwuZHXoUM6gzbbdb4FeddW8QXs+rlqFrCQ00ocg2CTS3GeUTVo3b08Q3x46lDPojQnlz/1ygnvrvv7clVD+6HUJ5Y+6r4ByX5f1qYTJ11ddNW/Q+TP6PFsTyh+NicnR3vf3YFgQaAiCtTHlBdqk+f322/MGzQv0xhtdBv3yl7UGrVvVrl0ug153ncug7mvw3SsDfOpTwqALAl04o8+xdWtnBjU52nv/HgyKU6Abv2urDC3933nVM0hTgTa5fOj22+cMmhPojTe6DPrlL2sNWreqXbtcBr3uOpdB3atAudem+tSnpEHnBbp4Ri/ZurU7g5oc7f1/D4akXKCPvS/98PO1/9LSWiJLv/OkQJtcwH777fMGnQl0OLzxRpdBv/xlnUHrs2uXy6DXXecyqHsdUvfqqJ/6VM6gcwJdPKOXbN3aoUFNjvZlfw/Wo0ygG/eMZo9eu2JwlpkppOXfeYcKDkDDCHQ482dcgTpWRUrMmVZQR6DXJ2RfBBTosPgAtH8C3Zbg/IXtCfVf9T0JrqKW/D1YD8eCymf911vO+P7G/8h6oNWEqmo6SZ5+E1igw6k/owrUtS7nyJ+pQYseLRLo9ddPDBpSoPkPPXsr0G3bKgy6fbuPQd/zHrdBl/w9WJMSgZ4cDD48viL+0S2GFhZZ7p03nePJvgst0OHEnzEF6lwZftfkKFgr0Ouvnxo0qEBz0+59Fei2bRUG3b7dx6DveU+FQZf7PVgX103lxkuKHOe+8FWEqUp+TJkSdBIpR4hJpELc9yaa/wPnKPVnzqCFT71m4s/iPvZ5f+bYMfHnjsKHrU4ibdtWYdDt230M+p73VBl0qd+DtXEtJjIWKHflrCSOQIO2MeVp3sZUTCOBLrQx5QTqbGO6ZmzQsguBHP4c7hgbdEexQK22MSHQPKYEOlLnWKCW1rZb6p236JeAjfRzNG2kL6GZQOcb6fMCdTXSXzMyaPmVlOX+TAS6Y+TPEoEabaRHoHkQqIal3nmVfqlHF1k1FOgccwJ1ULmUnIMdU+o/NzIIVI8pgW7clE4cjc150tA0/HLvvKD+7CYr9+2F6/6BWn8qlpJzYNafTCLVwJRARxNHI4EmMmUSqYKAbUwuvdSTazdZuW8vXPcfCK0/FUvJOajwZ7AFBp0UqS5WG5Pzz6WNqQ4lAn1xy+Atj2cCfem9A0Or0y/7zqv0Zw37dJSV+/bCdQ+wtf5ULCXnoNKf8Q1aKLtIjfQV/2DQSF+Dskb644PB4Lwtmy54c/L/i1qtyMkq77y657+rnFVdHFkFXGDQQfHpdpysGn5kwbiSlF4L/49bJquBGvLnKu+82lNMK5xVbcqzCnUTFDclEz5Rsmo6aca4kpQvJvLyvecl9jzT1g3iV3jnIdCIWBVo5Um6Bwg0JKwHGgIEqsdkVUYFWjlN5AMCDQkCDQEC1WOyKpsCrWxU8gKBhmReoBuf+8Ai3JWzAiaR9JisyuQkUmWrvCdMIgVkXqBzt5NbmZvKPZTg+2i8nZe/lHPen+6LNQ8mlD/qVoL7Qk/3686xcP1lGwN9cVmminYo17iK68/JKlClJ/DRTuJ9n41AJQg046GHXI50PzqMtvPmFxNZ9Ge5yQ4edBnULQX3UiPu151jcQWQFgb64sJ2VQ35rnG1I40q1mVKs3X0FpuYognU3fdaBQKV8BloykMPuRzpfjQrK0pV7uXs3AvWHTzoMqj7tNS92J37decoWIMu/kBfXBq08pJQx7iKeqGn83ZM8QTaCAQqQaDDmSGLHel+dFRWjKrcCyoXLpk85eDBmUG/lpB/1D0x4l5u2f26cxStghx9oC8urly9KEn5uAq71MjcolDutZwjTSI1BYFKuCvncMkF+rWvLRgUgc7TkkDnlyWtEGicNqamIFAJd+UcLrdAv/a1RYMi0HnaEejCwvhVAo3SSN8UBCrhrpzDpRbo175WYFAEOk8rAi2+NZNToI1fMwIIVMJdOVPiTyL9KKFuVSEmkaRAZ9uqM4k033oadBLpCwmqDdXB6iTSokCnBt2XMBxuTsiX1fxFw4NAJdyVMyN2G9OPfuRv0LJHNW1MnxYClVvTtzEtNu8HbGP6whciGlT+pFEbU9hPQIs+Bd2XsXnzvEFNqgqBSrgr54i4jfQ/+pG/QcsfrW6k/7QQaP54VttIX3T5U7BG+i98IaJB8z9p0EjfrGtSUCTQ4bw/cwY1qSoEKuGunCGoqOpHP/I1aBNOnEgtOe/PenepC3ybpqys6Vdf+EI0g9alnXFVcnflvD+lQU2O9n6+B2PBTeVCYFGgd9xxx6dnBq2Ykkq4O2HhhwYFql+jvk5R/uOqzvFp8d2VEWgIEKiGfu68LgR6x0Sgn57NILkEevfdRQa1J1D9XZJqFeU9rup9Qlp4d2UEGgJTAuWunPWwJ9A7ZgIdfdxZIdC77y40qDmB6u/TWa8o33EVYo4egYbAlEC5K2c9Yk0ieXPHHTmDpj9S+bPUoOFKazSJpL9TfM2iPMdVmC5RJpECYEug3JWzFpHamPy5I2fQ0c+qT+DLT+IDlubfxpT2BiylQIe0MTXHlkC5K2ct4jTSN+AOadDJDytmkIoFWvtGxFV4N9KPulOXUqBDGukbY0yg3JWzDuaqmgr0Dt3vOwQaGt+sJtdHLaVASzA3rlJ4D0q4K2cI7FVVz5+lk0gR8MxqdoX+0k0ilWNvXA15D+ZhPVANxxJcj7uqcveuu2+84X70mwklD6Xn3XX8OdfGVOtaozmuSXA9nsvqKwni2y8llDwtL9CSX6hZ6nB6zVLTNqb1dd/nOzGpKgQqQaAKjh2rMKijKvfVP+4bb7gf/eY3Sw06mvmp489cI32tq93nuOaaCoPKrL7ylZxBv/SlcoPmBFr6eN1qJ1fNN2ykX1+PY1CTqkKgkiqB/lMrVajpZOcdO1Zl0PKq3N3r7htvuB/95jdLDdqw96jWektzXHNNlUFFVl/5Ss6gX/qSw6DuRfYqbkNSxnTdpibjan2M/xZKMakqBCopFejGvednFyMNTH0I2sXOO3as0qClVbnb1+WNN+o++s1vlhq0Yfd7rRU/57jmmkqDzrL6yldyBv3Sl1QGdT5Yz6CzlUMbjKv19XgGNakqBCopE+jJLYPR1ZyDwSY7q9ktn0AfSDAgUDl/lJgzfdFoAp2uz1RPoM6TdATaHghUUt5IP7qA8/++ecuqN9LHFOgDD4wMWvxoawKdm0EavWokgc5WCK0pUNc0EQJtDwQqKV0P9KzJmfvKX8oZUaAPjOlYoPkeptsnLxtFoGKN+roCdYBA2wOBSspWYxJHnSu/Hmi0SaQHphQ+3NYk0lwXvVvcFWj9mTPo+LEqfxYuZTTGdxLpsoR+TiLtSYjwktUgUIlrObuibzpmudqYKgTatI1Jm1VIgVa1MeVvM1ejjalsMc0Jfm1Ml2U0HFfR/OkaV3v2dGVQBCrhCFRDpEb6KoE2a6RXZxVUoBWN9HP36dQ30pct5z7F35+JQZuNq1j+dIyrPXs6MygClZR+BnpO4ddds1w7r1KgjehIoG6KbnSsovCGQg25bErfxtWePd0ZtG9ZxaX8rpwX/i776uV7BitwV86G+Fal8+c/JHhsXJ/V3IXwEf1ZeKNjFcYFWnUBaynbE0ofRKB6bAk0vS/8YNN5552Xrslk5wB06Xae1p8+Bq2R1dxCIhH9WXSjYxW2BVp5AWsZ27e7DIpA9RgT6MbfTVaz2/RXrRbkZul2ntafHgatk9XcQkwR/Ska6WthWqDVF7CWsH2706AIVI8xgSYKfez9yRHoBf+LmfshpazezvuHf/A16JJlFd6fwSaRFJcPFLN9u9ugTCLpMSdQk6zezkOgE8L7M1AbUyyBOg/VaWOaA4FqWLmddwSBTgnvz5FBhzYFWvFhMY30eYwKtGw5u9dveNfki7WMd/wsZFllrNrOO4JAW8GgQH3bFaLDuJL4Lmd3dG0s0Fd2ItBoO+/IkZlBaz95xbJqhL1JJO+G2egwriR+y9mdPro2EeipyRdt8FxCnC0362aPKdAjpf4czZXfn1BclKuqJvfadC8VeiDB9ewwWV2XUPWTGthrY2oo0NsSyh9tdBcnBCrxWs7u959Zmwr06NrHYtaX47nnYhm04fVAkXbewSNTgxY9mnH//WUGdQ30JivWuxdbPnCgwqBBsrruunlfLv6kDvYa6ZsJ9LbbXAZtdh88BCrxWc7u6bW1j/7zWKCn77r4W/Gqy/Pcc7EM2vSKyjg77+BYoClFj878WWhQx0BvsmK9e7n6AweqDBoiq+uum/fl4k9qYU8KjQR6220ugza8k6i9rDJMCdS9mMjT7/zb6Zn76zdc8h+T49F/+9N4JU547rlYBm18TXqUnZf6UevPIoOWD/Qm9/xw3/DjwIFKgwbI6rrr5n25+JN6GJRCAH8WG7TpvewNZpViTKBVy9lNBDqZQ1r77PxvnAjNTKChtzwTqPfTvZ74cEL5owdnBi17VAi0zuvOBFqz4ISZQIsenQm05Onpu7r+i84x02X5T+KxKyHOltNVnU6cuDwh/W7kT5/tzARa9OhMoE1qXVmUAq1azm4i0FPJ6fwfhv/pG2sLZ/LBK7cqUO9nPvyw06AHpwYtf9SYQA9UCbT8bV2HTgW6a1csg47WFb38cmlQrw0h0IioBFq9nN1EoE+P/9/CXJLRU3jvpz48puxx97JyFk/hhT+LT+Hdn82p6fIUftcYv9dxIf15+eWjsvy2xCl8e/guZzffvXRq7ZI/hK5tHpOTSN7yffhhrUFdj1qaRFL7M5hBXT+phVoKu3bFMmjenyOD+kqBSaTW8F3Obl6gr+xsoZPeYhtTRIFWLCvXtI3J787vjjamKn+GE2joNib9U2sJtNaiViEFShtTa/guZ7co0PhHoCYb6WMKtOId2KyR3t3O6cJ7Cj6cQMM20teQbx2B1ltWNahAaaRvC9/l7MYCPX3XePq9pQuS7O28qAJthDsrdzunF20KNCR1Tv9rCLTmwv5hBRoRe+/BDHMCdXNqOnmUF2lkDO68aJNITXFm5W7n/HaCxytW9oCG8GfVpaK1qTcBVdufngbNfhRgtF+dsPDD6Qv4UOc9uDfB+4XqYVegG/f+584+0I/+YfjqZ1qYQ0oxKFD/z0/j+rOBQL/97UYGdfxCGH+GNWjNGfx6J/C+J/GjnzQf7VdfXWBQ+RL1qfEe3Lu3PYNaFehv3zcYOPpA0+s6s8WYWrgUaWhToP6fn0b1p79Av/3tRgZ1/kIYfwY1aN0WqBozSDVvLjW6PbKQW+PRfvXVBQbNHeTWR/8e3Lu3RYOaFOjGveksvFOgw1f/em3t4o+2cvxpVKB9/KzKIdBvf7uBQRVlNXmy4lLR2jTtIS0hxN2hm46rq68uMGj+Y1aPorRV7d3bpkENCjQ9+EwpXhG0ExCoHt9JpFUTaNMe0jIC3B0ageqxJtDxwefg/FvaLKcKBKqnIquKT0BXSKANl8IrpfndoRGoHlsCfWx88Flw8t4pCFRPVVauKfjVEmizxZjLaXx3aASqx5BAX74nO/jcdMEWBKrDZFXeWUX1Z8OsovhzeccVk0ixWRToY+8dffD5vfR+Hisj0GMJvo+6d96vEjyLatbz6J9VhT/dVe1PcJbleMw9R5+tjlnqT/ea8PsSyh91vMu9l5oPgSsrXWG0MUVmXqDpTZAGg7NueXz09aoI9NgxlyPdjw6dO+9Xv/I3aLODLf+sDqT+LH1dd1X791cY1FGVu0t0vL6ww5/lRtm3z2VQx/vc+2ZHQXBkpS2MRvq4FAj0rMnVm6sj0GPHXI50P5qVVfrIr37lb9CGp6veWblf1/3o/v1VBi2vyn2dknuFdvd9MfftcxnUcabpfbvNMJRn1WFhy/pxhx9FR6Dnjw26MgI9dszlSPejo7LKHvjVr/wN2nTCxDcr9+u6H92/v9KgpVW5r5R33yPIfWf2fftcBnXMdXjf8D0QpVl1WRgClcwLdOOe7BPQMz/8OAJVPToqq+wBBLpYVuFPb5MU/YJboHcm9Eeg6g0WZDVqGECgCxgR6HA6i3T+9xCo4tFRWWUPINDFsop+eFszgd5559SgRc81JlD9FhezGreszgr7NyErU4FAJYV9oJMm+lXpA0Wg+teNItDbmgn0zjtnBi16ri2B1tjkQlaTi6aEQFs3KAKVlF2J9NLNI4O+5XetllMFk0h6+jOJpPCnaxLpzjtnBi1+rqVJpDpSns9qdtn+zJ+tGxSBShzXwo9P5Td9qHhJ5U7oQxvTzxNm3/Wyjcn5ugWPbk4Yf+nTxqTx57SNaREh0LLnGmpjCiPQ4cyfCDTDnkBnp/JnmzmR70Ej/c9/vmhQ36qa+LNJVu7XLfRnzqDOshZ/pPLnuJG+gJlAy59rp5E+kECHU38i0AyLAh2OT+XtfBJqf+f9/OfzBu2K1rLavDln0AqcAvV6fY1Aq4pqb1yFEui/mRKlTEdR5t+DbaJYkf6x9yLQCmZV/fznZgzaVlabN9cyqGsSybOCxv5sdVyFmERKv+7In/bfg63ie0+kjjC/8xBoFY42pnqvK1aTqvbnaLH38qJiZbUnYf5nAdqYMrrxp/33YKsg0BAg0IYC9bjVR249U40/XQaNldWePWUGVT29tJF+RCf+tP8ebBUEGgIE2lSgtal1W+b19QqDRspqz55ig2oxOdrNvwdbBYGGgEmkRpNIHrhvyzzH+nqVQfNZuafs9ezZ09CgJke7/fdgmyDQELjamDqjvazq+LMHAnU3jdYAgbYIAtXQh51nxJ9tZlXDn/YF6r5sqQ4ItEUQqAZ2np6lziqeQN0XztcCgbYIAlXwfEL5o1XXC7lociXSLxLKH30owbeqJnwxofzRryf4bvnGhPJHDyWUP+pWXo3Lfhb86boCqs4kUi2B7kpwPMwkUnsg0Gqef95l0Mor1h00uRb+F79wGfShh7ox6Be/6DLo17/ub9Abb3QZ9NAhl0HdB421Ljwv8GeVQcs35inQXbtUBq3eUFlZ3s+MCAKV9Emgzz/vMmj1mknlNFmN6Re/cBn0oYe6MegXv+gy6Ne/7m/QG290GfTQIZdB3afdNZc+KvBnmUEjHYHu2qUyaOV2ysvyf2o8EKikRwJ9/nmXQRWrdpbSZD3QX/zCZdCHHurGoF/8osugX/+6v0FvvNFl0EOHXAZ1f3DZZPFN9zqkkSaRdu1SGLQRJlWFQCUItPK5dQV6JGHyNQKV9EOg6jamkTy/klC7XiUmVYVAJQi08rk1BXrkiDAoApX0RKDaRvqpP6MZ1KSqEKgEgVY+t55AjxyRBkWgkr4IVMnMn7EMalJVCFTSI4H2YhLpyJFig/pU1YQVmETKEW4SqQYzf0YyqElVIVBJnwTahzameYGuahuT/CBYELCNaY5gbUx1QKBdsiNh9h0CVWC/kX5BoKvZSJ+PQBCskX4B961EIq0HikC7Y8eOnEERqAYrO2+OWVWLAu2MDrNyZWByDyJQPUbegzt25A2KQDUY2XnziKrM+LPDrJz/ipjcg95ZMYnUETt2zBkUgWqwsfMWkFUdSc/off0Z8nwfgerxz4o2pm5AoF7Y2HkLyKrcl8a7CTrjhED1NMiKRvpOQKBe2Nh5C4iq3JfGuwnb84RA9dgfV3awkRUC9cLGzltgVpX70vhF7k+YfB24677/k0i7E0KV5Mb8uDKEkayYRPLByM6bx1ug998vDLo8Ai1vY6oz0Hfvbs2g5seVIaxkRRuTB1Z23hy+Ar3/fmnQJRJoWSP9sMZA3727PYOaH1eGMJMVjfT1MbPz8ngK9P77cwZdJoGWo61q9+4WDdrzrFqFrCTLJNA/JZQ/+khC+aMPJ5Q/+suE8kdz1yn5HIDOH4JOf8F9dc2BhPJH3bfWaPLLbtyz0ncn6LaDQBFoHRCoBtfO+9OfXAZ95BGXQR9+2GXQX/7SZdC5K+VrfwK68Cno9HH39d0HDrgM6r61RpNfduPui7z7brVBESgCrQMC1eDYeX/6k8ugjzziMujDD7sM+stfugy6sFZTvSn4nECHBf4sM+iBAy6DuldFavLLbtxX5tx9t96gCBSB1gGBaijfeX/6k8ugjzziMujDD7sM+stfugzaZB3S4bw/c7jXuDxwwGVQ97qcTX7Zjfva8Lvv9jFo46IUIAU9ZCVBoMMOBTos8OcPEp544gkEShsTAq0BAtWwbAIdFvpzZNCVFyiN9CarIisJAh12KtB5fvCDqUERaHsgBT1kJVkagdqZRGrCD35QYNDiX132SaRWQQp6yEqyPAK10sbUiJxAV7uNqVWQgh6ykiyRQG000jcjL9CVbqRvFaSgh6wkyyTQ7ghW1ZxAG7HsWYWErPSQlQSBhiBcVeH8ufxZBYSs9JCVBIGOaHYaXqOqnyS4Hq/tz9GFTwVLkDDQ9bSVVeFnMuV3DF3prGqCQDXE2nkNJ4L0Vf3kJxqD1vTnL35RtIgTA11PS1kVzgo67lm/ylnVBYFqiLTzmrYiqav6yU+qDVqLyeJPBQZloOtpJ6vCvrT19XKDrnBWtUGgGuLsvMbN8NqqfvKTwAadLT+6aFAGup5Wsiq8MmJ93WHQ1c2qPghUAwLNg0DDgED1MK4kCHSIQFvFZFUIVA/jSoJAhwi0VUxWhUD1MK4kCDSlyp+/SSh/tnsF5dx2q/zpviHSXIkHE5hECkIPJ5GuTwhZnBrGlQSBZlT7s9yg7nt4zG252p/lBp3b1MGDM4PSxtSM/rUxXX99VwZlXEkQaMqTT6ZqevLJ4kd/8xuXQd13kVs4tq32Z5lB5zZ18ODMoDTSN6R3jfTXX9+ZQRlXEgQ6TP05oejR3/zGZVD3fYxriQD/TQAAHjFJREFUfbrqvq3x3KYOTinbHANdT9+yuv767gzat6zigkCHCLRVfKqKvYZTZ58nVoBA9SBQDQh0FQUaexXR7j5PrACB6kGgGhDoCgo09jr2HX6eWAEC1YNANUSbRCr3Z+BJJBdek0ilW1uWgR77TkpdyqgCJpH0IFANsXaey5+LbUy/Tph9V6uNyY1HG1P5xrKsHkxQvHDAFemrQKB6aGPSg0A1RNt5Ln/ON9L/+teLBi1/bq0LnGo30ju2lWb14IMqgwa8J1IlCFQPjfR6EKgGCzvv17+eN6jZ1pwHH1QZNOBdORVl1X0CArWFhfdgAQhUg4Gd9+tfLxq0+6oKOHHiwQdVBg14X3hNWbWfwSSSKQy8B4tAoBoM7DwE2rCs+k+hjckSBt6DRSBQDQZ2HgJtWJbHc2ikN4SB92ARCFSDgZ2HQBuW1caL1MXAuCrCZFVkJUGgtWESqVlZrbxKTSyMqwJMVkVWEgRanwV/2h3obbQx1XzqLKvvJni+ZmhMjKtFTFZFVhIE6sG8Pw0P9PiN9HXlO83qu9+1Y1Ab42oBk1WRlQSBhsBkVe1kVfv0f1LVd79ryKCMKz1kJUGgITBZVStZ1Z+AGlf13e9aMijjSg9ZSVZHoM8klD/6bILvlhvcjW4e91Wh9WhZoO7rSme4BPqdhPA1aopCCmrISrIyAn3mGZdBn33W36C1lgtx416XpCbtC1RlUIdAv/OdrgyKFPSQlWRVBPrMMy6DPvusv0FrLVjnxr0yXl06EKjGoOUC/c53OjMoUtBDVpIVEegzz7gM+uyz/gattWSyG/fazLVpdxKpanXSKaWTSN/5TncGRQp6yEqCQIcItBE5f9YQ6EIbEwJdwGRVZCWJJ9ATlpgJtOjRmUDrb3km0KY1npgJtPGm2kT682CdJ6b+FN/OBBq4QIBwtCbQKHAEqqfFI4XqGzTNKK2KI9AFTFZFVpIVESiTSHHR+9Mx0JlEmsdkVWQlWRWB0sYUF7U/XQOdNqY5TFZFVpKVESiN9HHR+tM50Gmkz2OyKrKSrI5AY2KyKrLSQ1Z6yEqCQEOQq6rJwWxI+pBVV+xKkN+TlR6ykiDQEMiqmnycGpQeZNUVu3bNGZSs9JCVBIGGQFTVZEI/LPaz6opdu+YNSlZ6yEqCQEMwq6pJS2lgzGfVFbt2LRiUrPSQlQSBhqCGQN3NAEGLsp5VVyDQRpCVBIGGQC9Qdztq2KKsZ9UVCLQRZCVBoCFQC9R9QVTgoqxn1RUItBFkJUGgIdBOIrkvyQ9dlPmsuoJJpCaQlQSBjnBfAvRUguvZrjYmeZ1SXYE+kKD7zaKiGOhl0MbUALKSINAM90XoTz1VYVBHI33uSvmaAn3ggSYGZaCXQyO9P2QlQaAp7mWQnnqqyqDlVeXXaqon0AceaGRQBroestJDVhIEOqxaiPOppyoNWlrV/GqhPv70NSgDXQ9Z6SErCQIdtinQOm1MCLQ9yEoPWUkQ6LBVgdZopEeg7UFWeshKgkCH7QpUDwJtD7LSQ1YSBJrS1iRSPZhEag2y0kNWEgSaEbKNKU+TG37QxtQWZKWHrCQIdES4Rvp5mtzwg0b6liArPWQlQaAhMFkVWekhKz1kJUGgITBZFVnpISs9ZCVBoCEwWRVZ6SErPWQlQaAhMFkVWekhKz1kJUGgITBZFVnpISs9ZCVBoCEwWRVZ6WmQ1fUJASvJsWxZxQSBamDn6SErPf5ZXX99RIMuWVZRQaAa2Hl6yEqPd1bXXx/ToMuVVVwQqAZ2nh6y0uOb1fXXRzXoUmUVGQSqocHO+2OC73PdVxM9kVD+6JMJvltuBANdDwLVw7iSrIxA//hHf4O6r2d/4gmXQZ980mXQJlfKV8FA14NA9TCuJKsi0D/+0d+g7hWVnnjCZdAnn3QZtMlaTZUw0PUgUD2MK8mKCPSPf/Q3qHtNzyeecBn0ySddBm2yWmg1DHQ9TCLpYVxJEGgldQUqdYlAFzBZVeg2ph8mNKsoY8myigoC1dADgeZ8iUAXMFlV4Eb6H/4wjEGXLauYIFAN9gWaFyYCXcBkVWGz+uEPAxl0BbIKBgLVYH4Sad6YTCLN03ZVdydU/lLQrH74w1AGNbkHGVeSVRFoW21MC4ectDHN0XJVd9+tMSgC1cO4kqyMQFtqpF88Z6eRPk+7Vd19t8qgCFQP40qyOgKNyawq94eerWI+qxa4+26dQRGoHsaVBIGGQFQV2p8PJvg9035W8elEoEwidQEC1dCDnRfen54G7UFW0elGoLQxdQAC1dCHnRfen34G7UNWselIoDTStw8C1bBiO+/BBxsYdMWyKqaLSaRwmKyKrCQINASuqp5J8N0uAm1MB21M4TBZFVlJEGgIHFU980wDgyLQ5rTfSB8Ok1WRlQSBhqC8qmeeaWJQBNoSZKWHrCQINASlVT3zTBiDehXVs6y6hKz0kJVkmQTq9tQLCeWPPpXgW5TjaqKGAj12jDamViArPWQlWSKBukX1wgsugz71lL9BXdezNxNoul0a6duArPSQlWR5BOo21QsvuAz61FP+BnWuqNRIoA3XamKg6yErPWQlWRqBulX1wgsugz71lL9BK9b0DOBPX4My0PWQlR6ykiDQYVSBNmhjQqDtQVZ6yEqCQIdxBerfSI9A24Os9JCVBIEOIwvUGwTaHmSlh6wkSyNQm5NIjWASqTXISg9ZSZZHoCbbmJrRbMsMdD1kpYesJEskUIuN9A1ptGUGuh6y0kNWkmUSaHeYrIqs9JCVHrKSINAQmKyKrPSQlR6ykiDQEJisiqz0kJUespIg0BCYrIqs9JCVHrKSINAQmKyKrPSQlR6ykiDQEJisiqz0kJUespIg0BCYrIqs9JCVHrKSINAQmKyKrPSQlR6ykiDQEJisiqz0kJUespIg0BD4V/VQQsBCJEuXVUTISg9ZSRBoCLyreuiheAZdtqxiQlZ6yEqCQEPgW9VDD0U06JJlFRWy0kNWEgQaAs+qHnoopkGXK6u4kJUespIg0BAgUD0mqyIrPWQlQaAhQKB6TFZFVnrISoJAQ4BA9Zisiqz0kJUEgYaASSQ9JqsiKz1kJUGgIaCNSY/JqshKD1lJEGgIaKTXY7IqstJDVhIEGgKTVZGVHrLSQ1YSBBoCk1WRlR6y0kNWEgQaApNVkZUestJDVhIEGgKTVZGVHrLSQ1YSBBoCk1WRlR6y0kNWEgQaApNVkZUestJDVhIEGgKTVZGVHrLSQ1YSX4G+fsO7xl+d/sbOtbWP/DRUQW7YeXrISg9Z6SEria9Aj66NBfr6DWsp7/hZsJJcsPP0kJUestJDVhI/gZ4+ujYR6NG1S346fPWutUv+ELCqUjraeS8klD/6ZEJ7tahhoOshKz1kJfES6O8/szYR6Cs7s2PP12+4+Fshyyqjm533wgsugz75pE2DMtD1kJUespL4CPTptbWP/vNYoE9P//+xgFWV0snOe+EFl0GffNKoQRnoeshKD1lJvAT6zr8dnhqL8+jaZ7P/T76PTBc774UXXAZ98kmrBmWg6yErPWQl8Z1EGgvz9F3jU/dXds5/CHpiWZgJtOjRmUDbrgsAWgeB1gWBAsCYaAJtpZGJU3g9nGrpISs9ZCWJdwQaBSaR9DDQ9ZCVHrKSIFAFtDEFxGRVZKWHrCQNBboKs/BDGulDYrIqstJDVpKmAp30fy5zH2g1JqsiKz1kpYesJE0FuhJXIlVisiqy0kNWeshK0lSgp+9ae+fyXwtfhcmqyEoPWekhK0lTgQ5fZTUmBnodTFZFVnrIStJYoMNXv5H48yOtHH+y8+pAVnrISg9ZSViRPgQmqyIrPWSlh6wkCDQEJqsiKz1kpYesJAg0BCarIis9ZKWHrCQINAQmqyIrPWSlh6wkCLQ5xxLKH/1LQnu1CExmhRTqYLIqspIg0MYcO+Yy6F/+0pVBLWY1RAp1MFkVWUkQaFOOHXMZ9C9/6cygBrNKMVkVWekhKwkCbcixYy6D/uUv3RnUXlYZJqsiKz1kJUGgDUGgNTFZFVnpISsJAm0IAq2JyarISg9ZSRBoQxBoTUxWRVZ6yEqCQJvCJFI9TFZFVnrISoJAG0MbUy1MVkVWeshKgkCbQyN9HUxWRVZ6yEqCQENgsiqy0kNWeshKgkBDYLIqstJDVnrISoJAQ2CyKrLSQ1Z6yEqCQENgsiqy0kNWeshKgkBDYLIqstJDVnrISoJAQ2CyKrLSQ1Z6yEqCQENgsiqy0kNWeshKgkBDYLIqstJDVnrISoJAQ2CyKrLSQ1Z6yEqCQDX8OcH1uMkhxUDXQ1Z6yEqCQBX8+c8VBjU5pBjoeshKD1lJEGg1f/5zlUFNDikGuh6y0kNWEgRayZ//XGlQk0OKga6HrPSQlQSBVoJAg2KyKrLSQ1YSBFoJAg2KyarISg9ZSRBoJQg0KCarIis9ZCVBoNUwiRQSk1WRlR6ykiBQBbQxBcRkVWSlh6wkCFQDjfThMFkVWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAtXwfEL5o88mtFeLGga6HrLSQ1YSBKrg+eddBn32WZsGZaDrISs9ZCVBoNU8/7zLoM8+a9SgDHQ9ZKWHrCQItJLnn3cZ9NlnrRqUga6HrPSQlQSBVoJAg2KyKrLSQ1YSBFoJAg2KyarISg9ZSRBoJQg0KCarIis9ZCVBoNUwiRQSk1WRlR6ykiBQBbQxBcRkVWSlh6wkCFQDjfThMFkVWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkC1fBIgutxk0OKga6HrPSQlQSBKnjkkQqDmhxSDHQ9ZKWHrCQItJpHHqkyqMkhxUDXQ1Z6yEqCQCt55JFKg5ocUgx0PWSlh6wkCLQSBBoUk1WRlR6ykiDQShBoUExWRVZ6yEqCQCtBoEExWRVZ6SErCQKthkmkkJisiqz0kJUEgSqgjSkgJqsiKz1kJUGgGmikD4fJqshKD1lJEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUkQaAhMVkVWeshKD1lJEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUkQaAhMVkVWeshKD1lJEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUkQaAhMVkVWeshKD1lJEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUkQaAhMVkVWeshKD1lJEGgITFZFVnrISg9ZSRBoCExWRVZ6yEoPWUniCfQEAMCS0ZpAo8C/fnrISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npISsJAg2ByarISg9Z6SErCQINgcmqyEoPWekhKwkCDYHJqshKD1npIStJzwQKAGAHBAoA4AkCBQDwBIECAHiCQAEAPEGgAACeIFAAAE8QKACAJwgUAMATBAoA4AkCBQDwBIECAHiCQAEAPEGgAACeIFAAAE96I9DXb3jX+KvT39i5tvaRn3ZajWF+/9draxdP4iErJ7//TJLVf/+H0TdkVckrOy8ZhUVWE3oj0KNrY4G+fsNayjt+1m09Vvlxls7axd9KvyErJ0+PsnpnFg9ZVXL6rrWRQMlqSk8Eevro2kSgR9cu+enw1cmuhDyn1i7+m2EaTza4ycrFKzuzrD4zGllkVUnyD84oHbKa0g+BpqdaY4G+sjNTw+s3jI6xIEdyjPDZ9P/JIcJnyaqCo2sfS/83SomsKnll51igZDWjFwJN/uX76D+PBfr09P8f67Iko7x+w/i0KpMDWWkYZUZWVST/OP93o89AyWpGPwT6zr9Nzk1HO+3o6BBr+j0UkgmUrDSMZkbIqoqja+8aTyKR1YxeCDRlvLNO3zU+bZhOCEIB2dkVWWn4552pDsiqilPJ6fsoHLISINClJDvJIqtqjq6tXfy3Q7KqJPsnGYEu0GOB0kRRyqmsjYmsKjn9v/+3O9cu/h/IqpLsM6EFgZJVjwXKv35lnNp5cfohFVmp+H16Dk9Wbp7O5t85Al0AgS4fT4/b6MlKR/rpHlk5eWVnFg8CXaBvAmUGsJIfr03a88hKReYBsnIxvmZrfPkRWc3onUAnvWf0oBVz+uj40sQhWbmZXHQwEihZucgLlKxm9E6gXAXh5qi4vo6snBydntS8i6xUjM/ZyWpG7wSaHDe8k+twS3la5kJWTl7ZufbRPwxP/3jcskBWlYwFSlYzeifQ4ausBFPOeJmctfHSAWTl5NR45arsTJ6sqpnMGpHVlP4JdPjqN5J99xH+7Svi1FpOoGTl5lW5dipZVTKddierCb0RKACANRAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAoSe8+J+d/6///ezbjcc+cN453VUDkIJAoSe8uGUw2PT56bcnB4MBAoWOQaDQE1KBDi6afnsYgUL3IFDoCYlAzxuc/fj4u9eu2PRmBApdg0ChJyQC/eCW6Tn8ycG/ugmBQtcgUOgJiUA/fNP0HP5w+g0ChY5BoNATEoFeeXxyDv/aFWf8h5FAX7ticNHGvVsGg7NumfzmY+8bDDa95fHjgzO+31WxsCIgUOgJqUBfnJzDnxycszEV6FtvGmSM5Lox/u6MmxEoxAaBQk9IBboxOYc/nBx2TgU6GFz4u+HGPeNZ+cODwVsez75FoBAbBAo9IRXocHwO/9oVmz4vBDr6LPRw1iaa/NrIsccRKEQHgUJPyAQ6Poc/mXh0JtCxJ5Ovzkm9OfsWgUJkECj0hEyg6ZTRMDuDH84EOpmMPzzT6uhbBAqRQaDQEzKBZpJM3Jkch84EOmttOuP74ltm4SE6CBR6wkigJ9MPOl/ckll0ItArx79xHIFCyyBQ6AkjgWaCPJ5KsvQIdHIKj0AhOggUesJIoIklz8nO4AsFymeg0C4IFHrCWKAnB2f8fXoGLwQ6vTopVSmz8NAiCBR6wligiRfPy8wp+kAnzfX0gULLIFDoCWOBZguBpl/IK5He+vjwpZvHIj3OlUjQGggUesJEoJMjy5lAL9gyuvp9dOS5cXj03Vn/MwKF2CBQ6AkTgSb/z6aJxCRSevQ5uPC+yW+yGhO0BQKFfiNm4ec4PFu/HiAOCBT6zbxAp81LGyy4DNFBoNBv5gV6fDC+Mmk6HQ8QDQQK/WZeoIk3N304Of58dAsfgUJ0ECj0m4XPQE+O5+QHZ91X8hSAUCBQ6DeLk0gv3/PmRJ/n38IMEkQHgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAAQA8QaAAAJ4gUAAATxAoAIAnCBQAwBMECgDgCQIFAPAEgQIAeIJAzXJ4cMb3p9+8dsXgnA5rAYAiEKhZECiAdRCoWVZFoMmfljH6azdu3jIYXHhfpFeaZJh7lYgvOX3Fdv7Ix943GGwq/LNixrrSIFCzrIpAX9wi3DIWjfjLA3J4kNfZ6FVivuT0FVv5I+8Zvcamzw/nXyRqrCsNAjVLzwX6pgTVL56Uf9nhwdn3DV+6aXD246rnHkzQFrRxeDB5pdyr1HvJYwker9jkj3wuQfN7JwebPjxMt5uNmwZ/I+hBoGbpt0Df9CatQQ8PLpp+/eKW8SHa6CiqioMH9QZ97L2Dic5yr1LvJY8d0xtUvGKTP/K553QG3bhpcOUw2276/wZ/I9QAgZqlRKAvpZ9mTT7oSt806fv0zM+PHxicf8vkKblfTJ5/0ca9yQ/OKnp8Y3JsMn2Z9Pedr1bBm96kNejGTeJdfXz88seFb8o5eFBv0OODwVsenW5dvEqtlzx2TG9Q+YoN/sjnnlMa9LUrxuPl8MKfVe8VoQYI1CzFAj0+GH/Q9Vfpd4nSPjD+cOvR8QODs76f+8XBW8bPf+tNo+/Hp3G5DR0ff3D24pbxi54c/SC/EfFqFbzpTWqDvnbF2X+fSPn8+0Z/c3YQlT/jLePgwRoGPZ78yzHZau5V6rzksWM1DCpf0f+PfO45tUEnZAL1/huhFgjULIcHebKxnxjtrO8Nh79N3o3peyJRWmq6l25J1Xd28vbc+LvZL6bHjS/fM5JfNotw4e+GG/cUbih59pXjn06+SD07t5HZq1VRQ6CT6ZX0dacHai9uUXxaV0ugKWN/5F6l1kvWEqh4xQZ/ZH2BZifq/n8j1AKBmqVIoIkHR2+BjdFUQaq00cHF8cH0BC79InnHjg82RgeXqUAnh1/j7+WGkv+eM3nNi0Y/vWhxI7NXq6KGQE8mcn58+PLNg/m3feUzeyRQ/z+yvkCz83UE2hII1CxFAp2camdyu2jq0dwj428n59kjNybCHP9g9GHA/IZGv58cvPy7TKyjI9L5jcxerYoaAj0+FftF8m2veKEAAj3j+7Ve0lug/n9kbYGeHP9b5/s3Qi0QqFmKPgOd/Wz0g+nsT3qMs+nC701+fXJEOdpO8itiFj/7fn5Do7fdycHZ/2/2HjsuD0unT9rQ98HoJ5EmJK9d91Cppj+bH4HWmkQSryi+r/1H1vXnlk2jz3Y4Am0FBGqWAoEKg42+FI4bdVGf+aHfjX9dkGxnMqs+3u7ChkaPHx9clDXDTI9a8xuRRq2irj/nD5VU7/R6/gwg0FptTMNFgfr8kbX8OTmzQKAtgUDNUizQhWPC6Q/S6/iyWfhbigU6+fTy+Eig+Q1l/83kmV48M/rtRgLVN9KPyd7cdaeLa/mz+Sz8sF4jfZFAPf7IGv68Z/rJDLPw7YBAzVLzCDTlt59782iqd6HvvuoINDuHzz4iS88yT44/EZ3bSC2BKpm0f4/e3JNGxTgNi7NPJMWrRH3J6TFvK3/kxuFJD1ubf+Nqg0DNovwMdE5paR9TdiyZP1nLCbTgM9DsoPPk6MR90+dHl3AvbCSGQCeXi48cE/eSmVlTUVtX6cyOedv4Iw+L/cWVSO2AQM1SJNDj0z6ik4PxLPzkUhcxSZQ87/D0XG76Gef4zTX5tDO/oWwDh8eb/G/G5/vzG4ki0Be3pB0+L703qy95hbPiXbR9chbW7FWivqToA43/Rx6XG2zvb1xtEKhZigRa0Aea69QcTlyX9tVPp+fHn2deNN5sQR9otoEz3zy9+mj0o/mNRBHo5GqnM7KrdF6KuWzQ9CPA3KvEfMmTs90T/Y8UH1mfM/8iUWNdaRCoWQov5RQXEE2OG6e/sOnDj2eL8WSHj8dHs0mjM/rxu+utyUHQzWORzm1odLFMpsv0i9nbXm4kjkCHL6WrWL5lfGyUFji4MM6B0mwOJfcqEV9SvGL0P/JkvmW4tb9xtUGgZlFeCz95h06vFpxOGIzJrJg8/4It8uG5DY0uMzpn/FLTz0vzG4kkUIDegkDN4lyN6S1Zu2dOaRv3npc2go4fSX8xnZIfr86UfvI5OgqZrkqe29BQfCx6WFzUlNsIAgXIg0BXAzELDwChQKCrAQIFiAACXQ0QKEAEEOhqgEABIoBAVwMEChABBLoaIFCACCBQAABPECgAgCcIFADAEwQKAOAJAgUA8ASBAgB4gkABADxBoAAAniBQAABPECgAgCcIFADAEwQKAOAJAgUA8ASBAgB4gkABADxBoAAAniBQAABPECgAgCcIFADAEwQKAOAJAgUA8ASBAgB4gkABADxBoAAAniBQAABPECgAgCcIFADAEwQKAOAJAgUA8ASBAgB4gkABADxBoAAAniBQAABPECgAgCcIFADAk/8fD0BAcg3nXzgAAAAASUVORK5CYII=" width="672" />  In the above plot, the blue color points are null values. I can infer that cars of similar mpg and acceleration have similar horsepower. For a given missing value, I can look at the mpg of the car, its acceleration, look for its k nearest neighbors and get the cars horsepower.

  
I am using _preprocess_ function in _caret_ package for imputing NA’s. The _K_ value that I am taking is 20 (~ close to square root of number of variables) `library(caret)
preProcValues <- preProcess(cars_info %>% dplyr::select(mpg, cylinders, displacement, weight, acceleration, origin, horsepower),
                            method = c("knnImpute"),
                            k = 20,
                            knnSummary = mean)
impute_cars_info <- predict(preProcValues, cars_info,na.action = na.pass)` 

The _impute\_cars\_info_ data set will be normalized. To de-normalize and get the original data back:

`procNames <- data.frame(col = names(preProcValues$mean), mean = preProcValues$mean, sd = preProcValues$std)
for(i in procNames$col){
 impute_cars_info[i] <- impute_cars_info[i]*preProcValues$std[i]+preProcValues$mean[i] 
}` The imputed horsepower for the missing data points is:  


<table>
  <caption> Imputed data set </caption> <tr>
    <th>
      name
    </th>
    
    <th>
      year
    </th>
    
    <th>
      origin
    </th>
    
    <th>
      mpg
    </th>
    
    <th>
      cylinders
    </th>
    
    <th>
      displacement
    </th>
    
    <th>
      weight
    </th>
    
    <th>
      acceleration
    </th>
    
    <th>
      horsepower
    </th>
  </tr>
  
  <tr>
    <td>
      ford maverick
    </td>
    
    <td>
      74
    </td>
    
    <td>
      1
    </td>
    
    <td>
      21.0
    </td>
    
    <td>
      6
    </td>
    
    <td>
      200
    </td>
    
    <td>
      2875
    </td>
    
    <td>
      17.0
    </td>
    
    <td>
      93.60
    </td>
  </tr>
  
  <tr>
    <td>
      ford mustang cobra
    </td>
    
    <td>
      80
    </td>
    
    <td>
      1
    </td>
    
    <td>
      23.6
    </td>
    
    <td>
      4
    </td>
    
    <td>
      140
    </td>
    
    <td>
      2905
    </td>
    
    <td>
      14.3
    </td>
    
    <td>
      94.95
    </td>
  </tr>
  
  <tr>
    <td>
      ford pinto
    </td>
    
    <td>
      71
    </td>
    
    <td>
      1
    </td>
    
    <td>
      25.0
    </td>
    
    <td>
      4
    </td>
    
    <td>
      98
    </td>
    
    <td>
      2046
    </td>
    
    <td>
      19.0
    </td>
    
    <td>
      72.45
    </td>
  </tr>
  
  <tr>
    <td>
      renault 18i
    </td>
    
    <td>
      81
    </td>
    
    <td>
      2
    </td>
    
    <td>
      34.5
    </td>
    
    <td>
      4
    </td>
    
    <td>
      100
    </td>
    
    <td>
      2320
    </td>
    
    <td>
      15.8
    </td>
    
    <td>
      73.75
    </td>
  </tr>
  
  <tr>
    <td>
      renault lecar deluxe
    </td>
    
    <td>
      80
    </td>
    
    <td>
      2
    </td>
    
    <td>
      40.9
    </td>
    
    <td>
      4
    </td>
    
    <td>
      85
    </td>
    
    <td>
      1835
    </td>
    
    <td>
      17.3
    </td>
    
    <td>
      65.10
    </td>
  </tr>
</table> The actual hp for the cars are as follows: 

<table>
  <caption> Comparison </caption> <tr>
    <th>
      name
    </th>
    
    <th>
      year
    </th>
    
    <th>
      horsepower
    </th>
    
    <th>
      actual_hp
    </th>
    
    <th>
      difference
    </th>
  </tr>
  
  <tr>
    <td>
      ford maverick
    </td>
    
    <td>
      74
    </td>
    
    <td>
      93.60
    </td>
    
    <td>
      84
    </td>
    
    <td>
      9.60
    </td>
  </tr>
  
  <tr>
    <td>
      ford mustang cobra
    </td>
    
    <td>
      80
    </td>
    
    <td>
      94.95
    </td>
    
    <td>
      118
    </td>
    
    <td>
      23.05
    </td>
  </tr>
  
  <tr>
    <td>
      ford pinto
    </td>
    
    <td>
      71
    </td>
    
    <td>
      72.45
    </td>
    
    <td>
      100
    </td>
    
    <td>
      27.55
    </td>
  </tr>
  
  <tr>
    <td>
      renault 18i
    </td>
    
    <td>
      81
    </td>
    
    <td>
      73.75
    </td>
    
    <td>
      81
    </td>
    
    <td>
      7.25
    </td>
  </tr>
  
  <tr>
    <td>
      renault lecar deluxe
    </td>
    
    <td>
      80
    </td>
    
    <td>
      65.10
    </td>
    
    <td>
      51
    </td>
    
    <td>
      14.10
    </td>
  </tr>
</table>

Out of the 5 cars, I was able to impute horsepower for 2 cars with less than 10hp difference, one car within 15hp and two cars within 30hp difference. To get better results, I should use other imputation techniques. Generally these 5 cars are removed while doing any analysis. In R, you could find the removed data set as _mtcars_.