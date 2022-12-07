mapping
================
Qiaoyi Xu
2022-12-06

``` r
library(tidyverse)
```

``` r
legal_state = read_csv("data/legalization_state.csv") 
```

    ## Rows: 51 Columns: 5
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (3): State, Recreational, Medical
    ## dbl (2): Year_legalized_REC, Year_legalized_MED
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
legal_state = legal_state %>% 
  mutate(status = case_when(
    Recreational == "Yes" | Medical == "Yes" ~ "Full legal",
    Recreational == "No" | Medical == "Yes" ~ "Med legal",
    Recreational == "No" | Medical == "No" ~ "Unlegal"
  ))

legal_state
```

    ## # A tibble: 51 × 6
    ##    State      Recreational Year_legalized_REC Medical Year_legalized_MED status 
    ##    <chr>      <chr>                     <dbl> <chr>                <dbl> <chr>  
    ##  1 California Yes                        2016 Yes                   1996 Full l…
    ##  2 Alaska     Yes                        2014 Yes                   1998 Full l…
    ##  3 Nevada     Yes                        2016 Yes                   1998 Full l…
    ##  4 Oregon     Yes                        2014 Yes                   1998 Full l…
    ##  5 Washington Yes                        2012 Yes                   1998 Full l…
    ##  6 Maine      Yes                        2016 Yes                   1999 Full l…
    ##  7 Colorado   Yes                        2012 Yes                   2000 Full l…
    ##  8 Hawaii     No                           NA Yes                   2000 Full l…
    ##  9 Montana    Yes                        2020 Yes                   2004 Full l…
    ## 10 Vermont    Yes                        2020 Yes                   2004 Full l…
    ## # … with 41 more rows
