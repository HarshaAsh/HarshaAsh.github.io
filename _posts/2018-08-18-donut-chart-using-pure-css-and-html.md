---
id: 437
title: Donut chart using pure CSS and HTML
date: 2018-08-18T21:29:40+05:30
author: Achyuthuni Sri Harsha
layout: post
guid: https://www.harshaash.com/?p=437
permalink: /donut-chart-using-pure-css-and-html/
categories:
  - Web development
tags:
  - analytics
  - CSS
  - donut
  - Javascript
---
Last week time spent  
&#9632; Cleaning data  
&#9632; Formulating hypothesis  
&#9632; EDA  
&#9632; Actual analytics

One of the ways of plotting numerical proportions in statistics is by using the donut chart.

In the above example, the time I spent working on a problem in the last week is shown.

Although I recommend using D3, Plotly or similar visualization libraries, creating a donut chart using pure HTML and CSS is a challenge for any web developer.

Below is the code for creating the above donut chart using pure CSS and HTML.

###### HTML

<pre>&lt;div&gt;
    &lt;div&gt;
        &lt;div&gt;
            &lt;div id="section1"&gt;
                &lt;div data-rel="170"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;div id="section2"&gt;
                &lt;div data-rel="20"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;div id="section3"&gt;
                &lt;div data-rel="113"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;div id="section4"&gt;
                &lt;div data-rel="-32"&gt;&lt;/div&gt;
            &lt;/div&gt;
            &lt;div&gt;&lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</pre>

###### CSS

<pre>.block {
    margin: 25px 25px 0 0;
    background: white;
    border-radius: 5px;
    float: left;
    width: 50%;
    overflow: hidden;
  }
  .donut-chart-block {
    overflow: hidden;
  }
  .donut-chart {
    position: relative;
    width: 200px;
    height: 200px;
    margin: 2rem auto;
    border-radius: 100%;
    float: left;
  }
  .donut-chart .center {
    background: white;
    position: absolute;
    top: 30px;
    left: 30px;
    height: 140px;
    width: 140px;
    border-radius: 70px;
  }
  .donut-chart .clip {
    border-radius: 50%;
    clip: rect(0px, 200px, 200px, 100px);
    height: 100%;
    position: absolute;
    width: 100%;
  }
  .item {
    border-radius: 50%;
    clip: rect(0px, 100px, 200px, 0px);
    height: 100%;
    position: absolute;
    width: 100%;
    font-family: monospace;
    font-size: 1.5rem;
  }
  #section1 {
    transform: rotate(0deg);
  }
  #section1 .item {
    background-color: #E64C65;
    transform: rotate(170deg);
  }
  #section2 {
    transform: rotate(170deg);
  }
  #section2 .item {
    background-color: #11A8AB;
    transform: rotate(20deg);
  }
  #section3 {
    transform: rotate(190deg);
  }
  #section3 .item {
    background-color: #4FC4F6;
    transform: rotate(113deg);
  }
  #section4 {
    transform: rotate(-32deg);
  }
  #section4 .item {
    background-color: #FCB150;
    transform: rotate(32deg);
  }</pre>