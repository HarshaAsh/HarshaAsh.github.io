---
id: 946
title: Linear Programming
date: 2019-08-14T01:03:24+05:30
author: Achyuthuni Harsha
excerpt: Linear programming in R along with sensitivity analysis and cool visualizations.
layout: post
guid: https://www.harshaash.com/?p=946
permalink: /linear-programming/
categories:
  - caret
  - Data Sciences
tags:
  - analysis
  - linear
  - lp
  - programming
  - R
---
# Linear programming and sensitivity analysis

#### Harsha Achyuthuni

#### 13/08/2019

## Simple minimization problem

This Problem is taken from [An Introduction to Management Science : Quantitative Approach to Decision Making](https://www.cengage.co.in/category/higher-education/business-economics/operation-decision-sciences/management-science/an-introduction-to-management-science-quantitative-approach-to-decision-making-wcd-96) book. It is the example problem at page 52, chapter 2,5.

In this blog I will try to understand how to solve simple linear programming problems using R.

**Problem**  
M&D Chemicals produces two products that are sold as raw materials to companies manufacturing bath soaps and laundry detergents. Based on an analysis of current inventory levels and potential demand for the coming month, M&D’s management specified that the combined production for products A and B must total at least 350 gallons. Separately, a major customer’s order for 125 gallons of product A must also be satisfied. Product A requires 2 hours of processing time per gallon and product B requires 1 hour of processing time per gallon. For the coming month, 600 hours of processing time are available. M&D’s objective is to satisfy these requirements at a minimum total production cost. Production costs are dollar 2 per gallon for product A and dollar 3 per gallon for product B.  
Suppose additionally there is a constraint that the maximum production for B is 400 gallons. **Solution**  
The decision variables and objective function for the problem is as follows:  
(x_A) = number of gallons of product A  
(x_B) = number of gallons of product B With production costs at 2 per gallon for product A and 3 per gallon for product B, the objective function that corresponds to the minimization of the total production cost can be written as  
[ Min( 2x\_A + 3x\_B) ] The different constraints for the problem will be as follows:  
1. To satisfy the major customer’s demand for 125 gallons of product A, we know A must be at least 125.  
[ x_A geq 125 ] 2. The combined production for both products must total at least 350 gallons  
[ x\_A + x\_B geq 350 ] 3. The available processing time must not exceed 600 hours  
[ 2x\_A+x\_B leq 600 ] 4. The production of B cannot exceed 400 gallons  
[x_b leq 400] 5. As the production of A or B cannot be negative.  
[ x\_A geq 0, x\_B geq 0 ] 

#### Formulation Combining all the constraints, the LP can be written as:

  
[Min (2x\_A + 3x\_B) ] Subject to constraints: 

| A | B |       | RHS |
| - | - | ----- | --- |
| 1 |   | (geq) | 125 |
| 1 | 1 | (geq) | 350 |
| 2 | 1 | (leq) | 600 |
|   | 1 | (leq) | 400 |

#### Graphical solution Plotting the constraints I get the shaded region as the intersection region which satisfies all the constraints. Solutions that satisfy all the constraints are termed feasible solutions, and the shaded region is called the feasible solution region, or simply the feasible region.

  
<img src="data:image/png;base64,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" width="672" /> From the above plot, I observe that (x_b < 400) is a redundant constraint.  
To find the minimum-cost solution, we now draw the objective function line corresponding to a particular total cost value. For example, we might start by drawing the line (2x\_A + 3x\_B = 1200). This line is shown in below simulation. <figure></figure> 

If the above simulation is not clear or does not load on your screen, then please refer to  [LP Minimisation](https://harshaash.shinyapps.io/lp_minimisatiion/)

Clearly, some points in the feasible region would provide a total cost of $1200. To find the values of A and B that provide smaller total cost values, we move the objective function line in a lower left direction until, if we moved it any farther, it would be entirely outside the feasible region. Note that the objective function line (2x\_A + 3x\_B = 800) intersects the feasible region at the extreme point (x\_A = 250) and (x\_B = 100). This extreme point provides the minimum-cost solution with an objective function value of 800.

Therefore the ideal production to minimize cost should be to produce 250 gallons of A and 100 gallons of B.

#### Solution in R

In R, LP_solve is implemented through the lpSolve and lpSolveAPI packages. Using the lpSolve package, I can solve a linear programming problem as follows:

`library(lpSolve)
# A matrix of LHS of constraints (except the non negative)
constraints.LHS <- matrix(c(1,0,
              1,1,
              2,1,
              0,1), nrow = 4, byrow = TRUE)
# A list of RHS of constraints (except the non negative)  
RHS <- c(125, 350, 600,400)
# A list of the constraints directions (except the non negative)  
constranints_direction  <- c(">=", ">=", "<=", '<=')
# A list of objective function coefficients
objective.fxn <- c(2,3)
# Find the optimal solution
optimum <-  lp(direction="min",
               objective.in = objective.fxn,
               const.mat = constraints.LHS,
               const.dir = constranints_direction,
               const.rhs = RHS,
               all.int = T,
               compute.sens = TRUE)` 

The result of the above(after formatting) is:

`## Success: the objective function is 800` 

<table>
  <caption> Variables </caption> <tr>
    <th>
      Variable
    </th>
    
    <th>
      Optimum.Value
    </th>
    
    <th>
      Reduced.Cost
    </th>
    
    <th>
      Objective.coefficient
    </th>
    
    <th>
      Allowable.decrease
    </th>
    
    <th>
      Allowable.Increase
    </th>
  </tr>
  
  <tr>
    <td>
      A
    </td>
    
    <td>
      250
    </td>
    
    <td>
      0
    </td>
    
    <td>
      2
    </td>
    
    <td>
      -1e+30
    </td>
    
    <td>
      3
    </td>
  </tr>
  
  <tr>
    <td>
      B
    </td>
    
    <td>
      100
    </td>
    
    <td>
      0
    </td>
    
    <td>
      3
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1e+30
    </td>
  </tr>
</table>

<table>
  <caption> Constraints </caption> <tr>
    <th>
      Constraint
    </th>
    
    <th>
      Dual.Value
    </th>
    
    <th>
      Slack.Surplus
    </th>
    
    <th>
      RHS.Value
    </th>
    
    <th>
      Allowable.Decrease.to
    </th>
    
    <th>
      Allowable.Increase.to
    </th>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td>
      0
    </td>
    
    <td>
      125
    </td>
    
    <td>
      125
    </td>
    
    <td>
      -1e+30
    </td>
    
    <td>
      1e+30
    </td>
  </tr>
  
  <tr>
    <td>
      2
    </td>
    
    <td>
      4
    </td>
    
    <td>
      0
    </td>
    
    <td>
      350
    </td>
    
    <td>
      300
    </td>
    
    <td>
      475
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <td>
      -1
    </td>
    
    <td>
      0
    </td>
    
    <td>
      600
    </td>
    
    <td>
      475
    </td>
    
    <td>
      700
    </td>
  </tr>
  
  <tr>
    <td>
      4
    </td>
    
    <td>
      0
    </td>
    
    <td>
      -300
    </td>
    
    <td>
      400
    </td>
    
    <td>
      -1e+30
    </td>
    
    <td>
      1e+30
    </td>
  </tr>
  
  <tr>
    <td>
      5
    </td>
    
    <td>
      0
    </td>
    
    <td>
      250
    </td>
    
    <td>
      0
    </td>
    
    <td>
      -1e+30
    </td>
    
    <td>
      1e+30
    </td>
  </tr>
  
  <tr>
    <td>
      6
    </td>
    
    <td>
      0
    </td>
    
    <td>
      100
    </td>
    
    <td>
      0
    </td>
    
    <td>
      -1e+30
    </td>
    
    <td>
      1e+30
    </td>
  </tr>
</table>

#### Sensitivity analysis Sensitivity analysis is the study of how the changes in the coefficients of an optimization model affect the optimal solution. Using sensitivity analysis, we can answer questions such as the following:

  
1. How will a change in a coefficient of the objective function affect the optimal solution?  
2. How will a change in the right-hand-side value for a constraint affect the optimal solution? From the above solution, I observe the following  
1. The current price coefficient of A is 2 and the current price coefficient of B is 3. The optimal solution will remain the same even if the price of A is 3 keeping the price of B constant, or if the price of B is 2 keeping A constant. This can be visualized above.  
2. The binding constraints ie: processing time and production of both products have a Slack/Surplus values of zero. The other non binding constraints have positive/negative slack values. Slack values represent the unused capacity.  
3. The dual value associated with a constraint is the change in the optimal value of the solution per unit increase in the right-hand side of the constraint. For example, if I increased the minimum production constraint from 350 to 351, The cost of production will increase by 4 dollars. Similarly if I could increase the available processing time to 601 hours instead of 600 hours, the cost will decrease by 1 dollar. The range in which this increase or decrease is applicable is also given. This can be visualized in the above simulation.