
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Tidyverse workhorse functions

## The functions you will use all the time

-   %\>%

-   select

-   filter

-   group_by

-   mutate

-   summarise

-   head/tail/slice

-   arrange

-   tibble

## Pipes - %\>%

Pipes an object forward into a function or call expression. By defauly,
pipes take the result of the left hand side expression and puts it in
the first argument of the following function/call, without having to
specify the argument. It allows you to string together functions
step-by-step, without saving the intermediate steps to variables.
Tidyverse functions typically set their first argument as the *data*
argument, ww . The short-cut for entering a pipe in RStudio is cntrl +
shift + M.

``` r
select(mtcars,vs)
#>                     vs
#> Mazda RX4            0
#> Mazda RX4 Wag        0
#> Datsun 710           1
#> Hornet 4 Drive       1
#> Hornet Sportabout    0
#> Valiant              1
#> Duster 360           0
#> Merc 240D            1
#> Merc 230             1
#> Merc 280             1
#> Merc 280C            1
#> Merc 450SE           0
#> Merc 450SL           0
#> Merc 450SLC          0
#> Cadillac Fleetwood   0
#> Lincoln Continental  0
#> Chrysler Imperial    0
#> Fiat 128             1
#> Honda Civic          1
#> Toyota Corolla       1
#> Toyota Corona        1
#> Dodge Challenger     0
#> AMC Javelin          0
#> Camaro Z28           0
#> Pontiac Firebird     0
#> Fiat X1-9            1
#> Porsche 914-2        0
#> Lotus Europa         1
#> Ford Pantera L       0
#> Ferrari Dino         0
#> Maserati Bora        0
#> Volvo 142E           1

mtcars %>% 
  select(vs)
#>                     vs
#> Mazda RX4            0
#> Mazda RX4 Wag        0
#> Datsun 710           1
#> Hornet 4 Drive       1
#> Hornet Sportabout    0
#> Valiant              1
#> Duster 360           0
#> Merc 240D            1
#> Merc 230             1
#> Merc 280             1
#> Merc 280C            1
#> Merc 450SE           0
#> Merc 450SL           0
#> Merc 450SLC          0
#> Cadillac Fleetwood   0
#> Lincoln Continental  0
#> Chrysler Imperial    0
#> Fiat 128             1
#> Honda Civic          1
#> Toyota Corolla       1
#> Toyota Corona        1
#> Dodge Challenger     0
#> AMC Javelin          0
#> Camaro Z28           0
#> Pontiac Firebird     0
#> Fiat X1-9            1
#> Porsche 914-2        0
#> Lotus Europa         1
#> Ford Pantera L       0
#> Ferrari Dino         0
#> Maserati Bora        0
#> Volvo 142E           1

mtcars %>% 
  rownames_to_column(var = "carName") %>% 
  mutate(make = str_extract(carName,"\\w+")) %>% 
  group_by(make) %>% 
  summarise(mpg = mean(mpg)) %>% 
  arrange(-mpg) %>% 
  head(10)
#> # A tibble: 10 × 2
#>    make      mpg
#>    <chr>   <dbl>
#>  1 Honda    30.4
#>  2 Lotus    30.4
#>  3 Fiat     29.8
#>  4 Toyota   27.7
#>  5 Porsche  26  
#>  6 Datsun   22.8
#>  7 Volvo    21.4
#>  8 Mazda    21  
#>  9 Hornet   20.0
#> 10 Ferrari  19.7


mtcars %>% {select(.,vs)}
#>                     vs
#> Mazda RX4            0
#> Mazda RX4 Wag        0
#> Datsun 710           1
#> Hornet 4 Drive       1
#> Hornet Sportabout    0
#> Valiant              1
#> Duster 360           0
#> Merc 240D            1
#> Merc 230             1
#> Merc 280             1
#> Merc 280C            1
#> Merc 450SE           0
#> Merc 450SL           0
#> Merc 450SLC          0
#> Cadillac Fleetwood   0
#> Lincoln Continental  0
#> Chrysler Imperial    0
#> Fiat 128             1
#> Honda Civic          1
#> Toyota Corolla       1
#> Toyota Corona        1
#> Dodge Challenger     0
#> AMC Javelin          0
#> Camaro Z28           0
#> Pontiac Firebird     0
#> Fiat X1-9            1
#> Porsche 914-2        0
#> Lotus Europa         1
#> Ford Pantera L       0
#> Ferrari Dino         0
#> Maserati Bora        0
#> Volvo 142E           1
```

## select

