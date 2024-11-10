---
title: "ggplot2"
subtitle: ""
excerpt: "ggplot2 is an R package widely used for data visualization. Created by Hadley Wickham, it implements the Grammar of Graphics, which allows users to create complex multi-layered graphics by building them step-by-step. With ggplot2, you can create a wide range of visualizations, from simple scatter plots and bar charts to complex faceted plots."
 
date: 2024-05-26
author: "Kelvin Kiprono"
draft: false
images:
series:
tags:
categories:
layout: single
---

<link href="{{< blogdown/postref >}}index_files/htmltools-fill/fill.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>

## Loading dataset

``` r
library(palmerpenguins)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
ggplot(data = penguins, aes(x = flipper_length_mm)) +
  geom_histogram(aes(fill = species), alpha = 0.5, position = "identity") +
  scale_fill_manual(values = c("darkorange","darkorchid","cyan4"))
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

Plotly is an interactive graphing library for R that makes it easy to create interactive, web-ready visualizations. It is particularly useful for exploring data, sharing findings, and building dashboards with enhanced user experiences.

``` r
library(plotly)
```

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
Flipper <- ggplot(data = penguins, aes(x = flipper_length_mm)) +
  geom_histogram(aes(fill = species), alpha = 0.5, position = "identity") +
  scale_fill_manual(values = c("darkorange","darkorchid","cyan4"))
```

