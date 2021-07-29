Course Project: Shiny Application and Reproducible Pitch
========================================================
author: Xavier Aguiar
date: 7/29/2021
autosize: true

Step 1: Manipulating the ui.R Document
========================================================

For more details on authoring R presentations please visit <https://support.rstudio.com/hc/en-us/articles/200486468>.

- This is the user-interface definition of a Shiny web application. You can run the application by clicking 'Run App' above.

- Find out more about building applications with Shiny here: http://shiny.rstudio.com/

- We first want to install shiny with the command "library(shiny)"

This is the R Code I implemented on the ui.R file to develop a Random Number Plot
========================================================


```r
#install shiny
library(shiny)

# Define server logic required to implement graph plot
shinyUI(fluidPage(
    titlePanel("Plot Random Numbers"),
    sidebarLayout(
        sidebarPanel(
            numericInput("numeric", "How Many Random Numbers Should be Plotted?", 
                         value = 1000, min = 1, max = 1000, step = 1),
            sliderInput("sliderX", "Pick Minimum and Maximum X Values",
                        -100, 100, value = c(-50, 50)),
            sliderInput("sliderY", "Pick Minimum and Maximum Y Values",
                        -100, 100, value = c(-50, 50)),
            checkboxInput("show_xlab", "Show/Hide X Axis Label", value = TRUE),
            checkboxInput("show_ylab", "Show/Hide Y Axis Label", value = TRUE),
            checkboxInput("show_title", "Show/Hide Title")
        ),
        mainPanel(
            h3("Graph of Random Points"),
            plotOutput("plot1")
        )
    )
))
```

<!--html_preserve--><div class="container-fluid">
<h2>Plot Random Numbers</h2>
<div class="row">
<div class="col-sm-4">
<form class="well" role="complementary">
<div class="form-group shiny-input-container">
<label class="control-label" id="numeric-label" for="numeric">How Many Random Numbers Should be Plotted?</label>
<input id="numeric" type="number" class="form-control" value="1000" min="1" max="1000" step="1"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" id="sliderX-label" for="sliderX">Pick Minimum and Maximum X Values</label>
<input class="js-range-slider" id="sliderX" data-skin="shiny" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" id="sliderY-label" for="sliderY">Pick Minimum and Maximum Y Values</label>
<input class="js-range-slider" id="sliderY" data-skin="shiny" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_xlab" type="checkbox" checked="checked"/>
<span>Show/Hide X Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_ylab" type="checkbox" checked="checked"/>
<span>Show/Hide Y Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_title" type="checkbox"/>
<span>Show/Hide Title</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8" role="main">
<h3>Graph of Random Points</h3>
<div id="plot1" class="shiny-plot-output" style="width:100%;height:400px;"></div>
</div>
</div>
</div><!--/html_preserve-->



This is the server logic of a Shiny web application. You can run the application by clicking 'Run App' on Rstudio.
========================================================


```r
#Install Shiny
library(shiny)

# Define server logic required to implement graph plot
shinyServer(function(input, output) {
    output$plot1 <- renderPlot({
        set.seed(2016-05-25)
        number_of_points <- input$numeric
        minX <- input$sliderX[1]
        maxX <- input$sliderX[2]
        minY <- input$sliderY[1]
        maxY <- input$sliderY[2]
        dataX <- runif(number_of_points, minX, maxX)
        dataY <- runif(number_of_points, minY, maxY)
        xlab <- ifelse(input$show_xlab, "X Axis", "")
        ylab <- ifelse(input$show_ylab, "Y Axis", "")
        main <- ifelse(input$show_title, "Title", "")
        plot(dataX, dataY, xlab = xlab, ylab = ylab, main = main,
             xlim = c(-100, 100), ylim = c(-100, 100))
    })
})
```


My Final Slide With my Random Number Generating Plot of note: Its not sexy but it works
========================================================

<!--html_preserve--><div class="container-fluid">
<h2>Plot Random Numbers</h2>
<div class="row">
<div class="col-sm-4">
<form class="well" role="complementary">
<div class="form-group shiny-input-container">
<label class="control-label" id="numeric-label" for="numeric">How Many Random Numbers Should be Plotted?</label>
<input id="numeric" type="number" class="form-control" value="1000" min="1" max="1000" step="1"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" id="sliderX-label" for="sliderX">Pick Minimum and Maximum X Values</label>
<input class="js-range-slider" id="sliderX" data-skin="shiny" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" id="sliderY-label" for="sliderY">Pick Minimum and Maximum Y Values</label>
<input class="js-range-slider" id="sliderY" data-skin="shiny" data-type="double" data-min="-100" data-max="100" data-from="-50" data-to="50" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-drag-interval="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_xlab" type="checkbox" checked="checked"/>
<span>Show/Hide X Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_ylab" type="checkbox" checked="checked"/>
<span>Show/Hide Y Axis Label</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="show_title" type="checkbox"/>
<span>Show/Hide Title</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8" role="main">
<h3>Graph of Random Points</h3>
<div id="plot1" class="shiny-plot-output" style="width:100%;height:400px;"></div>
</div>
</div>
</div><!--/html_preserve-->
