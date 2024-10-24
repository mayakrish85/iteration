Writing Functions
================
Maya Krishnamoorthy
2024-10-24

Load key packages.

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

## Writing my first function

As an example, here is a z-score computation:

``` r
x_vec = rnorm(n = 25, mean = 10, sd = 3.5)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.26587421 -0.19627733 -0.12403943 -0.02601899  0.28340662 -0.57991465
    ##  [7]  0.18119736 -0.65853286  1.20098088 -0.71681226 -0.82706148  0.76844152
    ## [13]  0.53631063  1.27462407 -0.20996607 -0.23843024 -2.51111964 -1.21391039
    ## [19] -0.07662516 -0.31910713  2.13725387 -1.13569011  0.09438937  1.99627982
    ## [25]  0.09474736

Now I’ll write a function to do this.

``` r
z_scores = function(x) {
  
  z = (x - mean(x)) / sd(x)
  
  return(z)
}

z_scores(x = x_vec)
```

    ##  [1]  0.26587421 -0.19627733 -0.12403943 -0.02601899  0.28340662 -0.57991465
    ##  [7]  0.18119736 -0.65853286  1.20098088 -0.71681226 -0.82706148  0.76844152
    ## [13]  0.53631063  1.27462407 -0.20996607 -0.23843024 -2.51111964 -1.21391039
    ## [19] -0.07662516 -0.31910713  2.13725387 -1.13569011  0.09438937  1.99627982
    ## [25]  0.09474736
