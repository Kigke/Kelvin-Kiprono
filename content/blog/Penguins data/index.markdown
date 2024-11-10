---
title: "ggplot2"
subtitle: "Introduction"
excerpt: "ggplot2 is an R package widely used for data visualization. Created by Hadley Wickham, it implements the Grammar of Graphics, which allows users to create complex multi-layered graphics by building them step-by-step. With ggplot2, you can create a wide range of visualizations, from simple scatter plots and bar charts to complex faceted plots.

Key Concepts:
  
Aesthetic Mappings (aes): Links data columns to visual properties (e.g., x-axis, y-axis, color, size).
Geoms (Geometric Objects): Specify the type of plot (e.g., geom_point() for scatter plots, geom_line() for line plots, geom_bar() for bar charts).
Layers: Plots are created by adding layers (e.g., points, lines, text) using the + operator.
Scales: Customize axes and legends (e.g., scale_x_continuous(), scale_color_manual()).
Faceting: Create multi-panel plots using facet_wrap() or facet_grid() to show subsets of data.
Themes: Modify the non-data elements like background, grid lines, and text with theme() and pre-defined themes such as theme_minimal() or theme_classic()."
date: 2024-05-26
author: "Kelvin Kiprono"
draft: false
images:
series:
tags:
categories:
layout: single
---


## Loading dataset


``` r
library(palmerpenguins)
library(tidyverse)
```

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
```


``` r
ggplot(data = penguins, aes(x = flipper_length_mm)) +
  geom_histogram(aes(fill = species), alpha = 0.5, position = "identity") +
  scale_fill_manual(values = c("darkorange","darkorchid","cyan4"))
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

```
## Warning: Removed 2 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />





