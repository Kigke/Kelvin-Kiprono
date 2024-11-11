---
title: "Disaggregated data from surveys"
subtitle: "How to analyze survey data."
excerpt: ""
date: 2024-09-24
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---


Disaggregated data from surveys involves breaking down survey responses into smaller, more specific groups based on different characteristics or categories. This allows for more detailed analysis and helps to identify patterns, trends, or disparities that may not be visible in the aggregated data. The process of disaggregation can reveal important insights, particularly when working with diverse populations or when the goal is to make data-driven decisions that are inclusive and representative of different groups.

### How Disaggregated Data is Created from Surveys

- Survey Design:

Before collecting data, the survey needs to be designed with questions that allow for the segmentation of responses. These questions should ask for variables that can be categorized, such as age, gender, region, or income.

- Data Collection:

During data collection, responses are recorded in a way that each respondent's answers can be associated with specific demographic or other contextual variables.

- Data Segmentation:

After the survey is completed, the data is analyzed by dividing it into sub-groups. This can be done by categorizing respondents according to different criteria:
  - Demographic Variables: Age, gender, ethnicity, education, occupation, etc.
  - Geographic Variables: Region, urban vs. rural, country, etc.
  - Behavioral Variables: Employment status, health behaviors, or purchasing patterns.

- Analysis of Disaggregated Data:

Once the data is segmented, it is analyzed to reveal how different groups within the survey sample respond to specific questions. This allows for comparisons to be made between groups. For example, you might compare how men and women responded to a question on workplace satisfaction or how different income groups feel about healthcare access.

## Examples of Disaggregated Data from Surveys

- Income and Education Level in a Survey about Access to Technology:

   - Aggregated Data: 70% of survey respondents report having access to a computer.
   - Disaggregated Data:
   
     - 85% of individuals with a high school education or less report having access to a computer.
     - 95% of individuals with a college degree or higher report having access to a computer.
     - 60% of respondents with an annual income under $20,000 report having access to a computer, while 80% of those earning above $50,000 have access.

## Why Disaggregate Survey Data?

- Identifying Inequalities and Disparities:

Disaggregation allows you to identify differences between groups that might not be evident in the overall data. For example, if there are significant gaps in satisfaction between men and women, or if rural populations have less access to services, this can inform targeted interventions.

- Targeted Decision Making:

Policy makers and businesses can use disaggregated data to make decisions that are more specific to the needs of certain groups. For instance, a government might use disaggregated survey data on healthcare to allocate more resources to underserved areas.

- Improving Program Design:

Disaggregated data helps organizations tailor their programs to meet the needs of specific sub-groups. For example, a nonprofit working on educational programs might disaggregate data by age or socioeconomic status to design programs that address the unique challenges of different populations.

- Transparency and Accountability:

Disaggregation can help ensure that all groups, especially marginalized or underrepresented populations, are considered in the data analysis and that they are not overlooked in decision-making processes.

## Common Variables for Disaggregation in Survey Data
- Demographic Variables: Age, gender, income level, educational attainment, family status.
- Geographic Variables: Urban vs. rural, region, country, neighborhood.
- Health and Disability Variables: Chronic conditions, disability status.
- Ethnic or Cultural Background: Race, ethnicity, or cultural affiliation.
- Socioeconomic Variables: Employment status, income level, job sector.


## Preparing data for analysis


``` r
library(readxl)
sample_data_1<- read_excel("C:/Users/hp/Downloads/sample_data_1_1_.xlsx")
```

## Exploring the data

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
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
library(dplyr)
library(haven)
```
Using glimpse form the dplyr package we are able to see how our data looks like.Also using head() and tail() e can see the first five rows and last 5 rows.


``` r
glimpse(sample_data_1)
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
head(sample_data_1,5)
```

```
## # A tibble: 5 × 21
##      id   psu weight strata       v012 v025  v149  v190  b4    b5      b19 m3a  
##   <dbl> <dbl>  <dbl> <chr>       <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
## 1     1  1427  1.25  south kali…    31 rural inco… poor… fema… yes      28 no   
## 2     2  1859  0.188 maluku rur…    24 rural inco… poor… fema… yes      27 no   
## 3     3   891  1.89  central ja…    37 urban inco… midd… fema… yes      26 no   
## 4     4  1652  0.789 south sula…    26 rural inco… poor… male  yes      50 no   
## 5     5    20  0.359 aceh rural     37 rural comp… poor… male  yes      29 no   
## # ℹ 9 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>
```

``` r
tail(sample_data_1,5)
```

```
## # A tibble: 5 × 21
##      id   psu weight strata       v012 v025  v149  v190  b4    b5      b19 m3a  
##   <dbl> <dbl>  <dbl> <chr>       <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
## 1  2673  1366  1.07  west kalim…    36 rural comp… poor… male  yes      24 no   
## 2  2674  1294  0.360 east nusa …    29 rural comp… poor… male  yes      28 no   
## 3  2675   346  1.99  south suma…    32 rural inco… rich… fema… yes      10 no   
## 4  2676  1734  0.375 gorontalo …    28 rural comp… poor… male  yes      26 no   
## 5  2677   812  1.78  central ja…    36 urban comp… rich… fema… yes      52 no   
## # ℹ 9 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>
```

Obtaining the summary to get the picture of our data


``` r
summary(sample_data_1)
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

