---
id: 985
title: Inventory planning model
date: 2019-09-01T21:49:54+05:30
author: Achyuthuni Harsha
excerpt: A multi period integer programming model was used to predict when and by how much quantity a new purchase has to be done in a Kirana store.
layout: post
guid: https://www.harshaash.com/?p=985
permalink: /inventory-planning-model/
categories:
  - Data Sciences
tags:
  - CPLEX
  - inventory
  - kirana
  - optimisation
  - planning
  - prescriptive
---
 

Consider a simple problem of handling inventory in a store. In any store, there will be multiple items, and each item will have its own demand and supply constraints. In such scenario, how do we create a inventory management model?

This model was created for a kirana store. The store sold about 6000 different kind of items. The demand for each of these items is not constant and sporadic. I built a demand forecasting model which was about 80% accurate. The store already has some items ordered from different vendors which would arrive at a known time in the future. The current inventory can be calculated using the GST billing systems. The shop owner wanted to understand when and how much to order of each item so that he meets his demand.

Apart from meeting the demand, the owner wanted to maintain a safety stock of 20% for rainy days (literally). The total items ordered should not exceed the capacity of the store.

A multi period integer programming model was used to predict when and by how much quantity a new purchase has to be done. The objective was to reduce costs. Cost had two components, inventory cost and ordering cost. The code in CPLEX is given below <figure class="wp-block-image">

<img loading="lazy" width="1040" height="710" src="https://i1.wp.com/www.harshaash.website/wp-content/uploads/2019/09/image.png?fit=640%2C437&ssl=1" alt="" class="wp-image-989" srcset="https://www.harshaash.com/wp-content/uploads/2019/09/image.png 1040w, https://www.harshaash.com/wp-content/uploads/2019/09/image-300x205.png 300w, https://www.harshaash.com/wp-content/uploads/2019/09/image-768x524.png 768w, https://www.harshaash.com/wp-content/uploads/2019/09/image-1024x699.png 1024w" sizes="(max-width: 1040px) 100vw, 1040px" /> <figcaption> Inventory_planning.mod</figcaption></figure> 

A mock data to run the above file would be like below (.dat file)<figure class="wp-block-image">

<img loading="lazy" width="881" height="172" src="https://www.harshaash.com/wp-content/uploads/2019/09/image-2.png" alt="" class="wp-image-991" srcset="https://www.harshaash.com/wp-content/uploads/2019/09/image-2.png 881w, https://www.harshaash.com/wp-content/uploads/2019/09/image-2-300x59.png 300w, https://www.harshaash.com/wp-content/uploads/2019/09/image-2-768x150.png 768w" sizes="(max-width: 881px) 100vw, 881px" /> <figcaption>Inventory_planning.data</figcaption></figure> 

This model helped the store owner understand and plan for the shortfall in inventory.<figure class="wp-block-image">

<img loading="lazy" width="768" height="574" src="https://www.harshaash.com/wp-content/uploads/2019/09/kirana-store-768x574.jpg" alt="" class="wp-image-992" srcset="https://www.harshaash.com/wp-content/uploads/2019/09/kirana-store-768x574.jpg 768w, https://www.harshaash.com/wp-content/uploads/2019/09/kirana-store-768x574-300x224.jpg 300w" sizes="(max-width: 768px) 100vw, 768px" /> <figcaption>Kirana store</figcaption></figure>