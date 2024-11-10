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


``` r
sample_data1_a <- sample_data1 %>% 
  mutate(sba =
           if_else(m3a=='yes' |
                   m3b=='yes' |
                   m3c=='yes' |
                   m3d=='yes',
                   1,0,0))
```

``` r
count(sample_data1_a,sba)
```

```
## # A tibble: 2 × 2
##     sba     n
##   <dbl> <int>
## 1     0   605
## 2     1  2072
```

``` r
## Constructing Inequality dimensions
## Mothers age
```

``` r
str(sample_data1_a$v012)
```

```
##  num [1:2677] 31 24 37 26 37 34 32 35 24 31 ...
```

``` r
##Categorizing mothers age into 3 subgroups

sample_data1_b <- sample_data1_a %>% 
  mutate(mage=
           as.factor(case_when(
             v012 < 20 ~ '15 - 19 years',
             v012 >= 20 ~ '20 - 34 years',
             v012 >=35 & v012 <= 49 ~ '34 - 49 years'
           )))
```

``` r
count(sample_data1_b,mage)
```

```
## # A tibble: 2 × 2
##   mage              n
##   <fct>         <int>
## 1 15 - 19 years    72
## 2 20 - 34 years  2605
```

``` r
levels(sample_data1_b$mage)
```

```
## [1] "15 - 19 years" "20 - 34 years"
```

``` r
## Socioeconomic status (variable v190)
sample_data_1d <- sample_data1_b %>%
  mutate(quintile =
           fct_recode(v190,
                      "Quintile 1 (poorest)" = "poorest",
                      "Quintile 2" = "poorer",
                      "Quintile 3" = "middle",
                      "Quintile 4" = "richer",
                      "Quintile 5 (richest)" = "richest")
  )

count(sample_data_1d, quintile)
```

```
## # A tibble: 5 × 2
##   quintile                 n
##   <fct>                <int>
## 1 Quintile 3             491
## 2 Quintile 2             508
## 3 Quintile 1 (poorest)   747
## 4 Quintile 4             476
## 5 Quintile 5 (richest)   455
```



``` r
## Mother's education (variable v149)
count(sample_data_1d, v149)
```

```
## # A tibble: 6 × 2
##   v149                     n
##   <chr>                <int>
## 1 complete primary       469
## 2 complete secondary     805
## 3 higher                 493
## 4 incomplete primary     216
## 5 incomplete secondary   647
## 6 no education            47
```

``` r
sample_data_1e <- sample_data_1d %>%
  mutate(educatt =
           fct_recode(v149,
                      "No or primary education" = "no education",
                      "No or primary education" = "incomplete primary",
                      "No or primary education" = "complete primary",
                      "Secondary or higher education" = "incomplete secondary",
                      "Secondary or higher education" = "complete secondary",
                      "Secondary or higher education" = "higher")
  )

count(sample_data_1e, educatt)
```

```
## # A tibble: 2 × 2
##   educatt                           n
##   <fct>                         <int>
## 1 No or primary education         732
## 2 Secondary or higher education  1945
```



``` r
## Place of residence (variable v025)
sample_data_1f <- sample_data_1e %>%
  mutate(urban =
           fct_recode(v025,
                      "Urban" = "urban",
                      "Rural" = "rural")
  )

count(sample_data_1f, urban)
```

```
## # A tibble: 2 × 2
##   urban     n
##   <fct> <int>
## 1 Rural  1353
## 2 Urban  1324
```



``` r
## Finalizing data object preparation by selecting specified variables
sample_data_2 <- sample_data_1f %>%
  select(psu,
         weight,
         strata,
         sba,
         mage,
         quintile,
         educatt,
         urban)
```



``` r
view(sample_data_2)
```







