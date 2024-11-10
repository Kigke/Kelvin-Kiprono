---
title: "Disaggregated data from surveys"
subtitle: "How to analyze survey data."
excerpt: "Add tabbed sections with code and results."
date: 2024-09-24
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---


``` r
library(readxl)
sample_data1 <- read_excel("C:/Users/hp/Downloads/sample_data_1_1_.xlsx")
```

``` r
library(survey)
```

```
## Loading required package: grid
```

```
## Loading required package: Matrix
```

```
## Loading required package: survival
```

```
## 
## Attaching package: 'survey'
```

```
## The following object is masked from 'package:graphics':
## 
##     dotchart
```

``` r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ tidyr::expand() masks Matrix::expand()
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ✖ tidyr::pack()   masks Matrix::pack()
## ✖ tidyr::unpack() masks Matrix::unpack()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```



``` r
library(dplyr)
glimpse(sample_data1)
```

```
## Rows: 2,677
## Columns: 21
## $ id     <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, …
## $ psu    <dbl> 1427, 1859, 891, 1652, 20, 1962, 1618, 1063, 1567, 536, 1454, 1…
## $ weight <dbl> 1.253567, 0.187608, 1.889372, 0.788736, 0.358671, 1.354536, 0.7…
## $ strata <chr> "south kalimantan rural", "maluku rural", "central java urban",…
## $ v012   <dbl> 31, 24, 37, 26, 37, 34, 32, 35, 24, 31, 42, 36, 34, 39, 30, 28,…
## $ v025   <chr> "rural", "rural", "urban", "rural", "rural", "rural", "urban", …
## $ v149   <chr> "incomplete primary", "incomplete secondary", "incomplete secon…
## $ v190   <chr> "poorest", "poorest", "middle", "poorest", "poorer", "poorest",…
## $ b4     <chr> "female", "female", "female", "male", "male", "male", "female",…
## $ b5     <chr> "yes", "yes", "yes", "yes", "yes", "yes", "yes", "yes", "yes", …
## $ b19    <dbl> 28, 27, 26, 50, 29, 19, 59, 1, 4, 6, 49, 48, 28, 40, 31, 33, 15…
## $ m3a    <chr> "no", "no", "no", "no", "no", "no", "no", "no", "no", "no", "no…
## $ m3b    <chr> "no", "no", "no", "no", "yes", "no", "no", "no", "no", "yes", "…
## $ m3c    <chr> "no", "no", "no", "no", "no", "no", "yes", "no", "no", "yes", "…
## $ m3d    <chr> "no", "no", "no", "yes", "no", "no", "yes", "no", "no", "no", "…
## $ m3e    <chr> "no", "no", "no", "no", "no", "yes", "no", "yes", "yes", "no", …
## $ m3g    <chr> "yes", "yes", "yes", "no", "no", "no", "no", "yes", "no", "no",…
## $ m3h    <chr> "no", "no", "yes", "yes", "no", "yes", "no", "no", "no", "no", …
## $ m3k    <chr> "no", "no", "no", "no", "no", "no", "no", "no", "no", "no", "no…
## $ m3n    <chr> "no: some assistance", "no: some assistance", "no: some assista…
## $ h7     <chr> "vaccination date on card", "reported by mother", "no", NA, "re…
```

``` r
str(sample_data1)
```

```
## tibble [2,677 × 21] (S3: tbl_df/tbl/data.frame)
##  $ id    : num [1:2677] 1 2 3 4 5 6 7 8 9 10 ...
##  $ psu   : num [1:2677] 1427 1859 891 1652 20 ...
##  $ weight: num [1:2677] 1.254 0.188 1.889 0.789 0.359 ...
##  $ strata: chr [1:2677] "south kalimantan rural" "maluku rural" "central java urban" "south sulawesi rural" ...
##  $ v012  : num [1:2677] 31 24 37 26 37 34 32 35 24 31 ...
##  $ v025  : chr [1:2677] "rural" "rural" "urban" "rural" ...
##  $ v149  : chr [1:2677] "incomplete primary" "incomplete secondary" "incomplete secondary" "incomplete secondary" ...
##  $ v190  : chr [1:2677] "poorest" "poorest" "middle" "poorest" ...
##  $ b4    : chr [1:2677] "female" "female" "female" "male" ...
##  $ b5    : chr [1:2677] "yes" "yes" "yes" "yes" ...
##  $ b19   : num [1:2677] 28 27 26 50 29 19 59 1 4 6 ...
##  $ m3a   : chr [1:2677] "no" "no" "no" "no" ...
##  $ m3b   : chr [1:2677] "no" "no" "no" "no" ...
##  $ m3c   : chr [1:2677] "no" "no" "no" "no" ...
##  $ m3d   : chr [1:2677] "no" "no" "no" "yes" ...
##  $ m3e   : chr [1:2677] "no" "no" "no" "no" ...
##  $ m3g   : chr [1:2677] "yes" "yes" "yes" "no" ...
##  $ m3h   : chr [1:2677] "no" "no" "yes" "yes" ...
##  $ m3k   : chr [1:2677] "no" "no" "no" "no" ...
##  $ m3n   : chr [1:2677] "no: some assistance" "no: some assistance" "no: some assistance" "no: some assistance" ...
##  $ h7    : chr [1:2677] "vaccination date on card" "reported by mother" "no" NA ...
```

``` r
summary(sample_data1)
```

