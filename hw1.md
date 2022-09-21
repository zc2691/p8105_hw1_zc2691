8105 HW1
================

This is an R markdown document for HW1

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.0      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.2      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

# Problem 1

``` r
data("penguins", package = "palmerpenguins")
```

Here is a summary of the *penguins* dataset.

|                                                  |          |
|:-------------------------------------------------|:---------|
| Name                                             | penguins |
| Number of rows                                   | 344      |
| Number of columns                                | 8        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |          |
| Column type frequency:                           |          |
| factor                                           | 3        |
| numeric                                          | 5        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |          |
| Group variables                                  | None     |

Data summary

**Variable type: factor**

| skim_variable | n_missing | complete_rate | ordered | n_unique | top_counts                  |
|:--------------|----------:|--------------:|:--------|---------:|:----------------------------|
| species       |         0 |          1.00 | FALSE   |        3 | Ade: 152, Gen: 124, Chi: 68 |
| island        |         0 |          1.00 | FALSE   |        3 | Bis: 168, Dre: 124, Tor: 52 |
| sex           |        11 |          0.97 | FALSE   |        2 | mal: 168, fem: 165          |

**Variable type: numeric**

| skim_variable     | n_missing | complete_rate |    mean |     sd |     p0 |     p25 |     p50 |    p75 |   p100 | hist  |
|:------------------|----------:|--------------:|--------:|-------:|-------:|--------:|--------:|-------:|-------:|:------|
| bill_length_mm    |         2 |          0.99 |   43.92 |   5.46 |   32.1 |   39.23 |   44.45 |   48.5 |   59.6 | ▃▇▇▆▁ |
| bill_depth_mm     |         2 |          0.99 |   17.15 |   1.97 |   13.1 |   15.60 |   17.30 |   18.7 |   21.5 | ▅▅▇▇▂ |
| flipper_length_mm |         2 |          0.99 |  200.92 |  14.06 |  172.0 |  190.00 |  197.00 |  213.0 |  231.0 | ▂▇▃▅▂ |
| body_mass_g       |         2 |          0.99 | 4201.75 | 801.95 | 2700.0 | 3550.00 | 4050.00 | 4750.0 | 6300.0 | ▃▇▆▃▂ |
| year              |         0 |          1.00 | 2008.03 |   0.82 | 2007.0 | 2007.00 | 2008.00 | 2009.0 | 2009.0 | ▇▁▇▁▇ |

*penguins* is a **dataset** that includes variables of `species`,
`island`, `bill_length_mm`, `bill_depth_mm`, `flipper_length_mm`,
`body_mass_h`, `sex`, and `year`. `Species` includes
“Adelie”,“Chinstrap”, and “Gentoo”. `Island` includes “Torgersen”,
“Biscoe”, and “Dream”. The `year` ranges from 2007 to 2009.

Here’s a **code chunk** that calculate the size of the dataset.

``` r
nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8

The dataset has 344 rows and 8 columns.

``` r
max(penguins$bill_length_mm, na.rm = TRUE)
```

    ## [1] 59.6

``` r
min(penguins$bill_length_mm, na.rm = TRUE)
```

    ## [1] 32.1

``` r
mean(penguins$bill_length_mm, na.rm = TRUE)
```

    ## [1] 43.92193

The max value of `bill_length_mm` is 59.6mm and the min is 32.1mm. The
mean of `bill_length_mm` is 43.92193mm.

``` r
max(penguins$flipper_length_mm, na.rm = TRUE)
```

    ## [1] 231

``` r
min(penguins$flipper_length_mm, na.rm = TRUE)
```

    ## [1] 172

``` r
mean(penguins$flipper_length_mm, na.rm = TRUE)
```

    ## [1] 200.9152

The max value of `flipper_length_mm` is 231mm and the min is 172mm.The
mean of `flipper_length_mm` is 200.9152mm.

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
```

![](hw1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Problem 2

``` r
hw_df = 
  tibble(
    norm_sample = rnorm(10),
    vec_logical = norm_sample > 0,
    vec_char = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j"),
    vec_factor = factor(c("low", "medium", "high", "low", "medium", "high", "low", "medium", "high", "low"))
  )
```

Here’s a **code chunk** to calculate the mean of each variable in my
dataframe.

``` r
hw_df %>% pull(norm_sample)
```

    ##  [1] -0.58360150 -0.55415490 -0.86318242  1.58697690  1.21128186  1.81498873
    ##  [7]  0.69778163 -0.09606424 -0.34930971 -0.31291366

``` r
mean(hw_df$norm_sample)
```

    ## [1] 0.2551803

``` r
hw_df %>% pull(vec_logical)
```

    ##  [1] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE

``` r
mean(hw_df$vec_logical)
```

    ## [1] 0.4

``` r
hw_df %>% pull(vec_char)
```

    ##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j"

``` r
mean(hw_df$vec_char)
```

    ## Warning in mean.default(hw_df$vec_char): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
hw_df %>% pull(vec_factor)
```

    ##  [1] low    medium high   low    medium high   low    medium high   low   
    ## Levels: high low medium

``` r
mean(hw_df$vec_factor)
```

    ## Warning in mean.default(hw_df$vec_factor): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

The mean calculation works for random samples and logical vector but
doesn’t work for character vector and factor vector.

Here I used the `as.numeric` function to explicitly convert logical,
character, and factor variables from to numeric vectors.

``` r
as.numeric(hw_df$vec_logical)
as.numeric(hw_df$vec_char)
as.numeric(hw_df$vec_factor)
```

Logical vector is successfully converted to numeric variable by
converting `TRUE` to a numeric value of 1 and `FALSE` to 0. Therefore, I
could calculate the mean of the logical vector.

Character vector cannot be converted to a numeric variable and the
output is NA for all. Therefore, I could not calculate the mean of the
character vector.

Factor vector is converted to levels with “high” corresponding to 1,
“low” corresponding to 2, and “medium” corresponding to 3. But this is
not numerical value and the mean cannot be calculated.

In summary, the mean calculation only works for numeric and logical
vectors.
