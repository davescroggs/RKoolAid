
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Tutorial - Mutate & Summarise

From the description

## Mutate

`mutate()` adds new variables and preserves existing ones; transmute()
adds new variables and drops existing ones. New variables overwrite
existing variables of the same name. Variables can be removed by setting
their value to NULL.

The mutate function must return a vector of the same length as the
tibble/dataframe used in the data argument, or for grouped data, the
length of the group. Functions that are called inside mutate can take
column names as an argument which will input the column **as a vector**
(or sections of the vector by group).

``` r
print_and_return <- function(x) {
  print(x)
  return(x)
}

tbl <- tibble(A = 1:4,grp = rep(LETTERS[1:2],each = 2)) %>% 
  mutate(res = print_and_return(A))
#> [1] 1 2 3 4

# Vectors by group
tbl <- tibble(A = 1:4,grp = rep(LETTERS[1:2],each = 2)) %>% 
  group_by(grp) %>% 
  mutate(res = print_and_return(A))
#> [1] 1 2
#> [1] 3 4
```

If a single result is given for a group, it is repeated for the length
of the group.

``` r
tibble(A = rnorm(5)) %>% 
  mutate(B = 1,
         C = mean(A))
#> # A tibble: 5 × 3
#>           A     B      C
#>       <dbl> <dbl>  <dbl>
#> 1  0.0920       1 -0.305
#> 2 -0.647        1 -0.305
#> 3 -0.000905     1 -0.305
#> 4  0.389        1 -0.305
#> 5 -1.36         1 -0.305
```

### Common use cases

#### Calculating percentages of a single row as part of a group

``` r
planes %>% 
  group_by(type,engines) %>% 
  summarise(n = n(),.groups = "drop_last") %>% 
  # last group in group by is dropped
  # This call takes
  mutate(sum_n = sum(n),
         pct = n/sum_n,
         pct_label = scales::percent(pct))
#> # A tibble: 6 × 6
#> # Groups:   type [3]
#>   type                     engines     n sum_n      pct pct_label
#>   <chr>                      <int> <int> <int>    <dbl> <chr>    
#> 1 Fixed wing multi engine        2  3285  3292 0.998    99.787%  
#> 2 Fixed wing multi engine        3     3  3292 0.000911 0.091%   
#> 3 Fixed wing multi engine        4     4  3292 0.00122  0.122%   
#> 4 Fixed wing single engine       1    25    25 1        100%     
#> 5 Rotorcraft                     1     2     5 0.4      40%      
#> 6 Rotorcraft                     2     3     5 0.6      60%
```

## Summarise

`summarise()` creates a new data frame. It will have one (or more) rows
for each combination of grouping variables; if there are no grouping
variables, the output will have a single row summarising all
observations in the input. It will contain one column for each grouping
variable and one column for each of the summary statistics that you have
specified.
