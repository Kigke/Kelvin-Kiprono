---
title: "Exploring Air Quality in New York: A Predictive Analysis of Ozone Levels Using Environmental Factors"
subtitle: ""
excerpt: ""
date: 2024-09-12
author: "Kelvin Kiprono"
draft: false
tags:
- Statistical Data Analysis
categories:
- Linear Regression

---

For this analysis, we will explore the airquality dataset, which provides daily air quality measurements in New York from May to September 1973. The dataset includes variables such as Ozone, Solar.R (solar radiation), Wind, Temp (temperature), and the month and day of the observation. Our objective is to analyze the relationships between air quality and weather-related factors, focusing on predicting the levels of Ozone, a key indicator of air pollution.

We will begin by cleaning the data, handling missing values, and performing exploratory data analysis (EDA) to better understand the distribution of variables and their correlations. Subsequently, we will build a linear regression model to predict Ozone levels based on other relevant environmental factors. Through this process, we aim to uncover key insights that could inform further studies on air quality and its environmental determinants.

## Loading Data


``` r
data("airquality")
str(airquality)
```

```
## 'data.frame':	153 obs. of  6 variables:
##  $ Ozone  : int  41 36 12 18 NA 28 23 19 8 NA ...
##  $ Solar.R: int  190 118 149 313 NA NA 299 99 19 194 ...
##  $ Wind   : num  7.4 8 12.6 11.5 14.3 14.9 8.6 13.8 20.1 8.6 ...
##  $ Temp   : int  67 72 74 62 56 66 65 59 61 69 ...
##  $ Month  : int  5 5 5 5 5 5 5 5 5 5 ...
##  $ Day    : int  1 2 3 4 5 6 7 8 9 10 ...
```

``` r
head(airquality)
```

```
##   Ozone Solar.R Wind Temp Month Day
## 1    41     190  7.4   67     5   1
## 2    36     118  8.0   72     5   2
## 3    12     149 12.6   74     5   3
## 4    18     313 11.5   62     5   4
## 5    NA      NA 14.3   56     5   5
## 6    28      NA 14.9   66     5   6
```

## Data Cleaning and Handling Missing Values

First, we begin by inspecting the airquality dataset and handling the missing values. The Ozone variable contains some missing values, which we will address before proceeding with further analysis.

## Check for missing values in Ozone

``` r
sum(is.na(airquality$Ozone))  # Count of missing values
```

```
## [1] 37
```
## Remove rows with missing values

``` r
cleaned_data <- na.omit(airquality)
cleaned_data
```

