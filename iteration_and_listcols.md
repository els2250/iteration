Iteration and List Columns
================
Emma Sexton

## Lists

``` r
vec_numeric <- 5:8
vec_logical <- c(TRUE, FALSE, TRUE, TRUE)
```

Lets look at a list

``` r
l = list(
  vec_numeric = 5:8,
  mat         = matrix(1:8, 2, 4),
  vec_logical = c(TRUE, FALSE),
  summary     = summary(rnorm(1000))
)
```

Accessing list items

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[3]]
```

    ## [1]  TRUE FALSE

``` r
l[["mat"]]
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8

## Loops!

Let’s write a `for` loop to take the mean nand SD of four samples from a
normal distribution

``` r
list_norm = 
  list(
    a = rnorm(20, 5, 4),
    b = rnorm(20, -12, 3),
    c = rnorm(20, 17, 0.4),
    d = rnorm(20, 100, 1)
  )
```

Here’s my function

``` r
mean_and_sd <- function(x) {
  
  if (!is.numeric(x)) {
    stop("Z scores only work for numbers")
   }
  
  if (length(x) < 3) {
    stop("Z scores really only work if you have three or more numbers")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)
  
  tibble(
    mean = mean_x,
    sd = sd_x
  )
}
```

Let’s try to make this work.

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.54  2.75

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -12.1  2.26

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  17.0 0.356

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  100.  1.39

Let’s try a `for` loop instead.

``` r
output = vector("list", length = 4)
# this is an empty list -- this is where we're going to put the output

output[[1]] = mean_and_sd(list_norm[[1]])
# now we want to do that multiple times

for(i in 1:4) {
  
  output[[i]] = mean_and_sd(list_norm[[i]])

}

output
```

    ## [[1]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.54  2.75
    ## 
    ## [[2]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -12.1  2.26
    ## 
    ## [[3]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  17.0 0.356
    ## 
    ## [[4]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  100.  1.39

## Can we map??

We can map!!

``` r
map(list_norm, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.54  2.75
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -12.1  2.26
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  17.0 0.356
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  100.  1.39

So… what about other functions?

``` r
map(list_norm, median)
```

    ## $a
    ## [1] 6.975467
    ## 
    ## $b
    ## [1] -11.67477
    ## 
    ## $c
    ## [1] 16.90897
    ## 
    ## $d
    ## [1] 100.1858

``` r
map(list_norm, var)
```

    ## $a
    ## [1] 7.582721
    ## 
    ## $b
    ## [1] 5.089954
    ## 
    ## $c
    ## [1] 0.1268152
    ## 
    ## $d
    ## [1] 1.937131

``` r
map(list_norm, summary)
```

    ## $a
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.9949  4.6090  6.9755  6.5406  8.9325 10.9738 
    ## 
    ## $b
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -16.649 -13.001 -11.675 -12.071 -10.969  -7.846 
    ## 
    ## $c
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   16.26   16.71   16.91   16.95   17.26   17.55 
    ## 
    ## $d
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   97.82   99.15  100.19  100.03  101.13  102.36

map variants…

``` r
map(list_norm, median)
```

    ## $a
    ## [1] 6.975467
    ## 
    ## $b
    ## [1] -11.67477
    ## 
    ## $c
    ## [1] 16.90897
    ## 
    ## $d
    ## [1] 100.1858

``` r
# sometimes lists are a hassle

map_dbl(list_norm, median)
```

    ##          a          b          c          d 
    ##   6.975467 -11.674767  16.908970 100.185789

``` r
map_df(list_norm, mean_and_sd)
```

    ## # A tibble: 4 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1   6.54 2.75 
    ## 2 -12.1  2.26 
    ## 3  17.0  0.356
    ## 4 100.   1.39

``` r
# these simplify the outputs

output = map_df(list_norm, mean_and_sd)
# can also save it as above^
```

## List columns…

``` r
listcol_df =
  tibble(
    name = c("a", "b", "c", "d"),
    norm = list_norm
  )

