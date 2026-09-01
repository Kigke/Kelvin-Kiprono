---
title: "Python in RStudio"
subtitle: ""
excerpt: "RStudio isn't just for R — it has built-in support for Python through the reticulate package, letting you run Python code, share objects between R and Python, and use Python-based tools (pandas, matplotlib, scikit-learn) without leaving RStudio."
date: 2026-09-01
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---

``` r
library(reticulate)
```

```
## Warning: package 'reticulate' was built under R version 4.4.3
```


``` r
reticulate::use_virtualenv("my-python",required=TRUE)
```


``` r
reticulate::virtualenv_install(envname ="my-python","pandas",ignore_installed = FALSE,pip_options = character())
```

```
## Using virtual environment "my-python" ...
```

```
## + "C:/Users/hp/Documents/.virtualenvs/my-python/Scripts/python.exe" -m pip install --upgrade --no-user pandas
```


