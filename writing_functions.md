writing_functions
================

## Do Something simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -0.61647391  1.35062593 -0.08516710 -0.08610002  0.79917614 -0.51043248
    ##  [7]  1.64412893  0.63307563 -0.48826672 -2.53197709 -0.22739686  0.95297763
    ## [13]  0.42258690 -0.46318495 -0.12664072  0.76891723  0.41471454 -0.70097834
    ## [19]  1.89948127 -1.80795881  1.05775600  0.32973729 -0.56520271 -0.53889433
    ## [25]  0.94528515 -0.96009747  0.77441991 -1.02301581 -1.14726652 -0.11382871

I want a function to compute z-scores

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3) {
    stop("Input must be numeric")
  }
  
  z = (x - mean(x)) / sd(x)
  
  return(z)
}

z_scores(x_vec)
```

    ##  [1] -0.61647391  1.35062593 -0.08516710 -0.08610002  0.79917614 -0.51043248
    ##  [7]  1.64412893  0.63307563 -0.48826672 -2.53197709 -0.22739686  0.95297763
    ## [13]  0.42258690 -0.46318495 -0.12664072  0.76891723  0.41471454 -0.70097834
    ## [19]  1.89948127 -1.80795881  1.05775600  0.32973729 -0.56520271 -0.53889433
    ## [25]  0.94528515 -0.96009747  0.77441991 -1.02301581 -1.14726652 -0.11382871

Try my function on some other things: should give errors

``` r
z_scores(3)
```

    ## Error in z_scores(3): Input must be numeric

``` r
z_scores("my name is jeff")
```

    ## Error in z_scores("my name is jeff"): Input must be numeric

``` r
z_scores(mtcars)
```

    ## Error in z_scores(mtcars): Input must be numeric

``` r
z_scores(c(TRUE, TRUE, FALSE, FALSE))
```

    ## Error in z_scores(c(TRUE, TRUE, FALSE, FALSE)): Input must be numeric

## Multiple outputs

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3) {
    stop("Input must be numeric")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)
  
  tibble(
    mean = mean_x,
    sd = sd_x
  )
  
}
```

Check that the function works

``` r
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.42  3.50

## Multiple inputs

``` r
sim_data =
  tibble(
    x = rnorm(100, mean = 4, sd = 3)
  )

sim_data %>% 
  summarize(
    mean = mean(x),
    sd = sd(x)
  )
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.10  2.67

``` r
sim_mean_sd = function(sample_size, mu = 6, sigma = 4) {
  
  sim_data =
  tibble(
    x = rnorm(n = sample_size, mean = mu, sd = sigma)
  )

sim_data %>% 
  summarize(
    mean = mean(x),
    sd = sd(x)
  )
}
```

``` r
sim_mean_sd(100,6,3)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.03  3.16

``` r
sim_mean_sd(sample_size = 10, mu = 6, sigma = 3)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.72  4.93
