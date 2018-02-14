---
layout: post
title: Advanced R Shiny Topics
tags: R Shiny
comments: True
excerpt_separator: <!--more-->
---

In my [previous post](http://tianwei-zhang.github.io/Building-Shiny-Apps), I gave a tutorial on building a very simple R Shiny app. Today, we are going to talk about some advanced topics. 

# Changing the Theme
Although you can change the layout of your Shiny app, most of the apps will have the same look and feel. You can quickly make your app look unique by adding a bootstrap CSS file.

<!--more-->

According to Wikipedia,

>Bootstrap is a free and open-source collection of tools for creating websites and web applications. It contains HTML- and CSS-based design templates for typography, forms, buttons, navigation and other interface components, as well as optional JavaScript extensions.

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
Placing a logo on your Shiny app will make it look much more polished, and it is easy to do so with the `navbarPage` layout. In bootstrap.css, we make the following modification:
```
nav{
   background: url('logo.png') no-repeat left center;
   background-size: 120px 120px;
}
```

Logo.png is stored in the www folder and it will appear in the top-left corner of the app.

## Progress Bar
If your computation takes a long time to finish, Shiny provides this nice feature to display a progress bar. I use the simpler version `withProgress` like this:

```
output$plot.ui=renderUI({
	withProgress(message='Generating plot...',
					plotOutput('plot')
					)
})
```

![Progress Bar](/assets/progress.png)

It is a nice feature, but the pale blue background and the font do not always go well with your selected theme. It took me a while to find out, but here is how you can change it.

In your bootstrap.css file, you can add the following lines:

```
.shiny-progress .progress-text {
  position: absolute;
  right: 10px;
  height: 30px;
  width: 170px;
  background-color: #ffffff;
  margin: 0px;
  padding: 2px 3px;
  opacity: 0.85;
  font-size: 18px;
}
```

With this, you can change the background color, font size, and even the opacity of your progress message box.