```
##     Ozone Solar.R Wind Temp Month Day
## 1      41     190  7.4   67     5   1
## 2      36     118  8.0   72     5   2
## 3      12     149 12.6   74     5   3
## 4      18     313 11.5   62     5   4
## 7      23     299  8.6   65     5   7
## 8      19      99 13.8   59     5   8
## 9       8      19 20.1   61     5   9
## 12     16     256  9.7   69     5  12
## 13     11     290  9.2   66     5  13
## 14     14     274 10.9   68     5  14
## 15     18      65 13.2   58     5  15
## 16     14     334 11.5   64     5  16
## 17     34     307 12.0   66     5  17
## 18      6      78 18.4   57     5  18
## 19     30     322 11.5   68     5  19
## 20     11      44  9.7   62     5  20
## 21      1       8  9.7   59     5  21
## 22     11     320 16.6   73     5  22
## 23      4      25  9.7   61     5  23
## 24     32      92 12.0   61     5  24
## 28     23      13 12.0   67     5  28
## 29     45     252 14.9   81     5  29
## 30    115     223  5.7   79     5  30
## 31     37     279  7.4   76     5  31
## 38     29     127  9.7   82     6   7
## 40     71     291 13.8   90     6   9
## 41     39     323 11.5   87     6  10
## 44     23     148  8.0   82     6  13
## 47     21     191 14.9   77     6  16
## 48     37     284 20.7   72     6  17
## 49     20      37  9.2   65     6  18
## 50     12     120 11.5   73     6  19
## 51     13     137 10.3   76     6  20
## 62    135     269  4.1   84     7   1
## 63     49     248  9.2   85     7   2
## 64     32     236  9.2   81     7   3
## 66     64     175  4.6   83     7   5
## 67     40     314 10.9   83     7   6
## 68     77     276  5.1   88     7   7
## 69     97     267  6.3   92     7   8
## 70     97     272  5.7   92     7   9
## 71     85     175  7.4   89     7  10
## 73     10     264 14.3   73     7  12
## 74     27     175 14.9   81     7  13
## 76      7      48 14.3   80     7  15
## 77     48     260  6.9   81     7  16
## 78     35     274 10.3   82     7  17
## 79     61     285  6.3   84     7  18
## 80     79     187  5.1   87     7  19
## 81     63     220 11.5   85     7  20
## 82     16       7  6.9   74     7  21
## 85     80     294  8.6   86     7  24
## 86    108     223  8.0   85     7  25
## 87     20      81  8.6   82     7  26
## 88     52      82 12.0   86     7  27
## 89     82     213  7.4   88     7  28
## 90     50     275  7.4   86     7  29
## 91     64     253  7.4   83     7  30
## 92     59     254  9.2   81     7  31
## 93     39      83  6.9   81     8   1
## 94      9      24 13.8   81     8   2
## 95     16      77  7.4   82     8   3
## 99    122     255  4.0   89     8   7
## 100    89     229 10.3   90     8   8
## 101   110     207  8.0   90     8   9
## 104    44     192 11.5   86     8  12
## 105    28     273 11.5   82     8  13
## 106    65     157  9.7   80     8  14
## 108    22      71 10.3   77     8  16
## 109    59      51  6.3   79     8  17
## 110    23     115  7.4   76     8  18
## 111    31     244 10.9   78     8  19
## 112    44     190 10.3   78     8  20
## 113    21     259 15.5   77     8  21
## 114     9      36 14.3   72     8  22
## 116    45     212  9.7   79     8  24
## 117   168     238  3.4   81     8  25
## 118    73     215  8.0   86     8  26
## 120    76     203  9.7   97     8  28
## 121   118     225  2.3   94     8  29
## 122    84     237  6.3   96     8  30
## 123    85     188  6.3   94     8  31
## 124    96     167  6.9   91     9   1
## 125    78     197  5.1   92     9   2
## 126    73     183  2.8   93     9   3
## 127    91     189  4.6   93     9   4
## 128    47      95  7.4   87     9   5
## 129    32      92 15.5   84     9   6
## 130    20     252 10.9   80     9   7
## 131    23     220 10.3   78     9   8
## 132    21     230 10.9   75     9   9
## 133    24     259  9.7   73     9  10
## 134    44     236 14.9   81     9  11
## 135    21     259 15.5   76     9  12
## 136    28     238  6.3   77     9  13
## 137     9      24 10.9   71     9  14
## 138    13     112 11.5   71     9  15
## 139    46     237  6.9   78     9  16
## 140    18     224 13.8   67     9  17
## 141    13      27 10.3   76     9  18
## 142    24     238 10.3   68     9  19
## 143    16     201  8.0   82     9  20
## 144    13     238 12.6   64     9  21
## 145    23      14  9.2   71     9  22
## 146    36     139 10.3   81     9  23
## 147     7      49 10.3   69     9  24
## 148    14      20 16.6   63     9  25
## 149    30     193  6.9   70     9  26
## 151    14     191 14.3   75     9  28
## 152    18     131  8.0   76     9  29
## 153    20     223 11.5   68     9  30
```
Alternatively, impute missing values with the mean (if preferred)

- airquality$Ozone[is.na(airquality$Ozone)] <- mean(airquality$Ozone, na.rm = TRUE)

The dataset contains missing values, particularly in the Ozone variable. We address these missing values by removing rows with NA values using na.omit() or by imputing missing values with the mean of the Ozone variable. This ensures we have a complete dataset to work with.

## Exploratory Data Analysis (EDA)

Next, we perform exploratory data analysis to understand the distribution of variables and relationships between them.

``` r
library(ggplot2)
ggplot(cleaned_data,aes(Ozone)) +
  geom_histogram(bins = 30,colour = "red") +
  ggtitle("Histogram of Ozone Levels")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

``` r
ggplot(cleaned_data,aes(Temp))+
  geom_histogram(bins = 30,colour = "blue") + 
  ggtitle("Histogram of Temperature Levels")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

