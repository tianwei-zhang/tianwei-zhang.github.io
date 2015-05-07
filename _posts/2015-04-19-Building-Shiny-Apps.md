---
layout: post
title: Building R Shiny Applications
comments: True
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

	*  `pageWithSidebar()` specifies the page template, in this case a page with a sidebar consisted of three panels.
		*  The `headerPanel` prints a title.
		*  The `sidebarPanel` constructs a sidebar on the left.
		*  The `mainPanel` outputs a large panel on the right.

If we run the code above, our app looks like this:
![Demo App Screenshot2](/assets/shiny2.tiff)

#Sidebar/Input
Next, let's add user input options to the sidebar. We want to use two dropdown meuns to allow users to select a vendor and a customer. In order to do so, we add `selectInput` to the `sidebarPanel`. The first string (e.g. 'selected\_vendor') is the variable name for that user input. For example, if user selects 'Vendor 1', `input$selected_vendor` will equal to 'Vendor 1'. The second string (e.g. 'Vendor: ') will be printed before the dropdown menu. The last component lists the available options for users to choose. 

```
#ui.R
library(shiny)
shinyUI(
  pageWithSidebar(
    headerPanel('Hello World'),
    sidebarPanel(
      selectInput('selected_vendor','Vendor: ',c('Vendor 1', 'Vendor 2')),
      selectInput('selected_customer','Customer: ',c('Customer 1', 'Customer 2'))
      ),
    mainPanel()
    )
  )
```

![Demo App Screenshot3](/assets/shiny3.png)
 
 We can add a slider bar using the following code:
 
 ```
 sliderInput('a_number','Select a Number: ',min=1,max=100,value=50)
 ```
 ![Demo App Screenshot4](/assets/shiny4.tiff)
 
#Output
Now let's talk about how to construct the output. In this case, let's start with putting a plot in the `mainPanel`. To do so, we add the following part to the ui.R. 

```
mainPanel(
  plotOutput('plot1')
)
```

Since we want to output a plot, we use `plotOutput`. There are different types of outputs avaiable for R Shiny. For example, you can print a table with `tableOutput` or a html file with `htmlOutput`. The string 'plot1' is the name for this output that we will refer to later. 

In order to generate the output, let's switch to server.R. 

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

You can use any ploting packages such as [ggplot2](http://ggplot2.org) or [rCharts](http://rcharts.io), just load the packages at the beginning of the code. As you can see, there are two "input variables" for `shinyServer`, **input** and **output**. We can access the user inputs (e.g. vendor and customer) via input$variable\_name. In this tutorial, we can call the user selected vendor and customer via `input$selected_vendor` and `input$selected_customer` (recall that selected\_vendor and selected\_customer are the names we gave to dropdown menus). **Output** is the collective list where all outputs are stored. `output$plot1=renderPlot({})` tells the program that plot1 is a graph and it is going to be rendered according to the R code within the brackets.    
 
![Demo App Screenshot5](/assets/shiny5.tiff) 

To make our app more exciting and useful, let's make our output reactive to the user input. We can refer to any existing (e.g. csv, Excel) files in our shiny app. I added a csv file named masked\_sales\_opportunity\_0501.csv in the same directory as ui.R and server.R. The first few lines are displayed below. 

| CUSTOMER_NAME | VENDOR_NAME | MASTER_PRODCAT     | NETAMT | 
|---------------|-------------|--------------------|--------| 
| Customer 1    | Vendor 1    | Product Category 1 | 4437   | 
| Customer 10   | Vendor 1    | Product Category 1 | 14794  | 
| Customer 11   | Vendor 1    | Product Category 1 | 4575   | 
| Customer 13   | Vendor 1    | Product Category 1 | 93     | 
| Customer 14   | Vendor 1    | Product Category 1 | 2921   | 
| Customer 15   | Vendor 1    | Product Category 1 | 4742   | 
| Customer 17   | Vendor 1    | Product Category 1 | 7406   | 

It has 20 unique customers and 10 unique vendors. Now we want to select a subset of the data and plot a histogram of NETAMT. 

```
library(shiny)
library(ggplot2)

data=read.csv('masked_sales_opportunity_0501.csv',header=TRUE)
shinyServer(function(input, output) {
  
  selectData=reactive({
    subdata=data[which(data$VENDOR_NAME==input$selected_vendor &
                       data$CUSTOMER_NAME==input$selected_customer),]
    return(subdata)
  })    
  
  output$plot=renderPlot({
   data=selectData()
   hist(data$NETAMT)
  })

})
```
Notice that `selectData` is a function using the `reactive({})` wrap. **Reactivity** is a key concept in R Shiny. It means that the returned object will react to user inputs. If I invoke input variables without wrapping it in an reactive environment like in the following code,

```
#Incorrect code
library(shiny)
library(ggplot2)

data=read.csv('masked_sales_opportunity_0501.csv',header=TRUE)
shinyServer(function(input, output) {
    
    subdata=data[which(data$VENDOR_NAME==input$selected_vendor &
                       data$CUSTOMER_NAME==input$selected_customer),]

  output$plot=renderPlot({
  
    })

})
```
it will output an error 
>Error in .getReactiveEnvironment()$currentContext() : 
  Operation not allowed without an active reactive context. (You tried to do something that can only be done from inside a reactive expression or observer.)
 
 With the the correct code, this is what we have:
 
![Demo App Screenshot6](/assets/shiny6.tiff) 
![Demo App Screenshot7](/assets/shiny7.tiff) 

