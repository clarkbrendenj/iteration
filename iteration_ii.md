iteration_ii
================

## Lists

You can put anything in a list

``` r
l = list(
  vec_numeric = 5:8,
  vec_logical = c(TRUE, TRUE, FALSE, TRUE, FALSE, FALSE),
  mat = matrix(1:8, nrow = 2, ncol = 4),
  summary = summary(rnorm(100))
)
```

``` r
l
```

    ## $vec_numeric
    ## [1] 5 6 7 8
    ## 
    ## $vec_logical
    ## [1]  TRUE  TRUE FALSE  TRUE FALSE FALSE
    ## 
    ## $mat
    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8
    ## 
    ## $summary
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -2.57562 -0.65928 -0.04031  0.02447  0.56923  2.93216

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[1]]
```

    ## [1] 5 6 7 8

``` r
l[["vec_numeric"]]
```

    ## [1] 5 6 7 8

## for loop

Create a new list

``` r
list_norm = list(
  a = rnorm(20, mean = 3, sd = 1),
  b = rnorm(30, mean = 0, sd = 5),
  c = rnorm(40, mean = 10, sd = .2),
  d = rnorm(20, mean = -3, sd = 1)
  
)
```

``` r
list_norm
```

    ## $a
    ##  [1] 3.1554344 1.5283642 4.1743103 4.5053614 2.6705105 2.1523966 3.1127326
    ##  [8] 1.8029446 0.9813882 3.2451820 2.8014224 2.5778043 2.2170603 2.7536186
    ## [15] 2.5846735 2.2816697 1.3301537 3.6151023 4.6234846 1.4001015
    ## 
    ## $b
    ##  [1]  3.4226511  6.7873382 -6.6634402 -3.4174006  3.3881003  2.1841381
    ##  [7] -1.1693329  0.2887030  0.5339892 -4.4932133 -7.0413304 -3.3623824
    ## [13] -0.3785242  5.4015054 -4.8588747  1.1335123  3.4108829  1.0834099
    ## [19] -5.5291179 -4.7867071  3.6142444 -1.3010006 -5.5080854 -0.2097301
    ## [25] -7.2270379  2.5686054 -2.2208917 -2.2822976  2.1339644 -9.9954982
    ## 
    ## $c
    ##  [1]  9.874019 10.230978  9.757877 10.166123 10.506627 10.148405  9.842234
    ##  [8]  9.962728  9.962820 10.195072 10.030888  9.799356 10.216569  9.798025
    ## [15]  9.958085 10.190071  9.718639 10.132779 10.272442  9.582387  9.683388
    ## [22]  9.744847  9.926330 10.189989  9.982773 10.050812  9.876437  9.667857
    ## [29]  9.980203  9.949951 10.029270  9.998537 10.014377 10.269852  9.936177
    ## [36]  9.834015 10.202975  9.768428  9.794454 10.456380
    ## 
    ## $d
    ##  [1] -2.939705 -4.271903 -2.322543 -3.080663 -1.995061 -2.944664 -2.128413
    ##  [8] -3.643756 -1.749330 -2.977587 -2.889167 -1.833293 -3.272886 -4.371421
    ## [15] -4.269977 -1.899626 -4.385058 -2.904165 -2.603244 -4.097149

Pause and get my old function

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

i can apply that function to each list element

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.68  1.03

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -1.15  4.20

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.99 0.215

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.03 0.896

Let’s use a for loop

``` r
output = vector("list", length = 4)

for (i in 1:4) {

output[[i]] = mean_and_sd(list_norm[[i]])

}
```

Lets try map

``` r
output = map(list_norm, mean_and_sd)
```

what if you want a different fuinction?

``` r
output = map(list_norm, IQR)
```
