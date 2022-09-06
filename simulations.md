simulations
================

## Let’s simulate something

``` r
sim_mean_sd = function(samp_size, mu = 3, sigma = 4) {
  
  sim_data = 
    tibble(
      x = rnorm(n = samp_size, mean = mu, sd = sigma)
    )

sim_data %>% 
  summarize(
    mean = mean(x),
    sd = sd(x)
  )

  }
```

``` r
sim_mean_sd(30)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.89  4.54

## Let’s simulate a lot

lets start with a for loop

``` r
output = vector("list", length = 100)

for (i in 1:100) {
  
  output[[i]] = sim_mean_sd(samp_size = 30)
}

bind_rows(output)
```

    ## # A tibble: 100 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ##  1  2.94  3.09
    ##  2  4.27  3.65
    ##  3  4.35  4.32
    ##  4  2.49  4.64
    ##  5  2.73  3.46
    ##  6  1.57  3.71
    ##  7  1.95  4.25
    ##  8  2.88  3.74
    ##  9  3.29  4.58
    ## 10  3.14  4.58
    ## # … with 90 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

Let’s use a loop function

``` r
sim_results =
rerun(100, sim_mean_sd(samp_size = 30)) %>% 
  bind_rows()
```

Let’s look at results..

``` r
sim_results %>% 
  ggplot(aes(x = mean)) + geom_density() 
```

<img src="simulations_files/figure-gfm/unnamed-chunk-5-1.png" width="90%" />

``` r
sim_results %>% 
  summarize(
    avg_samp_mean = mean(mean),
    sd_samp_mean = sd(mean)
  )
```

    ## # A tibble: 1 × 2
    ##   avg_samp_mean sd_samp_mean
    ##           <dbl>        <dbl>
    ## 1          3.15        0.756

``` r
sim_results %>% 
  ggplot(aes(x = sd)) + geom_density() 
```

<img src="simulations_files/figure-gfm/unnamed-chunk-5-2.png" width="90%" />
