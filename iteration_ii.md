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
    ## -2.52302 -0.73669  0.07907  0.02977  0.77867  2.27683

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
    ##  [1] 2.984829 3.613977 3.032995 1.990296 2.870777 4.109047 2.144766 4.041489
    ##  [9] 2.758034 4.011928 3.856745 2.374943 1.409066 2.093881 4.623968 1.936952
    ## [17] 2.655955 3.889647 3.440780 3.414055
    ## 
    ## $b
    ##  [1]  1.0788640  2.0554058  8.5740221 -1.8918542 -3.5351363 -2.4414445
    ##  [7]  2.1610532 -3.3298433  6.3313745  0.2294827  5.0732314  7.6675057
    ## [13]  1.7013955 -5.2834432 -4.8273636  1.5453549 -1.4204720 -3.8863628
    ## [19] -1.9618173  7.8462513  3.3240728  3.5247784  7.5538084  0.6817095
    ## [25] -4.6888417 -4.6512817 -4.8753628  4.8319489  1.9055227 10.5395195
    ## 
    ## $c
    ##  [1]  9.602422 10.174054  9.938699  9.860933 10.086320  9.756290 10.187751
    ##  [8] 10.063273 10.103422  9.811137 10.117741 10.183936  9.989700 10.138556
    ## [15]  9.995960 10.035012  9.659541  9.888861 10.256105  9.894493 10.186377
    ## [22] 10.171423  9.886210  9.955219 10.108125  9.895714 10.023643 10.459583
    ## [29]  9.771624  9.986810  9.944320  9.889867 10.056668 10.241164  9.822156
    ## [36] 10.085666 10.268364 10.008119  9.943215  9.884308
    ## 
    ## $d
    ##  [1] -2.387306 -3.113068 -1.842483 -1.863563 -4.018971 -3.934680 -4.306670
    ##  [8] -3.407951 -4.031630 -1.221555 -2.885793 -3.945711 -3.908006 -2.316441
    ## [15] -2.661789 -3.095098 -3.076456 -2.863626 -4.632526 -1.464909

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
    ## 1  3.06 0.888

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.13  4.66

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.176

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.05 0.983

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

## List Columns!

``` r
listcol_df =
  tibble(
    name = c("a", "b", "c", "d"),
    samp = list_norm
  )
```

``` r
listcol_df %>% pull(name)
```

    ## [1] "a" "b" "c" "d"

``` r
listcol_df %>% pull(samp)
```

    ## $a
    ##  [1] 2.984829 3.613977 3.032995 1.990296 2.870777 4.109047 2.144766 4.041489
    ##  [9] 2.758034 4.011928 3.856745 2.374943 1.409066 2.093881 4.623968 1.936952
    ## [17] 2.655955 3.889647 3.440780 3.414055
    ## 
    ## $b
    ##  [1]  1.0788640  2.0554058  8.5740221 -1.8918542 -3.5351363 -2.4414445
    ##  [7]  2.1610532 -3.3298433  6.3313745  0.2294827  5.0732314  7.6675057
    ## [13]  1.7013955 -5.2834432 -4.8273636  1.5453549 -1.4204720 -3.8863628
    ## [19] -1.9618173  7.8462513  3.3240728  3.5247784  7.5538084  0.6817095
    ## [25] -4.6888417 -4.6512817 -4.8753628  4.8319489  1.9055227 10.5395195
    ## 
    ## $c
    ##  [1]  9.602422 10.174054  9.938699  9.860933 10.086320  9.756290 10.187751
    ##  [8] 10.063273 10.103422  9.811137 10.117741 10.183936  9.989700 10.138556
    ## [15]  9.995960 10.035012  9.659541  9.888861 10.256105  9.894493 10.186377
    ## [22] 10.171423  9.886210  9.955219 10.108125  9.895714 10.023643 10.459583
    ## [29]  9.771624  9.986810  9.944320  9.889867 10.056668 10.241164  9.822156
    ## [36] 10.085666 10.268364 10.008119  9.943215  9.884308
    ## 
    ## $d
    ##  [1] -2.387306 -3.113068 -1.842483 -1.863563 -4.018971 -3.934680 -4.306670
    ##  [8] -3.407951 -4.031630 -1.221555 -2.885793 -3.945711 -3.908006 -2.316441
    ## [15] -2.661789 -3.095098 -3.076456 -2.863626 -4.632526 -1.464909

``` r
listcol_df %>% 
  filter(name == "a")
```

    ## # A tibble: 1 × 2
    ##   name  samp        
    ##   <chr> <named list>
    ## 1 a     <dbl [20]>

Let’s try some operators

