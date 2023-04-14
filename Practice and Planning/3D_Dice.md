3D Printed Dice
================

- <a href="#overview" id="toc-overview">Overview</a>
- <a href="#packages" id="toc-packages">Packages</a>
- <a href="#gray---20-gyroid-infill" id="toc-gray---20-gyroid-infill">Gray
  - 20% Gyroid Infill</a>
- <a href="#magenta---20-cubic-infill"
  id="toc-magenta---20-cubic-infill">Magenta - 20% Cubic Infill</a>
- <a href="#green-with-gold-group-1---20-lightning-infill"
  id="toc-green-with-gold-group-1---20-lightning-infill">Green with Gold
  Group 1 - 20% Lightning Infill</a>
- <a href="#green-with-gold-group-2"
  id="toc-green-with-gold-group-2">Green with Gold Group 2</a>
- <a href="#green-with-black---solid-100-infill"
  id="toc-green-with-black---solid-100-infill">Green with Black - solid,
  100% infill</a>
- <a href="#yellow---20-triangle-infill"
  id="toc-yellow---20-triangle-infill">Yellow - 20% Triangle Infill</a>

### Overview

Five 6-sided dice were printed using a 3D printer. Each dice was printed
using a different method. The goal of this study is to find out if any
of them are unfair die.

Students, in groups of two, rolled one dice 50 times, each time
recording the side in which in landed. Below is the data from each
group’s rolls and the corresponding chi-squared test.

### Packages

``` r
library(tidyverse)
library(openintro)
library(infer)
library(janitor)
library(knitr)
library(kableExtra)
library(gghighlight)
library(readr)
library(skimr)
```

### Gray - 20% Gyroid Infill

#### The rolls