``` r
# Reference by individual name
mtcars %>% 
  select(mpg,cyl)
#>                      mpg cyl
#> Mazda RX4           21.0   6
#> Mazda RX4 Wag       21.0   6
#> Datsun 710          22.8   4
#> Hornet 4 Drive      21.4   6
#> Hornet Sportabout   18.7   8
#> Valiant             18.1   6
#> Duster 360          14.3   8
#> Merc 240D           24.4   4
#> Merc 230            22.8   4
#> Merc 280            19.2   6
#> Merc 280C           17.8   6
#> Merc 450SE          16.4   8
#> Merc 450SL          17.3   8
#> Merc 450SLC         15.2   8
#> Cadillac Fleetwood  10.4   8
#> Lincoln Continental 10.4   8
#> Chrysler Imperial   14.7   8
#> Fiat 128            32.4   4
#> Honda Civic         30.4   4
#> Toyota Corolla      33.9   4
#> Toyota Corona       21.5   4
#> Dodge Challenger    15.5   8
#> AMC Javelin         15.2   8
#> Camaro Z28          13.3   8
#> Pontiac Firebird    19.2   8
#> Fiat X1-9           27.3   4
#> Porsche 914-2       26.0   4
#> Lotus Europa        30.4   4
#> Ford Pantera L      15.8   8
#> Ferrari Dino        19.7   6
#> Maserati Bora       15.0   8
#> Volvo 142E          21.4   4

# Refernce by index
mtcars %>% 
  select(1,2)
#>                      mpg cyl
#> Mazda RX4           21.0   6
#> Mazda RX4 Wag       21.0   6
#> Datsun 710          22.8   4
#> Hornet 4 Drive      21.4   6
#> Hornet Sportabout   18.7   8
#> Valiant             18.1   6
#> Duster 360          14.3   8
#> Merc 240D           24.4   4
#> Merc 230            22.8   4
#> Merc 280            19.2   6
#> Merc 280C           17.8   6
#> Merc 450SE          16.4   8
#> Merc 450SL          17.3   8
#> Merc 450SLC         15.2   8
#> Cadillac Fleetwood  10.4   8
#> Lincoln Continental 10.4   8
#> Chrysler Imperial   14.7   8
#> Fiat 128            32.4   4
#> Honda Civic         30.4   4
#> Toyota Corolla      33.9   4
#> Toyota Corona       21.5   4
#> Dodge Challenger    15.5   8
#> AMC Javelin         15.2   8
#> Camaro Z28          13.3   8
#> Pontiac Firebird    19.2   8
#> Fiat X1-9           27.3   4
#> Porsche 914-2       26.0   4
#> Lotus Europa        30.4   4
#> Ford Pantera L      15.8   8
#> Ferrari Dino        19.7   6
#> Maserati Bora       15.0   8
#> Volvo 142E          21.4   4

# Select a range
mtcars %>% 
  select(mpg:hp,6:8)
#>                      mpg cyl  disp  hp    wt  qsec vs
#> Mazda RX4           21.0   6 160.0 110 2.620 16.46  0
#> Mazda RX4 Wag       21.0   6 160.0 110 2.875 17.02  0
#> Datsun 710          22.8   4 108.0  93 2.320 18.61  1
#> Hornet 4 Drive      21.4   6 258.0 110 3.215 19.44  1
#> Hornet Sportabout   18.7   8 360.0 175 3.440 17.02  0
#> Valiant             18.1   6 225.0 105 3.460 20.22  1
#> Duster 360          14.3   8 360.0 245 3.570 15.84  0
#> Merc 240D           24.4   4 146.7  62 3.190 20.00  1
#> Merc 230            22.8   4 140.8  95 3.150 22.90  1
#> Merc 280            19.2   6 167.6 123 3.440 18.30  1
#> Merc 280C           17.8   6 167.6 123 3.440 18.90  1
#> Merc 450SE          16.4   8 275.8 180 4.070 17.40  0
#> Merc 450SL          17.3   8 275.8 180 3.730 17.60  0
#> Merc 450SLC         15.2   8 275.8 180 3.780 18.00  0
#> Cadillac Fleetwood  10.4   8 472.0 205 5.250 17.98  0
#> Lincoln Continental 10.4   8 460.0 215 5.424 17.82  0
#> Chrysler Imperial   14.7   8 440.0 230 5.345 17.42  0
#> Fiat 128            32.4   4  78.7  66 2.200 19.47  1
#> Honda Civic         30.4   4  75.7  52 1.615 18.52  1
#> Toyota Corolla      33.9   4  71.1  65 1.835 19.90  1
#> Toyota Corona       21.5   4 120.1  97 2.465 20.01  1
#> Dodge Challenger    15.5   8 318.0 150 3.520 16.87  0
#> AMC Javelin         15.2   8 304.0 150 3.435 17.30  0
#> Camaro Z28          13.3   8 350.0 245 3.840 15.41  0
#> Pontiac Firebird    19.2   8 400.0 175 3.845 17.05  0
#> Fiat X1-9           27.3   4  79.0  66 1.935 18.90  1
#> Porsche 914-2       26.0   4 120.3  91 2.140 16.70  0
#> Lotus Europa        30.4   4  95.1 113 1.513 16.90  1
#> Ford Pantera L      15.8   8 351.0 264 3.170 14.50  0
#> Ferrari Dino        19.7   6 145.0 175 2.770 15.50  0
#> Maserati Bora       15.0   8 301.0 335 3.570 14.60  0
#> Volvo 142E          21.4   4 121.0 109 2.780 18.60  1

# Deselect
mtcars %>% 
  select(-c(mpg,hp))
#>                     cyl  disp drat    wt  qsec vs am gear carb
#> Mazda RX4             6 160.0 3.90 2.620 16.46  0  1    4    4
#> Mazda RX4 Wag         6 160.0 3.90 2.875 17.02  0  1    4    4
#> Datsun 710            4 108.0 3.85 2.320 18.61  1  1    4    1
#> Hornet 4 Drive        6 258.0 3.08 3.215 19.44  1  0    3    1
#> Hornet Sportabout     8 360.0 3.15 3.440 17.02  0  0    3    2
#> Valiant               6 225.0 2.76 3.460 20.22  1  0    3    1
#> Duster 360            8 360.0 3.21 3.570 15.84  0  0    3    4
#> Merc 240D             4 146.7 3.69 3.190 20.00  1  0    4    2
#> Merc 230              4 140.8 3.92 3.150 22.90  1  0    4    2
#> Merc 280              6 167.6 3.92 3.440 18.30  1  0    4    4
#> Merc 280C             6 167.6 3.92 3.440 18.90  1  0    4    4
#> Merc 450SE            8 275.8 3.07 4.070 17.40  0  0    3    3
#> Merc 450SL            8 275.8 3.07 3.730 17.60  0  0    3    3
#> Merc 450SLC           8 275.8 3.07 3.780 18.00  0  0    3    3
#> Cadillac Fleetwood    8 472.0 2.93 5.250 17.98  0  0    3    4
#> Lincoln Continental   8 460.0 3.00 5.424 17.82  0  0    3    4
#> Chrysler Imperial     8 440.0 3.23 5.345 17.42  0  0    3    4
#> Fiat 128              4  78.7 4.08 2.200 19.47  1  1    4    1
#> Honda Civic           4  75.7 4.93 1.615 18.52  1  1    4    2
#> Toyota Corolla        4  71.1 4.22 1.835 19.90  1  1    4    1
#> Toyota Corona         4 120.1 3.70 2.465 20.01  1  0    3    1
#> Dodge Challenger      8 318.0 2.76 3.520 16.87  0  0    3    2
#> AMC Javelin           8 304.0 3.15 3.435 17.30  0  0    3    2
#> Camaro Z28            8 350.0 3.73 3.840 15.41  0  0    3    4
#> Pontiac Firebird      8 400.0 3.08 3.845 17.05  0  0    3    2
#> Fiat X1-9             4  79.0 4.08 1.935 18.90  1  1    4    1
#> Porsche 914-2         4 120.3 4.43 2.140 16.70  0  1    5    2
#> Lotus Europa          4  95.1 3.77 1.513 16.90  1  1    5    2
#> Ford Pantera L        8 351.0 4.22 3.170 14.50  0  1    5    4
#> Ferrari Dino          6 145.0 3.62 2.770 15.50  0  1    5    6
#> Maserati Bora         8 301.0 3.54 3.570 14.60  0  1    5    8
#> Volvo 142E            4 121.0 4.11 2.780 18.60  1  1    4    2

# Select by string - all
col_names_all <- c("mpg","cyl")
mtcars %>% 
  select(all_of(col_names_all))
#>                      mpg cyl
#> Mazda RX4           21.0   6
#> Mazda RX4 Wag       21.0   6
#> Datsun 710          22.8   4
#> Hornet 4 Drive      21.4   6
#> Hornet Sportabout   18.7   8
#> Valiant             18.1   6
#> Duster 360          14.3   8
#> Merc 240D           24.4   4
#> Merc 230            22.8   4
#> Merc 280            19.2   6
#> Merc 280C           17.8   6
#> Merc 450SE          16.4   8
#> Merc 450SL          17.3   8
#> Merc 450SLC         15.2   8
#> Cadillac Fleetwood  10.4   8
#> Lincoln Continental 10.4   8
#> Chrysler Imperial   14.7   8
#> Fiat 128            32.4   4
#> Honda Civic         30.4   4
#> Toyota Corolla      33.9   4
#> Toyota Corona       21.5   4
#> Dodge Challenger    15.5   8
#> AMC Javelin         15.2   8
#> Camaro Z28          13.3   8
#> Pontiac Firebird    19.2   8
#> Fiat X1-9           27.3   4
#> Porsche 914-2       26.0   4
#> Lotus Europa        30.4   4
#> Ford Pantera L      15.8   8
#> Ferrari Dino        19.7   6
#> Maserati Bora       15.0   8
#> Volvo 142E          21.4   4

# Select by string - all
col_names_any <- c("mpg","cyl","duck")
mtcars %>% 
  select(any_of(col_names_any))
#>                      mpg cyl
#> Mazda RX4           21.0   6
#> Mazda RX4 Wag       21.0   6
#> Datsun 710          22.8   4
#> Hornet 4 Drive      21.4   6
#> Hornet Sportabout   18.7   8
#> Valiant             18.1   6
#> Duster 360          14.3   8
#> Merc 240D           24.4   4
#> Merc 230            22.8   4
#> Merc 280            19.2   6
#> Merc 280C           17.8   6
#> Merc 450SE          16.4   8
#> Merc 450SL          17.3   8
#> Merc 450SLC         15.2   8
#> Cadillac Fleetwood  10.4   8
#> Lincoln Continental 10.4   8
#> Chrysler Imperial   14.7   8
#> Fiat 128            32.4   4
#> Honda Civic         30.4   4
#> Toyota Corolla      33.9   4
#> Toyota Corona       21.5   4
#> Dodge Challenger    15.5   8
#> AMC Javelin         15.2   8
#> Camaro Z28          13.3   8
#> Pontiac Firebird    19.2   8
#> Fiat X1-9           27.3   4
#> Porsche 914-2       26.0   4
#> Lotus Europa        30.4   4
#> Ford Pantera L      15.8   8
#> Ferrari Dino        19.7   6
#> Maserati Bora       15.0   8
#> Volvo 142E          21.4   4

# Error
col_names_all <- c("mpg","cyl")
mtcars %>% 
  select(all_of(col_names_all))
#>                      mpg cyl
#> Mazda RX4           21.0   6
#> Mazda RX4 Wag       21.0   6
#> Datsun 710          22.8   4
#> Hornet 4 Drive      21.4   6
#> Hornet Sportabout   18.7   8
#> Valiant             18.1   6
#> Duster 360          14.3   8
#> Merc 240D           24.4   4
#> Merc 230            22.8   4
#> Merc 280            19.2   6
#> Merc 280C           17.8   6
#> Merc 450SE          16.4   8
#> Merc 450SL          17.3   8
#> Merc 450SLC         15.2   8
#> Cadillac Fleetwood  10.4   8
#> Lincoln Continental 10.4   8
#> Chrysler Imperial   14.7   8
#> Fiat 128            32.4   4
#> Honda Civic         30.4   4
#> Toyota Corolla      33.9   4
#> Toyota Corona       21.5   4
#> Dodge Challenger    15.5   8
#> AMC Javelin         15.2   8
#> Camaro Z28          13.3   8
#> Pontiac Firebird    19.2   8
#> Fiat X1-9           27.3   4
#> Porsche 914-2       26.0   4
#> Lotus Europa        30.4   4
#> Ford Pantera L      15.8   8
#> Ferrari Dino        19.7   6
#> Maserati Bora       15.0   8
#> Volvo 142E          21.4   4

# Reorder, include everything
mtcars %>% 
  select(vs,am,everything())
#>                     vs am  mpg cyl  disp  hp drat    wt  qsec gear carb
#> Mazda RX4            0  1 21.0   6 160.0 110 3.90 2.620 16.46    4    4
#> Mazda RX4 Wag        0  1 21.0   6 160.0 110 3.90 2.875 17.02    4    4
#> Datsun 710           1  1 22.8   4 108.0  93 3.85 2.320 18.61    4    1
#> Hornet 4 Drive       1  0 21.4   6 258.0 110 3.08 3.215 19.44    3    1
#> Hornet Sportabout    0  0 18.7   8 360.0 175 3.15 3.440 17.02    3    2
#> Valiant              1  0 18.1   6 225.0 105 2.76 3.460 20.22    3    1
#> Duster 360           0  0 14.3   8 360.0 245 3.21 3.570 15.84    3    4
#> Merc 240D            1  0 24.4   4 146.7  62 3.69 3.190 20.00    4    2
#> Merc 230             1  0 22.8   4 140.8  95 3.92 3.150 22.90    4    2
#> Merc 280             1  0 19.2   6 167.6 123 3.92 3.440 18.30    4    4
#> Merc 280C            1  0 17.8   6 167.6 123 3.92 3.440 18.90    4    4
#> Merc 450SE           0  0 16.4   8 275.8 180 3.07 4.070 17.40    3    3
#> Merc 450SL           0  0 17.3   8 275.8 180 3.07 3.730 17.60    3    3
#> Merc 450SLC          0  0 15.2   8 275.8 180 3.07 3.780 18.00    3    3
#> Cadillac Fleetwood   0  0 10.4   8 472.0 205 2.93 5.250 17.98    3    4
#> Lincoln Continental  0  0 10.4   8 460.0 215 3.00 5.424 17.82    3    4
#> Chrysler Imperial    0  0 14.7   8 440.0 230 3.23 5.345 17.42    3    4
#> Fiat 128             1  1 32.4   4  78.7  66 4.08 2.200 19.47    4    1
#> Honda Civic          1  1 30.4   4  75.7  52 4.93 1.615 18.52    4    2
#> Toyota Corolla       1  1 33.9   4  71.1  65 4.22 1.835 19.90    4    1
#> Toyota Corona        1  0 21.5   4 120.1  97 3.70 2.465 20.01    3    1
#> Dodge Challenger     0  0 15.5   8 318.0 150 2.76 3.520 16.87    3    2
#> AMC Javelin          0  0 15.2   8 304.0 150 3.15 3.435 17.30    3    2
#> Camaro Z28           0  0 13.3   8 350.0 245 3.73 3.840 15.41    3    4
#> Pontiac Firebird     0  0 19.2   8 400.0 175 3.08 3.845 17.05    3    2
#> Fiat X1-9            1  1 27.3   4  79.0  66 4.08 1.935 18.90    4    1
#> Porsche 914-2        0  1 26.0   4 120.3  91 4.43 2.140 16.70    5    2
#> Lotus Europa         1  1 30.4   4  95.1 113 3.77 1.513 16.90    5    2
#> Ford Pantera L       0  1 15.8   8 351.0 264 4.22 3.170 14.50    5    4
#> Ferrari Dino         0  1 19.7   6 145.0 175 3.62 2.770 15.50    5    6
#> Maserati Bora        0  1 15.0   8 301.0 335 3.54 3.570 14.60    5    8
#> Volvo 142E           1  1 21.4   4 121.0 109 4.11 2.780 18.60    4    2

# Rename columns during select, note it will only keep those listed
mtcars %>% 
  select(cylinders = cyl)
#>                     cylinders
#> Mazda RX4                   6
#> Mazda RX4 Wag               6
#> Datsun 710                  4
#> Hornet 4 Drive              6
#> Hornet Sportabout           8
#> Valiant                     6
#> Duster 360                  8
#> Merc 240D                   4
#> Merc 230                    4
#> Merc 280                    6
#> Merc 280C                   6
#> Merc 450SE                  8
#> Merc 450SL                  8
#> Merc 450SLC                 8
#> Cadillac Fleetwood          8
#> Lincoln Continental         8
#> Chrysler Imperial           8
#> Fiat 128                    4
#> Honda Civic                 4
#> Toyota Corolla              4
#> Toyota Corona               4
#> Dodge Challenger            8
#> AMC Javelin                 8
#> Camaro Z28                  8
#> Pontiac Firebird            8
#> Fiat X1-9                   4
#> Porsche 914-2               4
#> Lotus Europa                4
#> Ford Pantera L              8
#> Ferrari Dino                6
#> Maserati Bora               8
#> Volvo 142E                  4
```

