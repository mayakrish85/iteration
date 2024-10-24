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

    ##  [1]  0.597651238  0.632443229  0.325895576 -0.742289666  0.577308982
    ##  [6] -0.091927558 -1.825880477 -1.757669903  0.498215707  1.680227450
    ## [11] -1.672990104 -0.063207973 -0.090969863 -0.233855868 -1.214466889
    ## [16] -0.803207623 -0.891147798  1.829120563 -0.363000994  0.288738220
    ## [21]  0.001129458  1.126695704  1.136887965  0.148330288  0.907970335

Now I’ll write a function to do this.

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("x needs to be numeric")
  }
  
  if (length(x) < 5) {
    stop("you need at least 5 numbers to compute the z score")
  }
  
  z = (x - mean(x)) / sd(x)
  
  return(z)
}

z_scores(x = x_vec)
```

    ##  [1]  0.597651238  0.632443229  0.325895576 -0.742289666  0.577308982
    ##  [6] -0.091927558 -1.825880477 -1.757669903  0.498215707  1.680227450
    ## [11] -1.672990104 -0.063207973 -0.090969863 -0.233855868 -1.214466889
    ## [16] -0.803207623 -0.891147798  1.829120563 -0.363000994  0.288738220
    ## [21]  0.001129458  1.126695704  1.136887965  0.148330288  0.907970335

Does this always work?

``` r
z_scores(x = 3) # can't get SD of one number
```

    ## Error in z_scores(x = 3): you need at least 5 numbers to compute the z score

``` r
z_scores(x = c("my", "name", "is", "maya")) # not numeric vector
```

    ## Error in z_scores(x = c("my", "name", "is", "maya")): x needs to be numeric