``` r
ggplotly(Flipper)
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 2 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"orientation":"v","width":[2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975],"base":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"x":[172.93103448275861,174.9655172413793,176.99999999999997,179.03448275862067,181.06896551724137,183.10344827586204,185.13793103448273,187.17241379310343,189.20689655172413,191.24137931034483,193.27586206896549,195.31034482758619,197.34482758620686,199.37931034482756,201.41379310344826,203.44827586206895,205.48275862068965,207.51724137931032,209.55172413793102,211.58620689655169,213.62068965517238,215.65517241379308,217.68965517241378,219.72413793103448,221.75862068965515,223.79310344827584,225.82758620689651,227.86206896551721,229.89655172413791,231.93103448275861],"y":[1,1,4,6,8,9,15,15,25,15,13,17,9,6,3,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0],"text":["count:  1<br />flipper_length_mm: 172.9310<br />species: Adelie","count:  1<br />flipper_length_mm: 174.9655<br />species: Adelie","count:  4<br />flipper_length_mm: 177.0000<br />species: Adelie","count:  6<br />flipper_length_mm: 179.0345<br />species: Adelie","count:  8<br />flipper_length_mm: 181.0690<br />species: Adelie","count:  9<br />flipper_length_mm: 183.1034<br />species: Adelie","count: 15<br />flipper_length_mm: 185.1379<br />species: Adelie","count: 15<br />flipper_length_mm: 187.1724<br />species: Adelie","count: 25<br />flipper_length_mm: 189.2069<br />species: Adelie","count: 15<br />flipper_length_mm: 191.2414<br />species: Adelie","count: 13<br />flipper_length_mm: 193.2759<br />species: Adelie","count: 17<br />flipper_length_mm: 195.3103<br />species: Adelie","count:  9<br />flipper_length_mm: 197.3448<br />species: Adelie","count:  6<br />flipper_length_mm: 199.3793<br />species: Adelie","count:  3<br />flipper_length_mm: 201.4138<br />species: Adelie","count:  1<br />flipper_length_mm: 203.4483<br />species: Adelie","count:  1<br />flipper_length_mm: 205.4828<br />species: Adelie","count:  1<br />flipper_length_mm: 207.5172<br />species: Adelie","count:  1<br />flipper_length_mm: 209.5517<br />species: Adelie","count:  0<br />flipper_length_mm: 211.5862<br />species: Adelie","count:  0<br />flipper_length_mm: 213.6207<br />species: Adelie","count:  0<br />flipper_length_mm: 215.6552<br />species: Adelie","count:  0<br />flipper_length_mm: 217.6897<br />species: Adelie","count:  0<br />flipper_length_mm: 219.7241<br />species: Adelie","count:  0<br />flipper_length_mm: 221.7586<br />species: Adelie","count:  0<br />flipper_length_mm: 223.7931<br />species: Adelie","count:  0<br />flipper_length_mm: 225.8276<br />species: Adelie","count:  0<br />flipper_length_mm: 227.8621<br />species: Adelie","count:  0<br />flipper_length_mm: 229.8966<br />species: Adelie","count:  0<br />flipper_length_mm: 231.9310<br />species: Adelie"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(255,140,0,0.5)","line":{"width":1.8897637795275593,"color":"transparent"}},"name":"Adelie","legendgroup":"Adelie","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975],"base":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"x":[172.93103448275861,174.9655172413793,176.99999999999997,179.03448275862067,181.06896551724137,183.10344827586204,185.13793103448273,187.17241379310343,189.20689655172413,191.24137931034483,193.27586206896549,195.31034482758619,197.34482758620686,199.37931034482756,201.41379310344826,203.44827586206895,205.48275862068965,207.51724137931032,209.55172413793102,211.58620689655169,213.62068965517238,215.65517241379308,217.68965517241378,219.72413793103448,221.75862068965515,223.79310344827584,225.82758620689651,227.86206896551721,229.89655172413791,231.93103448275861],"y":[0,0,1,0,2,0,1,7,4,5,7,10,9,4,7,3,3,1,3,1,0,0,0,0,0,0,0,0,0,0],"text":["count:  0<br />flipper_length_mm: 172.9310<br />species: Chinstrap","count:  0<br />flipper_length_mm: 174.9655<br />species: Chinstrap","count:  1<br />flipper_length_mm: 177.0000<br />species: Chinstrap","count:  0<br />flipper_length_mm: 179.0345<br />species: Chinstrap","count:  2<br />flipper_length_mm: 181.0690<br />species: Chinstrap","count:  0<br />flipper_length_mm: 183.1034<br />species: Chinstrap","count:  1<br />flipper_length_mm: 185.1379<br />species: Chinstrap","count:  7<br />flipper_length_mm: 187.1724<br />species: Chinstrap","count:  4<br />flipper_length_mm: 189.2069<br />species: Chinstrap","count:  5<br />flipper_length_mm: 191.2414<br />species: Chinstrap","count:  7<br />flipper_length_mm: 193.2759<br />species: Chinstrap","count: 10<br />flipper_length_mm: 195.3103<br />species: Chinstrap","count:  9<br />flipper_length_mm: 197.3448<br />species: Chinstrap","count:  4<br />flipper_length_mm: 199.3793<br />species: Chinstrap","count:  7<br />flipper_length_mm: 201.4138<br />species: Chinstrap","count:  3<br />flipper_length_mm: 203.4483<br />species: Chinstrap","count:  3<br />flipper_length_mm: 205.4828<br />species: Chinstrap","count:  1<br />flipper_length_mm: 207.5172<br />species: Chinstrap","count:  3<br />flipper_length_mm: 209.5517<br />species: Chinstrap","count:  1<br />flipper_length_mm: 211.5862<br />species: Chinstrap","count:  0<br />flipper_length_mm: 213.6207<br />species: Chinstrap","count:  0<br />flipper_length_mm: 215.6552<br />species: Chinstrap","count:  0<br />flipper_length_mm: 217.6897<br />species: Chinstrap","count:  0<br />flipper_length_mm: 219.7241<br />species: Chinstrap","count:  0<br />flipper_length_mm: 221.7586<br />species: Chinstrap","count:  0<br />flipper_length_mm: 223.7931<br />species: Chinstrap","count:  0<br />flipper_length_mm: 225.8276<br />species: Chinstrap","count:  0<br />flipper_length_mm: 227.8621<br />species: Chinstrap","count:  0<br />flipper_length_mm: 229.8966<br />species: Chinstrap","count:  0<br />flipper_length_mm: 231.9310<br />species: Chinstrap"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(153,50,204,0.5)","line":{"width":1.8897637795275593,"color":"transparent"}},"name":"Chinstrap","legendgroup":"Chinstrap","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975,2.0344827586206975],"base":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"x":[172.93103448275861,174.9655172413793,176.99999999999997,179.03448275862067,181.06896551724137,183.10344827586204,185.13793103448273,187.17241379310343,189.20689655172413,191.24137931034483,193.27586206896549,195.31034482758619,197.34482758620686,199.37931034482756,201.41379310344826,203.44827586206895,205.48275862068965,207.51724137931032,209.55172413793102,211.58620689655169,213.62068965517238,215.65517241379308,217.68965517241378,219.72413793103448,221.75862068965515,223.79310344827584,225.82758620689651,227.86206896551721,229.89655172413791,231.93103448275861],"y":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,8,15,8,12,20,11,13,11,5,5,4,9,1],"text":["count:  0<br />flipper_length_mm: 172.9310<br />species: Gentoo","count:  0<br />flipper_length_mm: 174.9655<br />species: Gentoo","count:  0<br />flipper_length_mm: 177.0000<br />species: Gentoo","count:  0<br />flipper_length_mm: 179.0345<br />species: Gentoo","count:  0<br />flipper_length_mm: 181.0690<br />species: Gentoo","count:  0<br />flipper_length_mm: 183.1034<br />species: Gentoo","count:  0<br />flipper_length_mm: 185.1379<br />species: Gentoo","count:  0<br />flipper_length_mm: 187.1724<br />species: Gentoo","count:  0<br />flipper_length_mm: 189.2069<br />species: Gentoo","count:  0<br />flipper_length_mm: 191.2414<br />species: Gentoo","count:  0<br />flipper_length_mm: 193.2759<br />species: Gentoo","count:  0<br />flipper_length_mm: 195.3103<br />species: Gentoo","count:  0<br />flipper_length_mm: 197.3448<br />species: Gentoo","count:  0<br />flipper_length_mm: 199.3793<br />species: Gentoo","count:  0<br />flipper_length_mm: 201.4138<br />species: Gentoo","count:  1<br />flipper_length_mm: 203.4483<br />species: Gentoo","count:  0<br />flipper_length_mm: 205.4828<br />species: Gentoo","count:  8<br />flipper_length_mm: 207.5172<br />species: Gentoo","count: 15<br />flipper_length_mm: 209.5517<br />species: Gentoo","count:  8<br />flipper_length_mm: 211.5862<br />species: Gentoo","count: 12<br />flipper_length_mm: 213.6207<br />species: Gentoo","count: 20<br />flipper_length_mm: 215.6552<br />species: Gentoo","count: 11<br />flipper_length_mm: 217.6897<br />species: Gentoo","count: 13<br />flipper_length_mm: 219.7241<br />species: Gentoo","count: 11<br />flipper_length_mm: 221.7586<br />species: Gentoo","count:  5<br />flipper_length_mm: 223.7931<br />species: Gentoo","count:  5<br />flipper_length_mm: 225.8276<br />species: Gentoo","count:  4<br />flipper_length_mm: 227.8621<br />species: Gentoo","count:  9<br />flipper_length_mm: 229.8966<br />species: Gentoo","count:  1<br />flipper_length_mm: 231.9310<br />species: Gentoo"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(0,139,139,0.5)","line":{"width":1.8897637795275593,"color":"transparent"}},"name":"Gentoo","legendgroup":"Gentoo","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.228310502283104,"r":7.3059360730593621,"b":40.182648401826491,"l":37.260273972602747},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[168.86206896551721,236],"tickmode":"array","ticktext":["180","200","220"],"tickvals":[180,200,220],"categoryorder":"array","categoryarray":["180","200","220"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176002,"zeroline":false,"anchor":"y","title":{"text":"flipper_length_mm","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.25,26.25],"tickmode":"array","ticktext":["0","5","10","15","20","25"],"tickvals":[0,5,10,15,20,25],"categoryorder":"array","categoryarray":["0","5","10","15","20","25"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176002,"zeroline":false,"anchor":"x","title":{"text":"count","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.8897637795275593,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.68949771689498},"title":{"text":"species","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"44f862c91a69":{"x":{},"fill":{},"type":"bar"}},"cur_data":"44f862c91a69","visdat":{"44f862c91a69":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