## filter

``` r
flights <- nycflights13::flights

# Numerical filtering
flights %>%
  filter(month >= 6, day == 1)
#> # A tibble: 6,376 × 19
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013    10     1      447            500       -13      614            648
#>  2  2013    10     1      522            517         5      735            757
#>  3  2013    10     1      536            545        -9      809            855
#>  4  2013    10     1      539            545        -6      801            827
#>  5  2013    10     1      539            545        -6      917            933
#>  6  2013    10     1      544            550        -6      912            932
#>  7  2013    10     1      549            600       -11      653            716
#>  8  2013    10     1      550            600       -10      648            700
#>  9  2013    10     1      550            600       -10      649            659
#> 10  2013    10     1      551            600        -9      727            730
#> # … with 6,366 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

# is eqivalent to
flights %>%
  filter(month >= 6 & day == 1)
#> # A tibble: 6,376 × 19
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013    10     1      447            500       -13      614            648
#>  2  2013    10     1      522            517         5      735            757
#>  3  2013    10     1      536            545        -9      809            855
#>  4  2013    10     1      539            545        -6      801            827
#>  5  2013    10     1      539            545        -6      917            933
#>  6  2013    10     1      544            550        -6      912            932
#>  7  2013    10     1      549            600       -11      653            716
#>  8  2013    10     1      550            600       -10      648            700
#>  9  2013    10     1      550            600       -10      649            659
#> 10  2013    10     1      551            600        -9      727            730
#> # … with 6,366 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

# Filter for specific values
flights %>%
  filter(month %in% c(1,3,5,7,9))
#> # A tibble: 141,633 × 19
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     1     1      517            515         2      830            819
#>  2  2013     1     1      533            529         4      850            830
#>  3  2013     1     1      542            540         2      923            850
#>  4  2013     1     1      544            545        -1     1004           1022
#>  5  2013     1     1      554            600        -6      812            837
#>  6  2013     1     1      554            558        -4      740            728
#>  7  2013     1     1      555            600        -5      913            854
#>  8  2013     1     1      557            600        -3      709            723
#>  9  2013     1     1      557            600        -3      838            846
#> 10  2013     1     1      558            600        -2      753            745
#> # … with 141,623 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

# Betwween two numbers
# Between matches EQUAL and larger/smaller. 
flights %>% 
  filter(between(month,6,8)) %>% 
  count(month)
#> # A tibble: 3 × 2
#>   month     n
#>   <int> <int>
#> 1     6 28243
#> 2     7 29425
#> 3     8 29327

# Grouped filters
flights %>% 
  group_by(tailnum) %>% 
  filter(all(dep_delay < 0))
#> # A tibble: 238 × 19
#> # Groups:   tailnum [124]
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     1     1      622            630        -8     1017           1014
#>  2  2013     1     1     1059           1100        -1     1201           1215
#>  3  2013     1     2      626            630        -4      850            833
#>  4  2013     1     2      629            630        -1     1010           1014
#>  5  2013     1     2     1827           1829        -2     2035           2032
#>  6  2013     1     4      616            630       -14      806            833
#>  7  2013     1     4      622            630        -8     1004           1014
#>  8  2013     1     5      606            610        -4      857            910
#>  9  2013     1     5      627            630        -3      945           1014
#> 10  2013     1     5      734            740        -6     1101           1109
#> # … with 228 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
#> #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
#> #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

# String filters
nycflights13::airports %>% 
  filter(name == "Williams County Airport")
#> # A tibble: 1 × 8
#>   faa   name                      lat   lon   alt    tz dst   tzone           
#>   <chr> <chr>                   <dbl> <dbl> <dbl> <dbl> <chr> <chr>           
#> 1 0G6   Williams County Airport  41.5 -84.5   730    -5 A     America/New_York

nycflights13::airports %>% 
  filter(str_detect(name,"County"))
#> # A tibble: 117 × 8
#>    faa   name                                 lat    lon   alt    tz dst   tzone
#>    <chr> <chr>                              <dbl>  <dbl> <dbl> <dbl> <chr> <chr>
#>  1 0G6   Williams County Airport             41.5  -84.5   730    -5 A     Amer…
#>  2 0S9   Jefferson County Intl               48.1 -123.    108    -8 A     Amer…
#>  3 0W3   Harford County Airport              39.6  -76.2   409    -5 A     Amer…
#>  4 17G   Port Bucyrus-Crawford County Airp…  40.8  -83.0  1003    -5 A     Amer…
#>  5 19A   Jackson County Airport              34.2  -83.6   951    -5 U     Amer…
#>  6 24J   Suwannee County Airport             30.3  -83.0   104    -5 A     Amer…
#>  7 2G2   Jefferson County Airpark            40.4  -80.7  1196    -5 A     Amer…
#>  8 2G9   Somerset County Airport             40.0  -79.0  2275    -5 A     Amer…
#>  9 2H0   Shelby County Airport               39.4  -88.8   550    -6 A     Amer…
#> 10 3G4   Ashland County Airport              40.9  -82.3  1206    -5 A     Amer…
#> # … with 107 more rows
```

