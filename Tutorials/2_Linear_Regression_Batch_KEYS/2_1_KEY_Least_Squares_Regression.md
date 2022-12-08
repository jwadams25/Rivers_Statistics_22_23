5_Least_Squares_Regression
================
Mr. Adams

- <a href="#overview" id="toc-overview">Overview</a>
- <a href="#goals" id="toc-goals">Goals</a>
- <a href="#libraries" id="toc-libraries">Libraries</a>
  - <a href="#opening-tasks-and-questions---run-the-following-code-chunk"
    id="toc-opening-tasks-and-questions---run-the-following-code-chunk"><strong>Opening
    Tasks and Questions - Run the following code chunk</strong></a>
- <a href="#1-structured-walk-through"
  id="toc-1-structured-walk-through">1: Structured Walk-Through</a>
  - <a href="#11-the-data" id="toc-11-the-data">1.1: The Data</a>
    - <a href="#11-tasks-and-questions" id="toc-11-tasks-and-questions">1.1:
      Tasks and Questions</a>
  - <a href="#12-the-plot" id="toc-12-the-plot">1.2: The Plot</a>
    - <a href="#12-tasks-and-questions" id="toc-12-tasks-and-questions">1.2:
      Tasks and Questions</a>
  - <a href="#13-the-model" id="toc-13-the-model">1.3: The Model</a>
    - <a href="#13-tasks-and-questions" id="toc-13-tasks-and-questions">1.3:
      Tasks and Questions</a>
  - <a href="#14-interpreting-the-model"
    id="toc-14-interpreting-the-model">1.4: Interpreting the Model</a>
    - <a href="#14-tasks-and-questions" id="toc-14-tasks-and-questions">1.4:
      Tasks and Questions</a>
  - <a href="#sources" id="toc-sources">Sources:</a>

# Overview

Now that you’ve built a baseline understanding of least squares
regressions, you will learn to build scatter plots and generate linear
models here in Posit.

***Start by changing YOUR NAME next to where it says author above.***

# Goals

***By the end of this tutorial you should be able to…***

1.  Build a scatter plot that has a linear model.

2.  Generate the equation of the linear model.

3.  Interpret the linear regression model.

4.  Add design elements to the scatter plot to improve the labels,
    colors, and alpha.

# Libraries

## **Opening Tasks and Questions - Run the following code chunk**

``` r
library(tidyverse)
library(openintro)
library(knitr)
```

# 1: Structured Walk-Through

## 1.1: The Data

We had a great discussion in class about the relationship between gift
aid and family income for freshman at Elmhurst College after reading
Chapter 7 in Introduction to Modern Statistics. Therefore, let’s start
by recreating the scatter plot and the linear model you saw in the
reading.

### 1.1: Tasks and Questions

``` r
?elmhurst
glimpse(elmhurst)
```

    ## Rows: 50
    ## Columns: 3
    ## $ family_income <dbl> 92.922, 0.250, 53.092, 50.200, 137.613, 47.957, 113.534,…
    ## $ gift_aid      <dbl> 21.720, 27.470, 27.750, 27.220, 18.000, 18.520, 13.000, …
    ## $ price_paid    <dbl> 14.280, 8.530, 14.250, 8.780, 24.000, 23.480, 23.000, 29…

#### a. What are the observational units and how many are there?

The observational units are 50 randomly selected students gift aid for
students at Elmhurst College.

#### b. What are the names of the two variables we will explore when answering the question, “Is there an association between family income and the amount of gift aid received?”

family_income

gift_aid

#### c. What is the predictor variable?

family_income

#### d. What is the outcome variable?

gift_aid

## 1.2: The Plot

You will see in the code below the structure matches the code we used to
make other data visualizations. You ask the computer to reference a
dataset, make a plot with certain aesthetics, make a certain type of
plot, and add labels.

### 1.2: Tasks and Questions

#### a. Replace NAME_OF_DATASET with the name of the dataset.

#### b. Replace PREDICTOR and OUTCOME with the name of each variable.

#### c. Change the labels for the x and y axes as well as the title.

Be sure to list the units.