## Sample sizes for education subgroup


``` r
sample_data_1 %>%
  group_by(v149) %>%
  summarise(n())
```

```
## # A tibble: 6 × 2
##   v149                 `n()`
##   <chr>                <int>
## 1 complete primary       469
## 2 complete secondary     805
## 3 higher                 493
## 4 incomplete primary     216
## 5 incomplete secondary   647
## 6 no education            47
```

## Sample sizes and proportion of records for education subgroup


``` r
sample_data_1 %>%
  group_by(v149) %>%
  summarise(n = n()) %>%
  mutate(p = n/sum(n))
```

```
## # A tibble: 6 × 3
##   v149                     n      p
##   <chr>                <int>  <dbl>
## 1 complete primary       469 0.175 
## 2 complete secondary     805 0.301 
## 3 higher                 493 0.184 
## 4 incomplete primary     216 0.0807
## 5 incomplete secondary   647 0.242 
## 6 no education            47 0.0176
```

## Constructing health indicators (skilled birth attendance)

``` r
sample_data_1a <- sample_data_1 %>%
  mutate(sba =
           if_else(m3a == "yes"|
                   m3b == "yes"|
                   m3c == "yes"|
                   m3d == "yes",
                   1,0)
         )
```

# Tabulate *sba* variable (skilled birth attendance)

``` r
count(sample_data_1a, sba)
```

```
## # A tibble: 3 × 2
##     sba     n
##   <dbl> <int>
## 1     0   594
## 2     1  2072
## 3    NA    11
```

# # Replacing missing values in *sba* with zeros and inspecting results

``` r
sample_data_1b <- sample_data_1a %>%
  mutate(sba =
           if_else(m3a == "yes"|
                   m3b == "yes"|
                   m3c == "yes"|
                   m3d == "yes",
                   1,0,0)
         )
count(sample_data_1b, sba)
```

```
## # A tibble: 2 × 2
##     sba     n
##   <dbl> <int>
## 1     0   605
## 2     1  2072
```

# Inspecting R objects

``` r
sample_data_1b
```

```
## # A tibble: 2,677 × 22
##       id   psu weight strata      v012 v025  v149  v190  b4    b5      b19 m3a  
##    <dbl> <dbl>  <dbl> <chr>      <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
##  1     1  1427  1.25  south kal…    31 rural inco… poor… fema… yes      28 no   
##  2     2  1859  0.188 maluku ru…    24 rural inco… poor… fema… yes      27 no   
##  3     3   891  1.89  central j…    37 urban inco… midd… fema… yes      26 no   
##  4     4  1652  0.789 south sul…    26 rural inco… poor… male  yes      50 no   
##  5     5    20  0.359 aceh rural    37 rural comp… poor… male  yes      29 no   
##  6     6  1962  1.35  papua rur…    34 rural inco… poor… male  yes      19 no   
##  7     7  1618  0.782 south sul…    32 urban high… midd… fema… yes      59 no   
##  8     8  1063  2.36  east java…    35 rural inco… poor… male  yes       1 no   
##  9     9  1567  0.348 central s…    24 rural comp… rich… male  yes       4 no   
## 10    10   536  0.977 jakarta u…    31 urban high… rich… male  yes       6 no   
## # ℹ 2,667 more rows
## # ℹ 10 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>, sba <dbl>
```

``` r
head(sample_data_1b$sba , n = 10)
```

```
##  [1] 0 0 0 1 1 0 1 0 0 1
```

## Constructing inequality dimensions

# Mother's age categories (variable v012)

``` r
summary(sample_data_1b$v012)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   15.00   26.00   31.00   30.91   36.00   49.00
```

``` r
sample_data_1c <- sample_data_1b %>%
  mutate(mage =
           as.factor(case_when(
             v012 < 20 ~ '15-19 years',
             v012 >= 20 & v012 <= 34 ~ '20-34 years',
             v012 >= 35 & v012 <= 49 ~ '35-49 years')
           )
  )

levels(sample_data_1c$mage)
```

```
## [1] "15-19 years" "20-34 years" "35-49 years"
```

``` r
count(sample_data_1c, mage)
```

```
## # A tibble: 3 × 2
##   mage            n
##   <fct>       <int>
## 1 15-19 years    72
## 2 20-34 years  1793
## 3 35-49 years   812
```

## Socioeconomic status (variable v190)

``` r
sample_data_1d <- sample_data_1c %>%
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
## Mother's education (variable v149)

``` r
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

## Place of residence (variable v025)


``` r
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
## Finalizing data object preparation by selecting specified variables


``` r
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

