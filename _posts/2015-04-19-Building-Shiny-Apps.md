---
layout: post
title: Building R Shiny Applications
---

[R Shiny](http://shiny.rstudio.com) is a platform developed by RStudio that enables R users to develop **interative** web applications without knowing HTML or other programming languages. 

##Getting Started
First, we need to install the shiny package.
<pre><code>install.packages('shiny')</code></pre>
For every shiny app, there are two core components: **ui.R** and **server.R**. Roughly speaking, ui.R collects inputs and defines the look and feel of the app, and server.R determines outputs and performs all the backend calculations. In this tutorial, we will learn how to build the first part of [this demo application](https://infordsl.shinyapps.io/demo/). 

![Demo App Screenshot](/assets/shiny1.png)


  


 
