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
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -3.1163 -0.5666  0.1853  0.1126  0.7192  2.5586

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
    ##  [1] 3.296269 2.946937 2.964883 1.659567 3.877188 4.693512 4.307334 4.130224
    ##  [9] 1.331466 4.212569 2.438439 2.178827 2.355165 4.350509 2.644103 2.583075
    ## [17] 2.509414 4.824933 1.894165 4.040433
    ## 
    ## $b
    ##  [1]   3.6834553  -4.2142992   1.7262493   0.5536742  -0.2437009  -8.4363521
    ##  [7]   4.7609760  -1.5999235   7.4632689 -14.0463448   0.7117672  -3.1889019
    ## [13]   5.8509197  -1.0368978   1.8985578   1.5297883  -7.5885249  -1.7647393
    ## [19]   2.1748404  -3.8210113   5.5489964   2.9834175  -2.0764271   2.3783632
    ## [25]   2.5808641   2.3765600  -0.6679996   4.2987118   4.7543450   6.3038965
    ## 
    ## $c
    ##  [1]  9.905960 10.242368 10.274055 10.089116  9.800572 10.493707  9.995904
    ##  [8]  9.730869  9.952847 10.198706 10.008627 10.518817  9.520212 10.352880
    ## [15]  9.650814 10.333120 10.346487 10.140242  9.845645 10.094436  9.833479
    ## [22]  9.903431  9.976242  9.436123  9.707072 10.253623  9.982498 10.472401
    ## [29]  9.906666 10.497802  9.809826  9.944199 10.277418 10.354950 10.087980
    ## [36] 10.391938  9.989708 10.105717  9.917393  9.981594
    ## 
    ## $d
    ##  [1] -4.480002 -2.882927 -3.423372 -2.468424 -2.764419 -3.836816 -3.632506
    ##  [8] -2.797265 -3.003118 -2.281116 -4.082603 -4.105036 -2.850307 -2.720500
    ## [15] -3.219991 -1.998749 -3.697414 -3.093486 -2.971074 -2.044714

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
    ## 1  3.16  1.07

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.430  4.75

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.1 0.270

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.12 0.690

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
output = map(list_norm, median)
```

``` r
output = map_dbl(list_norm, median)
```

``` r
output = map_df(list_norm, mean_and_sd, .id = "input")
```
