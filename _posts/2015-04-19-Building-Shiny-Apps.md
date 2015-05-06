---
layout: post
title: Building R Shiny Applications
---

[R Shiny](http://shiny.rstudio.com) is a platform developed by RStudio that enables R users to develop **interative** web applications without knowing HTML or other programming languages. 

##Getting Started
First, we need to install the shiny package.
<pre><code>install.packages('shiny')</code></pre>
For every shiny app, there are two core components: **ui.R** and **server.R**. Roughly speaking, ui.R collects inputs and defines the look and feel of the app, and server.R determines outputs and performs all the backend calculations. In this tutorial, we will learn how to build a simplified version of [this demo application](https://infordsl.shinyapps.io/demo/). 

![Demo App Screenshot](/assets/shiny1.png)

Let's construct our first Shiny app!
##Constructing UI
For simple applications, ui.R and server.R are almost completely separate pieces. One can start building the UI component without worrying about the backend calculation. For now, let's only add the following lines to server.R
<pre><code>
\#server.R
library(shiny)
shinyServer(function(input, output) {

})
</code></pre>

For this tutorial, we want to build an app with a sidebar for inputs on the left and display output on the right. 
<pre><code>
\#ui.R
library(shiny)
shinyUI(
  pageWithSidebar(
    headerPanel('Hello World'),
    sidebarPanel(),
    mainPanel()
    )
  )
</code></pre>
There are three hiercharchy levels found in the code above. 

* `shinyUI()` is always required.

	*  `pageWithSidebar()` specifies the page template, in this case a page with a sidebar consisted with three panels.
		*  The `headerPanel` prints a title.
		*  The `sidebarPanel` constructs a sidebar on the left.
		*  The `mainPanel` outputs a large panel on the right.

If we run the code above, our app looks like this:
![Demo App Screenshot2](/assets/shiny2.tiff)


  


 
