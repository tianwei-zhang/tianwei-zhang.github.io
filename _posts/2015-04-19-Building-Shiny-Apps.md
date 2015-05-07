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

```
#server.R
library(shiny)
shinyServer(function(input, output) {
})
```

For this tutorial, we want to build an app with a sidebar for inputs on the left and display output on the right. 

```
#ui.R
library(shiny)
shinyUI(
  pageWithSidebar(
    headerPanel('Hello World'),
    sidebarPanel(),
    mainPanel()
    )
  )
```
There are three hiercharchy levels found in the code above. 

* `shinyUI()` is always required.

	*  `pageWithSidebar()` specifies the page template, in this case a page with a sidebar consisted with three panels.
		*  The `headerPanel` prints a title.
		*  The `sidebarPanel` constructs a sidebar on the left.
		*  The `mainPanel` outputs a large panel on the right.

If we run the code above, our app looks like this:
![Demo App Screenshot2](/assets/shiny2.tiff)

#Sidebar/Input
Next, let's add user input options to the sidebar. We want to use two dropdown meuns to allow users to select a vendor and a customer. 

```
#ui.R
library(shiny)
shinyUI(
  pageWithSidebar(
    headerPanel('Hello World'),
    sidebarPanel(
      selectInput('selected\_vendor','Vendor: ',c('Vendor 1', 'Vendor 2')),
      selectInput('selected\_customer','Customer: ',c('Customer 1', 'Customer 2'))
      ),
    mainPanel()
    )
  )
```
 
In order to do so, we add `selectInput` to the `sidebarPanel`. The first string (e.g. 'selected\_vendor') is the variable name for that user input. For example, if user selects 'Vendor 1', `input$selected_vendor` will equal to 'Vendor 1'. The second string (e.g. 'Vendor: ') will be printed before the dropdown menu. The last component lists the available options for users to choose. 
![Demo App Screenshot3](/assets/shiny3.png)
 
 We can add a slider bar using the following code:
 
 ```
 sliderInput('a_number','Select a Number: ',min=1,max=100,value=50)
 ```
 ![Demo App Screenshot4](/assets/shiny4.tiff)
 
#Output
Now let's talk about how to construct output. In this case, let's start with putting a plot in the `mainPanel`. To do so, we add the following part to the ui.R. 

```
mainPanel(
  plotOutput('plot1')
)
```

Since we want to output a plot, we use `plotOutput`. There are different types of outputs avaiable for R Shiny. For example, you can print a table with `tableOutput` or a html file with `htmlOutput`. The string 'plot1' is the name for this plot that we will refer to later. 

In order to generate a plot for plot1, let's switch to server.R. 

```
#server.R
library(shiny)
library(ggplot2)
shinyServer(function(input, output) {

  output$plot1=renderPlot({
    qplot(1:9,1:9)
  })
  
})
```

You can use any ploting packages such as [ggplot2](http://ggplot2.org) or [rCharts](http://rcharts.io), just load the packages at the beginning of the code. As you can see, There are two "input variables" for `shinyServer`, **input** and **output**. We can access the user inputs (e.g. vendor and customer) via input$variable\_name. In this tutorial, we can call the user selected vendor and customer via `input$selected\_vendor` and `input$selected\_customer` (recall that selected\_vendor and selected\_customer are the names we gave to dropdown menus). **Output** is the collective list where all outputs should be stored. `output$plot1=renderPlot({})` tells the program that plot1 is a graph and it is going to be rendered according to the R code within the brackets.    
 
![Demo App Screenshot5](/assets/shiny5.tiff) 

To make our app more exciting and useful, let's make our output reactive to the user input.



 