## mutate

``` r
flights %>% 
  mutate(ave_speed = distance/air_time*60)
#> # A tibble: 336,776 × 20
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     1     1      517            515         2      830            819
#>  2  2013     1     1      533            529         4      850            830
#>  3  2013     1     1      542            540         2      923            850
#>  4  2013     1     1      544            545        -1     1004           1022
#>  5  2013     1     1      554            600        -6      812            837
#>  6  2013     1     1      554            558        -4      740            728
#>  7  2013     1     1      555            600        -5      913            854
#>  8  2013     1     1      557            600        -3      709            723
#>  9  2013     1     1      557            600        -3      838            846
#> 10  2013     1     1      558            600        -2      753            745
#> # … with 336,766 more rows, and 12 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>,
#> #   ave_speed <dbl>

flights %>% 
  transmute(arr_delay,
            on_time1 = arr_delay < 0,
            on_time2 = if_else(arr_delay > 0,"Late","On-time"),
            # Functions that return a single result will be repeated in each row
            ave_delay_mean = mean(arr_delay,na.rm = T),
            ave_delay = arr_delay > 0)
#> # A tibble: 336,776 × 5
#>    arr_delay on_time1 on_time2 ave_delay_mean ave_delay
#>        <dbl> <lgl>    <chr>             <dbl> <lgl>    
#>  1        11 FALSE    Late               6.90 TRUE     
#>  2        20 FALSE    Late               6.90 TRUE     
#>  3        33 FALSE    Late               6.90 TRUE     
#>  4       -18 TRUE     On-time            6.90 FALSE    
#>  5       -25 TRUE     On-time            6.90 FALSE    
#>  6        12 FALSE    Late               6.90 TRUE     
#>  7        19 FALSE    Late               6.90 TRUE     
#>  8       -14 TRUE     On-time            6.90 FALSE    
#>  9        -8 TRUE     On-time            6.90 FALSE    
#> 10         8 FALSE    Late               6.90 TRUE     
#> # … with 336,766 more rows

flights %>% 
  transmute(across(c(dep_time,arr_time),as.character),
            dep_time = str_pad(dep_time,4,pad = "0",side = "left"),
            dep_hour = str_sub(dep_time,start = 1,end = 2),
            dep_min = str_sub(dep_time,start = 3,end = 4))
#> # A tibble: 336,776 × 4
#>    dep_time arr_time dep_hour dep_min
#>    <chr>    <chr>    <chr>    <chr>  
#>  1 0517     830      05       17     
#>  2 0533     850      05       33     
#>  3 0542     923      05       42     
#>  4 0544     1004     05       44     
#>  5 0554     812      05       54     
#>  6 0554     740      05       54     
#>  7 0555     913      05       55     
#>  8 0557     709      05       57     
#>  9 0557     838      05       57     
#> 10 0558     753      05       58     
#> # … with 336,766 more rows
```

