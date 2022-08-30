writing_functions
================

## Do Something simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.37284580 -0.94179035 -0.47975719 -0.48708966 -2.19538753 -2.19194913
    ##  [7]  2.23638180  0.38497063 -0.91371048 -0.24952267  1.00949348  0.47698135
    ## [13] -0.37659775 -0.73894381  0.31868246  0.26487770  0.19616153  0.73738752
    ## [19]  1.24557391  0.44885695 -0.12674166  0.74611618  1.24524562  0.09733944
    ## [25] -0.94312386  0.99298211  0.65737281 -1.01858216 -1.28436902  0.51629599

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

    ##  [1]  0.37284580 -0.94179035 -0.47975719 -0.48708966 -2.19538753 -2.19194913
    ##  [7]  2.23638180  0.38497063 -0.91371048 -0.24952267  1.00949348  0.47698135
    ## [13] -0.37659775 -0.73894381  0.31868246  0.26487770  0.19616153  0.73738752
    ## [19]  1.24557391  0.44885695 -0.12674166  0.74611618  1.24524562  0.09733944
    ## [25] -0.94312386  0.99298211  0.65737281 -1.01858216 -1.28436902  0.51629599

Try my function on some other things

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