``` r
mean_and_sd(listcol_df$samp[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.06 0.888

map?

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.06 0.888
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.13  4.66
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.176
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.05 0.983

So…can i add a list column?

``` r
listcol_df = listcol_df %>% 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map_dbl(samp, median)
  )
```

## Weather data

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(
    c("USW00094728", "USC00519397", "USS0023B17S"),
    var = c("PRCP", "TMIN", "TMAX"), 
    date_min = "2017-01-01",
    date_max = "2017-12-31") %>%
  mutate(
    name = recode(
      id, 
      USW00094728 = "CentralPark_NY", 
      USC00519397 = "Waikiki_HA",
      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) %>%
  select(name, id, everything())
```

    ## Registered S3 method overwritten by 'hoardr':
    ##   method           from
    ##   print.cache_info httr

    ## using cached file: C:\Users\Admin\AppData\Local/Cache/R/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2022-08-14 19:27:15 (8.408)

    ## file min/max dates: 1869-01-01 / 2022-08-31

    ## using cached file: C:\Users\Admin\AppData\Local/Cache/R/noaa_ghcnd/USC00519397.dly

    ## date created (size, mb): 2022-08-14 19:27:27 (1.701)

    ## file min/max dates: 1965-01-01 / 2020-02-29

    ## using cached file: C:\Users\Admin\AppData\Local/Cache/R/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2022-08-14 19:27:33 (0.95)

    ## file min/max dates: 1999-09-01 / 2022-08-31

Get our list columns

``` r
weather_nest = 
  weather_df %>% 
  nest(data = date:tmin)
```

``` r
weather_nest$name
```

    ## [1] "CentralPark_NY" "Waikiki_HA"     "Waterhole_WA"

``` r
weather_nest$data
```

    ## [[1]]
    ## # A tibble: 365 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0   8.9   4.4
    ##  2 2017-01-02    53   5     2.8
    ##  3 2017-01-03   147   6.1   3.9
    ##  4 2017-01-04     0  11.1   1.1
    ##  5 2017-01-05     0   1.1  -2.7
    ##  6 2017-01-06    13   0.6  -3.8
    ##  7 2017-01-07    81  -3.2  -6.6
    ##  8 2017-01-08     0  -3.8  -8.8
    ##  9 2017-01-09     0  -4.9  -9.9
    ## 10 2017-01-10     0   7.8  -6  
    ## # … with 355 more rows
    ## # ℹ Use `print(n = ...)` to see more rows
    ## 
    ## [[2]]
    ## # A tibble: 365 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0  26.7  16.7
    ##  2 2017-01-02     0  27.2  16.7
    ##  3 2017-01-03     0  27.8  17.2
    ##  4 2017-01-04     0  27.2  16.7
    ##  5 2017-01-05     0  27.8  16.7
    ##  6 2017-01-06     0  27.2  16.7
    ##  7 2017-01-07     0  27.2  16.7
    ##  8 2017-01-08     0  25.6  15  
    ##  9 2017-01-09     0  27.2  15.6
    ## 10 2017-01-10     0  28.3  17.2
    ## # … with 355 more rows
    ## # ℹ Use `print(n = ...)` to see more rows
    ## 
    ## [[3]]
    ## # A tibble: 365 × 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01   432  -6.8 -10.7
    ##  2 2017-01-02    25 -10.5 -12.4
    ##  3 2017-01-03     0  -8.9 -15.9
    ##  4 2017-01-04     0  -9.9 -15.5
    ##  5 2017-01-05     0  -5.9 -14.2
    ##  6 2017-01-06     0  -4.4 -11.3
    ##  7 2017-01-07    51   0.6 -11.5
    ##  8 2017-01-08    76   2.3  -1.2
    ##  9 2017-01-09    51  -1.2  -7  
    ## 10 2017-01-10     0  -5   -14.2
    ## # … with 355 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

Suppose I want to regress ‘tmax’ on ‘tmin’ for each station

this works…

``` r
lm(tmax ~ tmin, data = weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = weather_nest$data[[1]])
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

Let’s write a function

``` r
weather_lm = function(df) {
  
  lm(tmax ~ tmin, data = df)
  
}

output = vector("list", 3)

for (i in 1:3) {
  
  output[[i]] = weather_nest$data[[i]]

  }
```

What about a map …!?

``` r
map(weather_nest$data, weather_lm)
```

    ## [[1]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039  
    ## 
    ## 
    ## [[2]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##     20.0966       0.4509  
    ## 
    ## 
    ## [[3]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.499        1.221

What about a map in a list column

``` r
weather_nest = weather_nest %>% 
  mutate(models = map(data, weather_lm)
  )
```