``` r
elmhurst |>
  ggplot(aes(x = family_income, y = gift_aid)) +
  geom_point() +
  labs(
    x = "Family Income of the Student ($1000s)", 
    y = "Gift Aid ($1000s)",
    title = "Gift Aid vs Family Income"
    )
```

![](2_1_KEY_Least_Squares_Regression_files/figure-gfm/build%20a%20scatter%20plot-1.png)<!-- -->

## 1.3: The Model

As you know, adding a least squares regression line to the plot and
generating an equation allows you to better quantify the association
between the two numerical values. You will now do both of those things
in the following sections of this tutorial.

### 1.3: Tasks and Questions

#### a. Add the line representing the linear model to the scatter plot you just created.

#### To do this, type “lm” after where you see method = in the code chunk below.

*geom_smooth* is the function that adds the line and the *lm* code you
added stands for linear model. When you progress to higher levels of
statistics and data science, you will add in different types of models
while also using geom_smooth.

``` r
elmhurst |>
  ggplot(aes(x = family_income, y = gift_aid)) +
  geom_point() +
  geom_smooth(method = "lm" , se = FALSE) +
  labs(
    x = "Family Income of the Student ($1000s)", 
    y = "Gift Aid ($1000s)",
    title = "Gift Aid vs Family Income"
    )
```

    ## `geom_smooth()` using formula = 'y ~ x'

![](2_1_KEY_Least_Squares_Regression_files/figure-gfm/add%20the%20model-1.png)<!-- -->

#### b. Generate the intercept and slope of the model

#### To do this, replace NAME_OF_DATASET, PREDICTOR, and OUTCOME in the code chunk below.

``` r
lm(data = elmhurst, formula = gift_aid~family_income)
```

    ## 
    ## Call:
    ## lm(formula = gift_aid ~ family_income, data = elmhurst)
    ## 
    ## Coefficients:
    ##   (Intercept)  family_income  
    ##      24.31933       -0.04307

#### c. Write the equation in the space below.

gift_aid = 24.31933 - 0.04307\*family_income

#### d. Find the mean and standard deviation of each variable along with the correlation coefficient by changing PREDICTOR and OUTCOME in the code chunk below.

``` r
elmhurst |>
  summarise(
    mean_income = mean(family_income), 
    sd_income = sd(family_income), 
    mean_aid = mean(gift_aid), 
    sd_aid = sd(gift_aid),
    r = cor(gift_aid, family_income)
  )  |>
  mutate(
    r_squared = r^2
  )
```

    ## # A tibble: 1 × 6
    ##   mean_income sd_income mean_aid sd_aid      r r_squared
    ##         <dbl>     <dbl>    <dbl>  <dbl>  <dbl>     <dbl>
    ## 1        102.      63.2     19.9   5.46 -0.499     0.249

## 1.4: Interpreting the Model

Getting the numbers is only part of the battle. Interpreting the model
properly and then clearly communicating that to others is essential. You
will now practice doing just that.

### 1.4: Tasks and Questions

#### a. Use the slope coefficient to describe the direction of the association.

For each additional \$1,000 in family income, gift aid is predicted to
be lower, on average, by \$43.07.

For each additional \$10,000 in family income, gift aid is predicted to
be lower, on average, by \$430.07.

#### b. Use the R-squared value to describe the strength of the association.

About 25%, of the variation in gift aid that can be explained by the
linear model with the predictor variable family income.

#### c. If a family income of an incoming freshman student was \$125,000, how much gift aid would the model predict they’d receive. <u>***USE THE EQUATION to find this. DO NOT JUST LOOK AT THE SCATTER PLOT!!***</u> Remember r can be used as calculator.

Our model predicts that a family earning \$125,000 would receive about
\$18,935.58.

``` r
# find slope in thousands
-0.04307*10000
```

    ## [1] -430.7

``` r
# Make prediction
(24.31933+(-0.04307*125))*1000
```

    ## [1] 18935.58

## Sources:

<https://openintro-ims.netlify.app/model-slr.html>
<https://openintro.shinyapps.io/ims-03-model-04/#section-data-set-up>