``` r
ggplot(cleaned_data,aes(Temp,Ozone)) +
  geom_point() +
  ggtitle("Ozone vs Temperature")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

``` r
ggplot(cleaned_data,aes(Solar.R,Ozone)) +
  geom_point() +
  ggtitle("Solar Radiation vs Ozone ")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
In the EDA phase, we generate summary statistics and visualizations to understand the data better. Histograms of Ozone and Temp show the distribution of these variables, while scatter plots reveal the relationships between Ozone and other variables like Temp and Solar.R. We also calculate the correlation matrix to identify any linear relationships between numeric variables. These steps help us understand the patterns in the data before building predictive models.

## Building a Linear Regression Model

After cleaning and exploring the data, we build a linear regression model to predict Ozone levels based on environmental factors like Solar.R, Wind, and Temp.

``` r
model <- lm(Ozone ~ Solar.R + Wind + Temp, data = cleaned_data)
summary(model)
```

```
## 
## Call:
## lm(formula = Ozone ~ Solar.R + Wind + Temp, data = cleaned_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -40.485 -14.219  -3.551  10.097  95.619 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -64.34208   23.05472  -2.791  0.00623 ** 
## Solar.R       0.05982    0.02319   2.580  0.01124 *  
## Wind         -3.33359    0.65441  -5.094 1.52e-06 ***
## Temp          1.65209    0.25353   6.516 2.42e-09 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 21.18 on 107 degrees of freedom
## Multiple R-squared:  0.6059,	Adjusted R-squared:  0.5948 
## F-statistic: 54.83 on 3 and 107 DF,  p-value: < 2.2e-16
```
## Model Summary

The linear regression model was fitted with Ozone as the dependent variable and Solar.R, Wind, and Temp as independent variables.

##Key Findings: 

- Intercept: The intercept is -64.34, which represents the estimated ozone level when all predictors (solar radiation, wind, and temperature) are zero.

- Solar.R: The coefficient for Solar.R is 0.05982, indicating that for each unit increase in solar radiation, the ozone level is expected to increase by approximately 0.05982 units. The p-value of 0.01124 suggests that solar radiation is a statistically significant predictor of ozone levels at the 5% significance level.

- Wind: The coefficient for Wind is -3.33359, implying that for each unit increase in wind speed, the ozone level is expected to decrease by about 3.33 units. The p-value of 1.52e-06 is highly significant, indicating that wind is a strong predictor of ozone levels.

- Temp: The coefficient for Temp is 1.65209, meaning that for each unit increase in temperature, the ozone level is expected to increase by approximately 1.65 units. The p-value of 2.42e-09 indicates that temperature is also a highly significant predictor.

##Model Fit: 

- Residual Standard Error: The residual standard error of 21.18 tells us about the typical size of the residuals (i.e., the typical difference between the observed and predicted ozone levels). A lower value would suggest a better fit, but this value is relatively moderate.

- R-squared: The Multiple R-squared value of 0.6059 indicates that approximately 60.6% of the variability in ozone levels is explained by the model. The Adjusted R-squared of 0.5948 adjusts for the number of predictors and is slightly lower, but still suggests a reasonably good fit for the data.

- F-statistic: The F-statistic is 54.83 with a p-value of < 2.2e-16, which indicates that the model as a whole is statistically significant, meaning the independent variables together do a good job of explaining ozone levels.

## Interpretation:

The results suggest that:

- Temperature, solar radiation, and wind all have significant impacts on ozone levels in New York.
- Solar radiation and temperature are positively related to ozone levels, meaning that higher solar radiation and warmer temperatures lead to higher ozone concentrations.
- Wind speed, on the other hand, has a negative relationship with ozone levels, suggesting that stronger winds are associated with lower ozone concentrations.
- The model has a decent fit (with an R-squared of around 60%), but there may still be unexplained variability, which is typical in environmental datasets. Further refinement or additional variables could potentially improve the model’s predictive power.

## Model Diagnostics and Evaluation

To ensure the model is valid, we perform diagnostic checks, including evaluating the residuals to confirm the assumptions of linear regression.

``` r
par(mfrow = c(2, 2))
plot(model)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />
Q-Q Residual plot - Residuals are approximately normal, and the normality assumption holds.




