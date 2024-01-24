wk2-workshop
================
Yang Shu Ting (A0238974L)
2024-01-24

- [Read in data](#read-in-data)
- [Statistics on Returns](#statistics-on-returns)
- [S&P Prices](#sp-prices)
- [S&P Yearly Returns](#sp-yearly-returns)

## Read in data

``` r
df <- readRDS("data/wk2_stocks.rds")
str(df)
```

    ## 'data.frame':    5798 obs. of  4 variables:
    ##  $ SPY_prices : num  88.1 87.1 84.3 84.9 84.7 ...
    ##  $ SPY_returns: num  0.04804 -0.01076 -0.03264 0.00774 -0.00264 ...
    ##  $ SPY_vol    : num  88.1 87.1 84.3 84.9 84.7 ...
    ##  $ date       : Date, format: "2001-01-03" "2001-01-04" ...

## Statistics on Returns

- The cumulative returns of the S&P index during this period is 218.33%.
- The average daily returns of the S&P index during this period is
  0.04%.
- The standard deviation of the daily returns of the S&P index during
  this period is 1.22%.

## S&P Prices

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.1.3

    ## Warning: package 'tibble' was built under R version 4.1.3

    ## Warning: package 'tidyr' was built under R version 4.1.3

    ## Warning: package 'readr' was built under R version 4.1.3

    ## Warning: package 'purrr' was built under R version 4.1.3

    ## Warning: package 'dplyr' was built under R version 4.1.3

    ## Warning: package 'forcats' was built under R version 4.1.3

    ## Warning: package 'lubridate' was built under R version 4.1.3

    ## -- Attaching core tidyverse packages ------------------------ tidyverse 2.0.0 --
    ## v dplyr     1.1.2     v readr     2.1.4
    ## v forcats   1.0.0     v stringr   1.5.1
    ## v ggplot2   3.4.4     v tibble    3.2.1
    ## v lubridate 1.9.2     v tidyr     1.3.0
    ## v purrr     1.0.1     
    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()
    ## i Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
ggplot(data = df, aes(x = date, y = SPY_prices)) +
  geom_line()
```

![](wk2-workshop_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

## S&P Yearly Returns

``` r
df %>%
  mutate(year = year(date)) %>%
  filter(year <= 2023) %>%
  group_by(year) %>%
  summarize(yr_return = sum(SPY_returns) * 100) %>%
  ggplot(aes(x = year, y = yr_return)) +
  geom_col()
```

![](wk2-workshop_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
