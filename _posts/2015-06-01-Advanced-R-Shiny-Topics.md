---
layout: post
title: Advanced R Shiny Topics
tags: R Shiny
comments: True
excerpt_separator: <!--more-->
---

In my [previous post](http://tianwei-zhang.github.io/2015/04/19/Building-Shiny-Apps/), I gave a tutorial on building a very simple R Shiny app. Today, we are going to talk about some advanced topics. 

<!--more-->

# Changing the Theme
Although you can change the layout of your Shiny app, most of the apps will have the same look and feel with the default theme. You can quickly make your app look unique by adding a bootstrap CSS file. According to Wikipedia, 

>Bootstrap is a free and open-source collection of tools for creating websites and web applications. It contains HTML- and CSS-based design templates for typography, forms, buttons, navigation and other interface components, as well as optional JavaScript extensions. The bootstrap framework aims to ease web development.

In order to use a custom bootstrap template, we can modify the following code in **ui.R**. 

```
shinyUI(navbarPage('App Title',theme='bootstrap.css',
	tabPanel('Panel 1',
		sidebarPanel(
		),
		mainPanel(
		)
	)
))
```
Where do we store this bootstrap.css file? We will create a www folder in the app directory. 

* ui.R
* server.R
* www
	* bootstrap.css

How do we find themes for Bootstrap? [Bootswatch](http://bootswatch.com) is a great website that offers many free themes to download. From here, the possibility is endless. You can start making small modifications to an existing css file or even building your own bootstrap theme from scratch. 

![Bootswatch](/assets/shiny_ad_1.tiff)

## Adding a Logo
Having a logo on our Shiny app will make it look much more polished, and it is easy to do so with the `navbarPage` layout. In bootstrap.css, we modify the `nav` part:

```
nav{
   background: url('logo.png') no-repeat left center;
   background-size: 120px 120px;
}
```

Logo.png is stored in the www folder and it will appear in the top-left corner of the app. 

# selectizeInput v.s. selectInput

to be continued...

