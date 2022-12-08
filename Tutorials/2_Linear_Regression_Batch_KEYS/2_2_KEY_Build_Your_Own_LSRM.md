6_Build_Your_OwnLeast_Squares_Regression
================
YOUR NAME

- <a href="#overview" id="toc-overview">Overview</a>
- <a href="#goals" id="toc-goals">Goals</a>
- <a href="#libraries" id="toc-libraries">Libraries</a>
  - <a href="#opening-tasks-and-questions---run-the-following-code-chunk"
    id="toc-opening-tasks-and-questions---run-the-following-code-chunk"><strong>Opening
    Tasks and Questions - Run the following code chunk</strong></a>
- <a href="#the-question-you-will-explore"
  id="toc-the-question-you-will-explore">The Question you will
  explore:</a>
  - <a
    href="#are-textbooks-at-uclas-bookstore-overpriced-in-relation-to-the-same-ones-sold-on-amazon"
    id="toc-are-textbooks-at-uclas-bookstore-overpriced-in-relation-to-the-same-ones-sold-on-amazon">“Are
    textbooks at UCLA’s bookstore overpriced in relation to the same ones
    sold on Amazon?”</a>
- <a href="#1-build-your-own-scatter-plot-and-model"
  id="toc-1-build-your-own-scatter-plot-and-model">1: Build Your Own
  Scatter Plot and Model</a>
  - <a href="#11-learn-about-the-data" id="toc-11-learn-about-the-data">1.1:
    Learn about the Data</a>
  - <a href="#12-build-the-scatter-plot-with-the-linear-model-included"
    id="toc-12-build-the-scatter-plot-with-the-linear-model-included">1.2:
    Build the scatter plot with the linear model included</a>
  - <a href="#13-generate-the-equation-of-the-least-squares-regression-line"
    id="toc-13-generate-the-equation-of-the-least-squares-regression-line">1.3:
    Generate the equation of the least squares regression line.</a>
  - <a href="#14-generate-the-correlation-coefficient-and-r-squared"
    id="toc-14-generate-the-correlation-coefficient-and-r-squared">1.4:
    Generate the correlation coefficient and r-squared</a>
  - <a
    href="#15-using-what-you-just-calculated-describe-the-relationship-between-prices-of-textbooks-on-amazon-and-the-ucla-book-store-in-your-answer-you-should-reference-the-context-direction-form-and-strength-your-description-should-inclue-the-slope-and-the-r-squared-values"
    id="toc-15-using-what-you-just-calculated-describe-the-relationship-between-prices-of-textbooks-on-amazon-and-the-ucla-book-store-in-your-answer-you-should-reference-the-context-direction-form-and-strength-your-description-should-inclue-the-slope-and-the-r-squared-values">1.5:
    Using what you just calculated, describe the relationship between prices
    of textbooks on Amazon and the UCLA book store. In your answer, you
    should reference the context, direction, form, and strength. Your
    description should inclue the slope and the R-squared values!</a>
  - <a href="#sources" id="toc-sources">Sources:</a>

# Overview

Now that you’ve built a baseline understanding of how to build least
squares regressions here on Posit, you will apply your new skills to a
new dataset.

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

# The Question you will explore:

### “Are textbooks at UCLA’s bookstore overpriced in relation to the same ones sold on Amazon?”

*Note: This section is modeled after a tutorial developed in
Introduction to Modern Statistics.*

# 1: Build Your Own Scatter Plot and Model

***Everything you do below is something you did on the previous
tutorial. Therefore, copy and paste is your friend!***

## 1.1: Learn about the Data

``` r
?textbooks
```

## 1.2: Build the scatter plot with the linear model included

Before you dive into the coding, you may want to draw a quick sketch of
the plot you want to create so you know which variables go on which
axis. You can do this on paper, your iPad, or the board. Tip: Amazon_new
will be the predictor variable.

``` r
textbooks |>
  ggplot(aes(x = amaz_new, y = ucla_new)) +
  geom_point() +
  geom_smooth(method = "lm" , se = FALSE) +
  labs(
    x = "Price of Book on Amazon (US Dollars)", 
    y = "Price of Book at the UCLA Bookstore (US Dollars)",
    title = "UCLA Bookstore Price vs Amazon Price"
    )
```

    ## `geom_smooth()` using formula = 'y ~ x'

![](2_2_KEY_Build_Your_Own_LSRM_files/figure-gfm/textbook%20viz-1.png)<!-- -->

## 1.3: Generate the equation of the least squares regression line.

``` r
lm(data = textbooks, formula = ucla_new~amaz_new)
```

    ## 
    ## Call:
    ## lm(formula = ucla_new ~ amaz_new, data = textbooks)
    ## 
    ## Coefficients:
    ## (Intercept)     amaz_new  
    ##       0.929        1.199

ucla_new = 0.929 + 1.199\*amazon_new

## 1.4: Generate the correlation coefficient and r-squared

``` r
textbooks %>%
  summarise(
    r = cor(ucla_new, amaz_new)
  ) |>
    mutate(
    r_squared = r^2
  )
```

    ## # A tibble: 1 × 2
    ##       r r_squared
    ##   <dbl>     <dbl>
    ## 1 0.985     0.970

## 1.5: Using what you just calculated, describe the relationship between prices of textbooks on Amazon and the UCLA book store. In your answer, you should reference the context, direction, form, and strength. Your description should inclue the slope and the R-squared values!

UCLA students looking to save money should buy their books on Amazon.
There is a very strong associate between Amazon prices and UCLA
bookstore prices, in fact, roughly 97% of the variation in UCLA book
prices is explained by the Amazon prices. We would expect this becuase
it means that the prices are closely related. However, the slope of our
least squares regression model, 1.199, tells us that for every
additional dollar a book costs on Amazon, we can expect that on average,
the price of a book in the UCLA book store will increase by \$1.20. In
other words, we can say that on average the price of books at the UCLA
book store are 20% higher than the prices of books on Amazon.

## Sources:

<https://openintro-ims.netlify.app/model-slr.html>
<https://openintro.shinyapps.io/ims-03-model-04/#section-data-set-up>
