Iteration and Listcols
================
Maya Krishnamoorthy
2024-10-29

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
set.seed(1)
```

## Lists

``` r
vec_numeric = 5:8
vec_char = c("My", "name", "is", "Jeff")
vec_logical = c(TRUE, TRUE, TRUE, FALSE)

l = list(
  vec_numeric = 5:8,
  mat         = matrix(1:8, 2, 4),
  vec_logical = c(TRUE, FALSE),
  summary     = summary(rnorm(1000)))
l
```

    ## $vec_numeric
    ## [1] 5 6 7 8
    ## 
    ## $mat
    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8
    ## 
    ## $vec_logical
    ## [1]  TRUE FALSE
    ## 
    ## $summary
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -3.00805 -0.69737 -0.03532 -0.01165  0.68843  3.81028

Make a list that’s hopefully more useful.

``` r
list_norm = 
  list(
    a = rnorm(20, 0, 5),
    b = rnorm(20, 4, 5),
    c = rnorm(20, 0, 10),
    d = rnorm(20, 40, 10)
  )

list_norm[["b"]]
```

    ##  [1]  2.36755203  7.87002606  7.92503200  7.81623040  5.47404380 -2.26177962
    ##  [7] -1.04751876  7.75695597 -2.54176756  6.63770049  1.33230213  2.00811993
    ## [13]  0.05215275  2.84929432  8.38592421  6.26866589  2.83767926  8.35002762
    ## [19] 12.28001867  3.96815536

Let’s reuse the function we wrote last time.

``` r
mean_and_sd = function(x) {
  
  mean_x = mean(x)
  sd_x = sd(x)
  
  output_df =
    tibble(
      mean = mean_x,
      sd = sd_x
    )
  
  return(output_df)
}
```

Use the function to take mean and sd of all samples.

``` r
mean_and_sd(list_norm[["a"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -1.50  5.60

``` r
mean_and_sd(list_norm[["b"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.42  4.08

``` r
mean_and_sd(list_norm[["c"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.64  9.53

``` r
mean_and_sd(list_norm[["d"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  35.7  11.8

## Use a for loop

Create output list, and run a for loop.

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  
  output[[i]] = mean_and_sd(list_norm[[i]])
  
}

output
```

    ## [[1]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -1.50  5.60
    ## 
    ## [[2]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.42  4.08
    ## 
    ## [[3]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.64  9.53
    ## 
    ## [[4]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  35.7  11.8