## summarise

``` r
flights %>% 
  summarise(n = n(),
            mean_late = mean(arr_delay,na.rm = T),
            sd = mean(arr_delay,na.rm = T))
#> # A tibble: 1 × 3
#>        n mean_late    sd
#>    <int>     <dbl> <dbl>
#> 1 336776      6.90  6.90


flights %>% 
  group_by(origin) %>% 
  summarise(n = n(),
            mean_late = mean(arr_delay,na.rm = T),
            sd = mean(arr_delay,na.rm = T))
#> # A tibble: 3 × 4
#>   origin      n mean_late    sd
#>   <chr>   <int>     <dbl> <dbl>
#> 1 EWR    120835      9.11  9.11
#> 2 JFK    111279      5.55  5.55
#> 3 LGA    104662      5.78  5.78

flights %>% 
  group_by(origin) %>% 
  summarise(unique_destinations = n_distinct(dest),
            unique_carriers = n_distinct(carrier))
#> # A tibble: 3 × 3
#>   origin unique_destinations unique_carriers
#>   <chr>                <int>           <int>
#> 1 EWR                     86              12
#> 2 JFK                     70              10
#> 3 LGA                     68              13
```

## head/tail/slice

``` r
flights %>% 
  head()
#> # A tibble: 6 × 19
#>    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#> 1  2013     1     1      517            515         2      830            819
#> 2  2013     1     1      533            529         4      850            830
#> 3  2013     1     1      542            540         2      923            850
#> 4  2013     1     1      544            545        -1     1004           1022
#> 5  2013     1     1      554            600        -6      812            837
#> 6  2013     1     1      554            558        -4      740            728
#> # … with 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
#> #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
#> #   hour <dbl>, minute <dbl>, time_hour <dttm>

flights %>% 
  tail(10)
#> # A tibble: 10 × 19
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     9    30     2240           2250       -10     2347              7
#>  2  2013     9    30     2241           2246        -5     2345              1
#>  3  2013     9    30     2307           2255        12     2359           2358
#>  4  2013     9    30     2349           2359       -10      325            350
#>  5  2013     9    30       NA           1842        NA       NA           2019
#>  6  2013     9    30       NA           1455        NA       NA           1634
#>  7  2013     9    30       NA           2200        NA       NA           2312
#>  8  2013     9    30       NA           1210        NA       NA           1330
#>  9  2013     9    30       NA           1159        NA       NA           1344
#> 10  2013     9    30       NA            840        NA       NA           1020
#> # … with 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
#> #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
#> #   hour <dbl>, minute <dbl>, time_hour <dttm>

flights %>% 
  group_by(tailnum) %>% 
  arrange(month,day,dep_time) %>% 
  slice(1)
#> # A tibble: 4,044 × 19
#> # Groups:   tailnum [4,044]
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     2    11     1508           1400        68     1807           1636
#>  2  2013     1     1     1604           1510        54     1817           1710
#>  3  2013     1    10      626            630        -4      802            800
#>  4  2013     1    31      623            630        -7      850            831
#>  5  2013     1     6      629            630        -1      820            841
#>  6  2013     1    13     1829           1829         0     2018           2032
#>  7  2013     1     2     1548           1340       128     1710           1500
#>  8  2013     2    10      757            759        -2      931           1011
#>  9  2013     1    12     1847           1850        -3     2039           2055
#> 10  2013     1    16      623            630        -7      849            831
#> # … with 4,034 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

flights %>% 
  group_by(tailnum) %>% 
  arrange(month,day,dep_time) %>% 
  slice(1)
#> # A tibble: 4,044 × 19
#> # Groups:   tailnum [4,044]
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     2    11     1508           1400        68     1807           1636
#>  2  2013     1     1     1604           1510        54     1817           1710
#>  3  2013     1    10      626            630        -4      802            800
#>  4  2013     1    31      623            630        -7      850            831
#>  5  2013     1     6      629            630        -1      820            841
#>  6  2013     1    13     1829           1829         0     2018           2032
#>  7  2013     1     2     1548           1340       128     1710           1500
#>  8  2013     2    10      757            759        -2      931           1011
#>  9  2013     1    12     1847           1850        -3     2039           2055
#> 10  2013     1    16      623            630        -7      849            831
#> # … with 4,034 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

flights %>% 
  arrange(distance) %>% 
  slice(1:5,(n() - 4):n())
#> # A tibble: 10 × 19
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     7    27       NA            106        NA       NA            245
#>  2  2013     1     3     2127           2129        -2     2222           2224
#>  3  2013     1     4     1240           1200        40     1333           1306
#>  4  2013     1     4     1829           1615       134     1937           1721
#>  5  2013     1     4     2128           2129        -1     2218           2224
#>  6  2013     9    25     1001           1000         1     1508           1445
#>  7  2013     9    27      951           1000        -9     1442           1445
#>  8  2013     9    28      955           1000        -5     1412           1445
#>  9  2013     9    29      957           1000        -3     1405           1445
#> 10  2013     9    30      959           1000        -1     1438           1445
#> # … with 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
#> #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
#> #   hour <dbl>, minute <dbl>, time_hour <dttm>

flights %>% 
  group_by(tailnum) %>% 
  slice_max(distance,n = 1,with_ties = F)
#> # A tibble: 4,044 × 19
#> # Groups:   tailnum [4,044]
#>     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#>  1  2013     3    23     1340           1300        40     1638           1554
#>  2  2013    12     4     1513           1520        -7     1744           1750
#>  3  2013     1    16     2114           1935        99       12           2220
#>  4  2013    12     4      836            845        -9     1035           1053
#>  5  2013     1     6      629            630        -1      820            841
#>  6  2013    11    14     1542           1544        -2     1744           1750
#>  7  2013     4     1      815            822        -7     1042           1045
#>  8  2013    10    27     1543           1545        -2     1747           1751
#>  9  2013     1    12     1847           1850        -3     2039           2055
#> 10  2013    10    14     1533           1540        -7     1741           1742
#> # … with 4,034 more rows, and 11 more variables: arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#> #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>
```