```
##        id            psu             weight           strata         
##  Min.   :   1   Min.   :   1.0   Min.   :0.06359   Length:2677       
##  1st Qu.: 670   1st Qu.: 451.0   1st Qu.:0.35909   Class :character  
##  Median :1339   Median :1022.0   Median :0.84843   Mode  :character  
##  Mean   :1339   Mean   : 993.2   Mean   :0.94872                     
##  3rd Qu.:2008   3rd Qu.:1522.0   3rd Qu.:1.41101                     
##  Max.   :2677   Max.   :1970.0   Max.   :5.40138                     
##       v012           v025               v149               v190          
##  Min.   :15.00   Length:2677        Length:2677        Length:2677       
##  1st Qu.:26.00   Class :character   Class :character   Class :character  
##  Median :31.00   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :30.91                                                           
##  3rd Qu.:36.00                                                           
##  Max.   :49.00                                                           
##       b4                 b5                 b19            m3a           
##  Length:2677        Length:2677        Min.   : 0.00   Length:2677       
##  Class :character   Class :character   1st Qu.:15.00   Class :character  
##  Mode  :character   Mode  :character   Median :30.00   Mode  :character  
##                                        Mean   :29.97                     
##                                        3rd Qu.:45.00                     
##                                        Max.   :59.00                     
##      m3b                m3c                m3d                m3e           
##  Length:2677        Length:2677        Length:2677        Length:2677       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      m3g                m3h                m3k                m3n           
##  Length:2677        Length:2677        Length:2677        Length:2677       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##       h7           
##  Length:2677       
##  Class :character  
##  Mode  :character  
##                    
##                    
## 
```



``` r
sample_data1 %>% 
  group_by(v149) %>% 
  summarise(n=n()) %>% 
  mutate(p=n/sum(n()))
```

```
## # A tibble: 6 × 3
##   v149                     n      p
##   <chr>                <int>  <dbl>
## 1 complete primary       469  78.2 
## 2 complete secondary     805 134.  
## 3 higher                 493  82.2 
## 4 incomplete primary     216  36   
## 5 incomplete secondary   647 108.  
## 6 no education            47   7.83
```


## But first, panelsets with R code chunks

{{< panelset class="greetings" >}}
{{< panel name="Plot" >}}

<img src="{{< blogdown/postref >}}index_files/figure-html/plot-1.png" width="672" />

{{< /panel >}}
{{< panel name="Code" >}}


``` r
plot(pressure)
```

{{< /panel >}}
{{< /panelset  >}}

## I'm half machine. I'm a monster.

It's a hug, Michael. I'm hugging you. I'm half machine. I'm a monster. There's only one man I've ever called a coward, and that's Brian Doyle Murray. No, what I'm calling you is a television actor. Bad news. Andy Griffith turned us down. He didn't like his trailer.

No, I did not kill Kitty. However, I am going to oblige and answer the nice officer's questions because I am an honest man with no secrets to hide. Guy's a pro. Really? __Did nothing cancel?__ *Get me a vodka rocks.* And a piece of toast.

## No… but I'd like to be asked!

Oh, you're gonna be in a coma, all right. Steve Holt! I hear the jury's still out on science. No, I did not kill Kitty. However, I am going to oblige and answer the nice officer's questions because I am an honest man with no secrets to hide.

1. Really? Did nothing cancel?
2. That's what it said on 'Ask Jeeves.'
3. Get me a vodka rocks. And a piece of toast.

### That's what it said on 'Ask Jeeves.'

Did you enjoy your meal, Mom? You drank it fast enough. What's Spanish for "I know you speak English?" Bad news. Andy Griffith turned us down. He didn't like his trailer. Really? Did nothing cancel? I care deeply for nature.

* Michael!
* No! I was ashamed to be SEEN with you. I like being with you.
* We just call it a sausage.

Well, what do you expect, mother? It's called 'taking advantage.' It's what gets you ahead in life. Now, when you do this without getting punched in the chest, you'll have more fun. No, I did not kill Kitty. However, I am going to oblige and answer the nice officer's questions because I am an honest man with no secrets to hide.

I'm half machine. I'm a monster. It's a hug, Michael. I'm hugging you. Guy's a pro. First place chick is hot, but has an attitude, doesn't date magicians. He'll want to use your yacht, and I don't want this thing smelling like fish.

He'll want to use your yacht, and I don't want this thing smelling like fish. Now, when you do this without getting punched in the chest, you'll have more fun. We just call it a sausage. Guy's a pro. Bad news. Andy Griffith turned us down. He didn't like his trailer.

There's only one man I've ever called a coward, and that's Brian Doyle Murray. No, what I'm calling you is a television actor. It's called 'taking advantage.' It's what gets you ahead in life. We just call it a sausage.

Michael! First place chick is hot, but has an attitude, doesn't date magicians. I've opened a door here that I regret. Guy's a pro.

Army had half a day. Michael! Now, when you do this without getting punched in the chest, you'll have more fun. Well, what do you expect, mother? Now, when you do this without getting punched in the chest, you'll have more fun.

But I bought a yearbook ad from you, doesn't that mean anything anymore? Oh, you're gonna be in a coma, all right. It's a hug, Michael. I'm hugging you. I've opened a door here that I regret.

There's only one man I've ever called a coward, and that's Brian Doyle Murray. No, what I'm calling you is a television actor. That's why you always leave a note! He'll want to use your yacht, and I don't want this thing smelling like fish.

I've opened a door here that I regret. Now, when you do this without getting punched in the chest, you'll have more fun. I care deeply for nature. It's called 'taking advantage.' It's what gets you ahead in life.

It's a hug, Michael. I'm hugging you. No… but I'd like to be asked! What's Spanish for "I know you speak English?" It's called 'taking advantage.' It's what gets you ahead in life. It's a hug, Michael. I'm hugging you.

I don't understand the question, and I won't respond to it. Really? Did nothing cancel? Did you enjoy your meal, Mom? You drank it fast enough. Bad news. Andy Griffith turned us down. He didn't like his trailer.