``` r
gray_dice <- c(3, 4, 3, 4, 4, 1, 4, 4, 2, 2, 2, 3, 3, 2, 4, 4, 2, 1, 2, 2, 3, 4, 5, 6, 4, 2, 6, 1, 1, 3, 2, 3, 2, 4, 3, 1, 6, 1, 3, 2, 4, 2, 6, 2, 3, 1, 4, 4, 2, 6)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
gray_dice_data <- data.frame(
                      gray_dice = as.character(gray_dice)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
gray_count_tbl <- gray_dice_data |>

  count(gray_dice)|>

  mutate(proportion = n / sum(n)) 

gray_count_tbl
```

    ##   gray_dice  n proportion
    ## 1         1  7       0.14
    ## 2         2 14       0.28
    ## 3         3 10       0.20
    ## 4         4 13       0.26
    ## 5         5  1       0.02
    ## 6         6  5       0.10

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(gray_dice_data,
           response = gray_dice,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      14.8        5  0.0113

### Magenta - 20% Cubic Infill

#### The rolls

``` r
magenta_dice <- c(4, 2, 2, 6, 3, 5, 4, 4, 4, 3, 1, 6, 6, 4, 6, 5, 3, 6, 4, 4, 6, 5, 5, 5, 4, 4, 2, 5, 5, 2, 4, 5, 5, 6, 5, 5, 5, 2, 2, 1, 2, 4, 2, 3, 3, 1, 1, 3, 1, 4)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
magenta_dice_data <- data.frame(
                      magenta_dice = as.character(magenta_dice)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
magenta_count_tbl <- magenta_dice_data |>
  count(magenta_dice)|>
  mutate(proportion = n / sum(n)) 
magenta_count_tbl
```

    ##   magenta_dice  n proportion
    ## 1            1  5       0.10
    ## 2            2  8       0.16
    ## 3            3  6       0.12
    ## 4            4 12       0.24
    ## 5            5 12       0.24
    ## 6            6  7       0.14

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(magenta_dice_data,
           response = magenta_dice,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      5.44        5   0.365

### Green with Gold Group 1 - 20% Lightning Infill

#### The rolls

``` r
greengold_dice <- c(5,1,3,6,1,2,4,5,1,2,2,3,4,5,4,6,5,1,1,4,2,1,4,4,3,5,2,6,3,5,1,3,4,4,2,1,5,1,3,1,2,4,1,6,1,3,4,1,2,4)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
green_gold_dice_data <- data.frame(
                      greengold_dice = as.character(greengold_dice)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
green_gold_count_tbl <- green_gold_dice_data |>
  count(greengold_dice)|>
  mutate(proportion = n / sum(n)) 

green_gold_count_tbl
```

    ##   greengold_dice  n proportion
    ## 1              1 13       0.26
    ## 2              2  8       0.16
    ## 3              3  7       0.14
    ## 4              4 11       0.22
    ## 5              5  7       0.14
    ## 6              6  4       0.08

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(green_gold_dice_data,
           response = greengold_dice,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      6.16        5   0.291

### Green with Gold Group 2

#### The rolls

``` r
green_with_gold_dots <- c(5, 3, 4, 1, 5, 2, 1, 5, 2, 1, 5, 2, 2, 1, 4, 5, 5, 3, 4, 2, 6, 2, 2, 2, 6, 3, 5, 5, 3, 2, 6, 1, 2, 1, 4, 5, 4, 5, 1, 2, 2, 5, 1, 2, 6, 4, 6, 5, 2, 4)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
green_gold_dice_data_2 <- data.frame(
                      green_with_gold_dots = as.character(green_with_gold_dots)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
green_gold_count_tbl_2 <- green_gold_dice_data_2 |>
  count(green_with_gold_dots)|>
  mutate(proportion = n / sum(n)) 

green_gold_count_tbl_2
```

    ##   green_with_gold_dots  n proportion
    ## 1                    1  8       0.16
    ## 2                    2 14       0.28
    ## 3                    3  4       0.08
    ## 4                    4  7       0.14
    ## 5                    5 12       0.24
    ## 6                    6  5       0.10

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(green_gold_dice_data_2,
           response = green_with_gold_dots,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      9.28        5  0.0984

### Green with Black - solid, 100% infill

#### The rolls

``` r
green_dice_black_dots <- c(2,3,5,4,2,4,2,2,3,2,1,6,4,4,6,3,5,5,4,5,5,5,2,4,5,4,3,6,3,4,1,3,1,1,6,6,2,2,4,5,5,1,5,5,3,2,3,6,3,4)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
green_black_dice_data <- data.frame(
                      green_dice_black_dots = as.character(green_dice_black_dots)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
green_black_count_tbl <- green_black_dice_data |>
  count(green_dice_black_dots)|>
  mutate(proportion = n / sum(n)) 

green_black_count_tbl
```

    ##   green_dice_black_dots  n proportion
    ## 1                     1  5       0.10
    ## 2                     2  9       0.18
    ## 3                     3  9       0.18
    ## 4                     4 10       0.20
    ## 5                     5 11       0.22
    ## 6                     6  6       0.12

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(green_black_dice_data,
           response = green_dice_black_dots,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      3.28        5   0.657

### Yellow - 20% Triangle Infill

#### The Rolls

``` r
YELLOW <- c(6,4,2,2,5,2,1,4,1,6,2,4,2,6,4,1,5,5,1,4,2,5,6,1,3,2,1,2,3,4,1,2,5,1,3,6,3,6,3,1,6,6,2,1,6,5,6,4,5,2)
```

#### Convert the rolls into a data frame and the numbers into characterse rolls

``` r
yellow_dice_data <- data.frame(
                      YELLOW = as.character(YELLOW)
)
```

**A table showing the number and proportion of times the dice landed on
each side**

``` r
yellow_count_tbl <- yellow_dice_data |>
  count(YELLOW)|>
  mutate(proportion = n / sum(n)) 

yellow_count_tbl
```

    ##   YELLOW  n proportion
    ## 1      1 10       0.20
    ## 2      2 11       0.22
    ## 3      3  5       0.10
    ## 4      4  7       0.14
    ## 5      5  7       0.14
    ## 6      6 10       0.20

#### The Chi-Squared Test for Goodness of Fit

``` r
chisq_test(yellow_dice_data,
           response = YELLOW,
           p = c("1" = 1/6,
                 "2" = 1/6,
                 "3" = 1/6,
                 "4" = 1/6,
                 "5" = 1/6,
                 "6" = 1/6))
```

    ## # A tibble: 1 × 3
    ##   statistic chisq_df p_value
    ##       <dbl>    <dbl>   <dbl>
    ## 1      3.28        5   0.657