## group_by

``` r
print_return <- function(x) {
  print(x)
  x
}

example_data <- 
  tibble(dat = 1:6,grp = rep(c("A","B"),times = 3)) 

example_data %>% 
  mutate(ret = print_return(dat),
         min_dat = min(ret))
#> [1] 1 2 3 4 5 6
#> # A tibble: 6 × 4
#>     dat grp     ret min_dat
#>   <int> <chr> <int>   <int>
#> 1     1 A         1       1
#> 2     2 B         2       1
#> 3     3 A         3       1
#> 4     4 B         4       1
#> 5     5 A         5       1
#> 6     6 B         6       1

example_data %>% 
  group_by(grp) %>% 
  mutate(ret = print_return(dat),
         min_dat = min(ret))  
#> [1] 1 3 5
#> [1] 2 4 6
#> # A tibble: 6 × 4
#> # Groups:   grp [2]
#>     dat grp     ret min_dat
#>   <int> <chr> <int>   <int>
#> 1     1 A         1       1
#> 2     2 B         2       2
#> 3     3 A         3       1
#> 4     4 B         4       2
#> 5     5 A         5       1
#> 6     6 B         6       2
```

## arrange

``` r
flights %>% 
  distinct(carrier,month,day) %>% 
  arrange(desc(carrier),-month,-day) %>% 
  select(carrier,month,day) 
#> # A tibble: 5,432 × 3
#>    carrier month   day
#>    <chr>   <int> <int>
#>  1 YV         12    31
#>  2 YV         12    30
#>  3 YV         12    28
#>  4 YV         12    27
#>  5 YV         12    26
#>  6 YV         12    24
#>  7 YV         12    23
#>  8 YV         12    22
#>  9 YV         12    21
#> 10 YV         12    20
#> # … with 5,422 more rows
```
