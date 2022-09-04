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
    ##       Min.    1st Qu.     Median       Mean    3rd Qu.       Max. 
    ## -2.1109520 -0.6047945 -0.0002903 -0.0012326  0.5440438  2.0135934

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
    ##  [1] 2.0615900 3.3689449 2.7486009 3.1693329 5.0061944 4.1299267 3.6547479
    ##  [8] 4.0944732 0.7239235 2.8750892 2.2962828 3.5606287 3.8119997 4.8468486
    ## [15] 2.9837150 3.9879213 1.9204788 2.0239148 3.3567112 4.8591200
    ## 
    ## $b
    ##  [1] -11.04476337  -2.80086160   1.96123136   5.83415381  -2.79039067
    ##  [6]  -2.20298483   4.73051638  -4.17819697  -1.32200202  -4.95073788
    ## [11]   1.09889928  -4.08893384   5.47567210   7.62101751  -7.55978150
    ## [16]  -5.66213266   6.72892652   4.99503060   1.31314740  -5.20102890
    ## [21]   7.63980225   0.94092846  -0.66041385  -0.37400977  -2.49368556
    ## [26]   2.07677827   0.36825241  -0.03503148  -2.29280783  -3.70735501
    ## 
    ## $c
    ##  [1]  9.977312  9.806155  9.937467 10.025173 10.170302  9.900482 10.038441
    ##  [8]  9.684292 10.204681  9.922980  9.796636  9.917075 10.442318 10.058187
    ## [15] 10.209720  9.811093 10.058121  9.727894  9.874650 10.014316  9.378097
    ## [22] 10.134869  9.886317  9.886765 10.347415  9.786004  9.721615  9.780836
    ## [29]  9.700595  9.895811 10.295755 10.001207 10.077113  9.374076  9.802946
    ## [36]  9.996832 10.221523  9.687821  9.950229 10.253108
    ## 
    ## $d
    ##  [1] -2.383422 -3.133240 -3.148976 -3.371638 -3.204928 -4.305405 -3.240847
    ##  [8] -3.088990 -3.385083 -2.821455 -2.016476 -2.545783 -2.928503 -3.955306
    ## [15] -3.386444 -2.265176 -3.389506 -3.206604 -1.740048 -2.465615

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
    ## 1  3.27  1.11

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.353  4.65

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.94 0.231

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.00 0.624

Let’s use a for loop

``` r
output = vector("list", length = 4)

for (i in 1:4) {

output[[i]] = mean_and_sd(list_norm[[i]])

}
```