listcol_df[["norm"]]
```

    ## $a
    ##  [1]  8.9020353  5.8429128  5.2102619 10.9737717  4.1326404  9.5529804
    ##  [7]  0.9949455  8.3279937  2.0666405  4.7677805  3.8261793  6.8176675
    ## [13]  9.4751214  9.0239809  7.1332657  9.1475584  3.5645581  5.1983615
    ## [19]  8.5317824  7.3220146
    ## 
    ## $b
    ##  [1] -11.582220 -11.479957 -12.545093 -11.539298  -8.251842  -7.845887
    ##  [7] -12.773879 -10.034273 -11.125667 -11.767315 -12.495287 -16.297028
    ## [13] -14.423348 -10.352121 -14.165990 -11.414605 -10.500343 -13.683446
    ## [19] -12.484979 -16.649441
    ## 
    ## $c
    ##  [1] 17.54513 16.68475 16.71320 16.85204 17.25980 16.68741 17.38765 16.73545
    ##  [9] 16.42623 17.13349 17.14077 16.81835 17.26431 16.96590 17.17334 16.59057
    ## [17] 17.45065 16.72986 16.25545 17.25935
    ## 
    ## $d
    ##  [1] 101.27846  97.82176  98.94705 101.37787  98.02684 101.52930 100.07915
    ##  [8]  99.37265 101.90930 100.78427  99.48466  97.82724 101.07791 100.87928
    ## [15]  98.23426 100.38523 100.29243  99.21764  99.73299 102.36419

``` r
map(listcol_df[["norm"]], mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.54  2.75
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -12.1  2.26
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  17.0 0.356
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  100.  1.39

``` r
# only thing change is that now that's in a data frame, extract variable, then apply function
# problem: output isn't in the data frame
```

Can we add list columns, and then what

``` r
listcol_df %>% 
  mutate(
    m_sd = map(norm, mean_and_sd)
  ) %>% 
  select(-norm)
```

    ## # A tibble: 4 × 2
    ##   name  m_sd            
    ##   <chr> <named list>    
    ## 1 a     <tibble [1 × 2]>
    ## 2 b     <tibble [1 × 2]>
    ## 3 c     <tibble [1 × 2]>
    ## 4 d     <tibble [1 × 2]>

## What about something more realistic…

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

    ## using cached file: ~/Library/Caches/R/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2022-09-29 11:01:00 (8.401)

    ## file min/max dates: 1869-01-01 / 2022-09-30

    ## using cached file: ~/Library/Caches/R/noaa_ghcnd/USC00519397.dly

    ## date created (size, mb): 2022-09-29 11:01:06 (1.699)

    ## file min/max dates: 1965-01-01 / 2020-03-31

    ## using cached file: ~/Library/Caches/R/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2022-09-29 11:01:09 (0.95)

    ## file min/max dates: 1999-09-01 / 2022-09-30

Let’s nest within weather stations…

``` r
weather_nest_df = 
  weather_df %>% 
  nest(data = date:tmin)
# collapse down to a single data frame
```

Really is a list column!

``` r
weather_nest_df[["data"]]
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

``` r
weather_nest_df[["data"]][[1]]
```

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

``` r
lm(tmax ~ tmin, data = weather_nest_df[["data"]][[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = weather_nest_df[["data"]][[1]])
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

``` r
lm(tmax ~ tmin, data = weather_nest_df[["data"]][[2]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = weather_nest_df[["data"]][[2]])
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##     20.0966       0.4509

``` r
lm(tmax ~ tmin, data = weather_nest_df[["data"]][[3]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = weather_nest_df[["data"]][[3]])
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.499        1.221

``` r
# for a different data set each time (Waikiki, Central Park, and Waterhole)
```

Let’s write a short lil ol function

``` r
weather_lm = function(df) {
  
  lm(tmax ~ tmin, data = df)
  
}

weather_lm(weather_nest_df[["data"]][[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

Advantage of having a function is we can map across a list of data
frames

``` r
map(weather_nest_df[["data"]], weather_lm)
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

Spits out a LIST with a linear model of each thing

Map function – give it an input LIST and a FUNCTION; it’ll apply that
element to each element of that list (which can be a data frame – see
nested)

One more problem to solve… we have to pull out the data frame

Start with data frame and mutate to add a column that is a list of
linear regression results

Can I do all this in a tidy way?

``` r
weather_nest_df %>% 
  mutate(
    models = map(data, weather_lm)
  )
```

    ## # A tibble: 3 × 4
    ##   name           id          data               models
    ##   <chr>          <chr>       <list>             <list>
    ## 1 CentralPark_NY USW00094728 <tibble [365 × 4]> <lm>  
    ## 2 Waikiki_HA     USC00519397 <tibble [365 × 4]> <lm>  
    ## 3 Waterhole_WA   USS0023B17S <tibble [365 × 4]> <lm>

YUP

Unnesting

``` r
weather_nest_df %>% 
  unnest(data)
```

    ## # A tibble: 1,095 × 6
    ##    name           id          date        prcp  tmax  tmin
    ##    <chr>          <chr>       <date>     <dbl> <dbl> <dbl>
    ##  1 CentralPark_NY USW00094728 2017-01-01     0   8.9   4.4
    ##  2 CentralPark_NY USW00094728 2017-01-02    53   5     2.8
    ##  3 CentralPark_NY USW00094728 2017-01-03   147   6.1   3.9
    ##  4 CentralPark_NY USW00094728 2017-01-04     0  11.1   1.1
    ##  5 CentralPark_NY USW00094728 2017-01-05     0   1.1  -2.7
    ##  6 CentralPark_NY USW00094728 2017-01-06    13   0.6  -3.8
    ##  7 CentralPark_NY USW00094728 2017-01-07    81  -3.2  -6.6
    ##  8 CentralPark_NY USW00094728 2017-01-08     0  -3.8  -8.8
    ##  9 CentralPark_NY USW00094728 2017-01-09     0  -4.9  -9.9
    ## 10 CentralPark_NY USW00094728 2017-01-10     0   7.8  -6  
    ## # … with 1,085 more rows

``` r
# gets you back to the data column you had
```

## Napoleon!!

Here’s my scraping function that works for a single page:

``` r
read_page_reviews <- function(url) {
  
  html = read_html(url)
  
  review_titles = 
    html %>%
    html_nodes(".a-text-bold span") %>%
    html_text()
  
  review_stars = 
    html %>%
    html_nodes("#cm_cr-review_list .review-rating") %>%
    html_text() %>%
    str_extract("^\\d") %>%
    as.numeric()
  
  review_text = 
    html %>%
    html_nodes(".review-text-content span") %>%
    html_text() %>% 
    str_replace_all("\n", "") %>% 
    str_trim() %>% 
    str_subset("The media could not be loaded.", negate = TRUE) %>% 
    str_subset("^$", negate = TRUE)
  
  tibble(
    title = review_titles,
    stars = review_stars,
    text = review_text
  )
}
```

What we did last time:

``` r
url_base = "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber="

vec_url = str_c(url_base, 1:5)

map(vec_url, read_page_reviews)
```

    ## [[1]]
    ## # A tibble: 10 × 3
    ##    title                                      stars text                        
    ##    <chr>                                      <dbl> <chr>                       
    ##  1 Goofy movie                                    5 I used this movie for a mid…
    ##  2 Lol hey it’s Napoleon. What’s not to love…     5 Vote for Pedro              
    ##  3 Still the best                                 5 Completely stupid, absolute…
    ##  4 70’s and 80’s Schtick Comedy                   5 …especially funny if you ha…
    ##  5 Amazon Censorship                              5 I hope Amazon does not cens…
    ##  6 Watch to say you did                           3 I know it's supposed to be …
    ##  7 Best Movie Ever!                               5 We just love this movie and…
    ##  8 Quirky                                         5 Good family film            
    ##  9 Funny movie - can't play it !                  1 Sony 4k player won't even r…
    ## 10 A brilliant story about teenage life           5 Napoleon Dynamite delivers …
    ## 
    ## [[2]]
    ## # A tibble: 10 × 3
    ##    title                                         stars text                     
    ##    <chr>                                         <dbl> <chr>                    
    ##  1 HUHYAH                                            5 Spicy                    
    ##  2 Cult Classic                                      4 Takes a time or two to f…
    ##  3 Sweet                                             5 Timeless Movie. My Grand…
    ##  4 Cute                                              4 Fun                      
    ##  5 great collectible                                 5 one of the greatest movi…
    ##  6 Iconic, hilarious flick ! About friend ship .     5 Who doesn’t love this mo…
    ##  7 Funny                                             5 Me and my dad watched th…
    ##  8 Low budget but okay                               3 This has been a classic …
    ##  9 Disappointing                                     2 We tried to like this, b…
    ## 10 Favorite movie 🍿                                 5 This is one of my favori…
    ## 
    ## [[3]]
    ## # A tibble: 10 × 3
    ##    title                                                             stars text 
    ##    <chr>                                                             <dbl> <chr>
    ##  1 none                                                                  5 "thi…
    ##  2 Great movie                                                           5 "Vot…
    ##  3 Get this to improve your nunchuck and bowstaff skills. Dancing i…     5 "Got…
    ##  4 Incredible Movie                                                      5 "Fun…
    ##  5 Always loved this movie!                                              5 "I h…
    ##  6 Great movie                                                           5 "Bou…
    ##  7 The case was damaged                                                  3 "It …
    ##  8 It’s classic                                                          5 "Cle…
    ##  9 Irreverent comedy                                                     5 "If …
    ## 10 Great classic!                                                        5 "Fun…
    ## 
    ## [[4]]
    ## # A tibble: 10 × 3
    ##    title                                                             stars text 
    ##    <chr>                                                             <dbl> <chr>
    ##  1 Most Awesomsomest Movie EVER!!!                                       5 "Thi…
    ##  2 Always a favorite                                                     5 "I r…
    ##  3 It’s not working the disc keeps showing error when I tried other…     1 "It’…
    ##  4 Gosh!                                                                 5 "Eve…
    ##  5 An Acquired Taste                                                     1 "Thi…
    ##  6 What is this ?                                                        4 "Nic…
    ##  7 Napoleon Dynamite                                                     2 "I w…
    ##  8 Great movie                                                           5 "Gre…
    ##  9 Good movie                                                            5 "Goo…
    ## 10 Came as Described                                                     5 "Cam…
    ## 
    ## [[5]]
    ## # A tibble: 10 × 3
    ##    title                                                           stars text   
    ##    <chr>                                                           <dbl> <chr>  
    ##  1 Oddly on my list of keepers.                                        5 "Good …
    ##  2 Low budget fun                                                      5 "Oddba…
    ##  3 On a scale of 1 to 10 this rates a minus                            1 "This …
    ##  4 I always wondered...                                                5 "what …
    ##  5 Audio/video not synced                                              1 "I tho…
    ##  6 Kind of feels like only a bully would actually laugh at this...     1 "...as…
    ##  7 movie                                                               5 "good …
    ##  8 An Overdose of Comical Cringe                                       5 "Excel…
    ##  9 Glad I never wasted money on this                                   2 "I rem…
    ## 10 A little disappointed                                               3 "The c…

``` r
napoleon_reviews = 
  tibble(
    page = 1:5,
    page_url = str_c(url_base, page)
  ) %>% 
  mutate(
    reviews = map(page_url, read_page_reviews)
  )

napoleon_reviews %>% 
  select(-page_url) %>% 
  unnest(reviews)
```

    ## # A tibble: 50 × 4
    ##     page title                                      stars text                  
    ##    <int> <chr>                                      <dbl> <chr>                 
    ##  1     1 Goofy movie                                    5 I used this movie for…
    ##  2     1 Lol hey it’s Napoleon. What’s not to love…     5 Vote for Pedro        
    ##  3     1 Still the best                                 5 Completely stupid, ab…
    ##  4     1 70’s and 80’s Schtick Comedy                   5 …especially funny if …
    ##  5     1 Amazon Censorship                              5 I hope Amazon does no…
    ##  6     1 Watch to say you did                           3 I know it's supposed …
    ##  7     1 Best Movie Ever!                               5 We just love this mov…
    ##  8     1 Quirky                                         5 Good family film      
    ##  9     1 Funny movie - can't play it !                  1 Sony 4k player won't …
    ## 10     1 A brilliant story about teenage life           5 Napoleon Dynamite del…
    ## # … with 40 more rows
