Writing Functions
================
Emma Sexton
2022-11-03

## Z-scores!!

Let’s compute the z-score version of a list of numbers.

``` r
x_vec = rnorm(25, mean = 7, sd = 4)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  1.35101500 -0.03640894  0.03577479 -2.02029397  1.36025288 -0.44594498
    ##  [7]  1.16626020  1.39065940 -1.08452799  1.07096733 -0.53264283  0.11516325
    ## [13]  0.06721428 -0.24582287  0.24785276 -0.28396296  0.91161322 -0.24980675
    ## [19] -0.40582855 -1.95964718 -0.50238365 -1.85451122  0.52914693  0.46021730
    ## [25]  0.91564453

Suppose you want to do this often.

``` r
z_scores = function(x) {
    
  if (!is.numeric(x)) {
    stop("Z scores only owork for numebrs")
   }
  
  if (length(x) < 3) {
    stop("Z scores really only work if you have three or more numbers")
  }
  
 z = (x - mean(x)) / sd(x)
 
 z
}
```

``` r
z_scores(x_vec)
```

    ##  [1]  1.35101500 -0.03640894  0.03577479 -2.02029397  1.36025288 -0.44594498
    ##  [7]  1.16626020  1.39065940 -1.08452799  1.07096733 -0.53264283  0.11516325
    ## [13]  0.06721428 -0.24582287  0.24785276 -0.28396296  0.91161322 -0.24980675
    ## [19] -0.40582855 -1.95964718 -0.50238365 -1.85451122  0.52914693  0.46021730
    ## [25]  0.91564453

``` r
z_scores(x = 1:10)
```

    ##  [1] -1.4863011 -1.1560120 -0.8257228 -0.4954337 -0.1651446  0.1651446
    ##  [7]  0.4954337  0.8257228  1.1560120  1.4863011

``` r
z_scores(x = rbinom(1000, 1, .6))
```

    ##    [1]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882
    ##    [7]  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##   [13] -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##   [19]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##   [25] -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##   [31]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##   [37]  0.8160882 -1.2241323 -1.2241323  0.8160882 -1.2241323 -1.2241323
    ##   [43] -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882
    ##   [49]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##   [55] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##   [61] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##   [67] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##   [73] -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323
    ##   [79] -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##   [85]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##   [91] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##   [97]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [103] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##  [109]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [115]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [121]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [127]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [133]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [139]  0.8160882 -1.2241323  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##  [145]  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323
    ##  [151]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [157]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [163]  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [169]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [175] -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [181]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [187]  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323
    ##  [193]  0.8160882 -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [199]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [205]  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [211] -1.2241323 -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [217]  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [223] -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [229]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [235]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##  [241]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323
    ##  [247] -1.2241323  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [253]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [259]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [265] -1.2241323 -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [271]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [277]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [283] -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [289]  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [295]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [301]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [307] -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [313]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##  [319]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [325]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [331] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [337] -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323 -1.2241323
    ##  [343]  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [349] -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [355]  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##  [361]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [367] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [373]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [379] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [385]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [391] -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##  [397]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [403] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [409] -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [415]  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [421]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [427]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [433] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##  [439]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [445] -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [451]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [457] -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [463]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [469] -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [475]  0.8160882 -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [481] -1.2241323  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [487] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [493]  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [499] -1.2241323  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [505]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [511]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [517]  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [523] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [529] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [535]  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323
    ##  [541]  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323 -1.2241323
    ##  [547]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [553]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [559] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [565]  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##  [571] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [577] -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [583]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [589] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [595]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [601]  0.8160882  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323
    ##  [607]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [613] -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [619] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [625] -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [631]  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [637] -1.2241323  0.8160882 -1.2241323 -1.2241323  0.8160882 -1.2241323
    ##  [643] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [649]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [655] -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [661]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [667] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [673]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [679] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [685]  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [691] -1.2241323  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [697] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [703]  0.8160882 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [709]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [715] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [721]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [727]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [733]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [739]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [745] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [751] -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [757] -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [763]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [769]  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [775] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323
    ##  [781]  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [787]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [793] -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [799] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [805]  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882
    ##  [811]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [817]  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323
    ##  [823]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [829] -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [835]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [841] -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [847] -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882
    ##  [853]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [859] -1.2241323  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [865] -1.2241323 -1.2241323  0.8160882  0.8160882 -1.2241323 -1.2241323
    ##  [871]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [877]  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [883] -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [889]  0.8160882  0.8160882 -1.2241323 -1.2241323  0.8160882  0.8160882
    ##  [895] -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [901]  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [907]  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882  0.8160882
    ##  [913]  0.8160882  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323
    ##  [919] -1.2241323  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [925] -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [931]  0.8160882 -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [937]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323
    ##  [943] -1.2241323 -1.2241323 -1.2241323  0.8160882 -1.2241323  0.8160882
    ##  [949]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882 -1.2241323
    ##  [955] -1.2241323 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [961] -1.2241323  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [967]  0.8160882  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882
    ##  [973]  0.8160882  0.8160882 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [979] -1.2241323  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [985]  0.8160882  0.8160882  0.8160882 -1.2241323  0.8160882  0.8160882
    ##  [991]  0.8160882 -1.2241323 -1.2241323 -1.2241323 -1.2241323  0.8160882
    ##  [997]  0.8160882 -1.2241323 -1.2241323 -1.2241323

``` r
#z_scores(x = 3)
# can't take the SD of one number

#z_scores(x = "my name is jeff")
# this won't work because it's not a number
```

## Let’s have multiple outputs

Let’s just get the mean and sd from the vector input.

``` r
mean_and_sd <- function(x) {
  
  if (!is.numeric(x)) {
    stop("Z scores only owork for numebrs")
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

mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.38  3.99

``` r
mean_and_sd(x = 1:10)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1   5.5  3.03

``` r
mean_and_sd(x = rbinom(1000, 1, .5))
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.506 0.500

## Let’s start with simulations…

``` r
x_vec = rnorm(n = 25, mean = 17, sd = 4)

tibble(
  mean = mean(x_vec),
  sd = sd(x_vec)
)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  17.3  3.11

Can I do this using a function … YUP

``` r
#set default values to true_mean and true_sd (if you don't replace it, it'll assume that)
sim_mean_sd = function(n_obs, true_mean = 7, true_sd = 4) {
  
  x = rnorm(n_obs, true_mean, true_sd)

  tibble(
    mean = mean(x),
    sd = sd(x)
  )
  
}
```

does it work?

``` r
sim_mean_sd(n_obs = 25,true_mean = 10, true_sd = 5)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.92  4.81

``` r
sim_mean_sd(25000)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.97  4.00

``` r
# you don't have to name depending on what you defined as arguments in the function
# it'll take them in whatever order, as long as you name them
```

## Fixing bad stuff

``` r
url = "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1"

dynamite_html = read_html(url)

review_titles = 
  dynamite_html %>%
  html_nodes(".a-text-bold span") %>%
  html_text()

review_stars = 
  dynamite_html %>%
  html_nodes("#cm_cr-review_list .review-rating") %>%
  html_text() %>%
  str_extract("^\\d") %>%
  as.numeric()

review_text = 
  dynamite_html %>%
  html_nodes(".review-text-content span") %>%
  html_text() %>% 
  str_replace_all("\n", "") %>% 
  str_trim()

reviews = tibble(
  title = review_titles,
  stars = review_stars,
  text = review_text
)
```

Let’s write a function to get reviews.

``` r
read_page_reviews <- function(url) {
  
  dynamite_html = read_html(url)

  review_titles = 
    dynamite_html %>%
    html_nodes(".a-text-bold span") %>%
    html_text()

  review_stars = 
    dynamite_html %>%
    html_nodes("#cm_cr-review_list .review-rating") %>%
    html_text() %>%
    str_extract("^\\d") %>%
    as.numeric()

  review_text = 
    dynamite_html %>%
    html_nodes(".review-text-content span") %>%
    html_text() %>% 
    str_replace_all("\n", "") %>% 
    str_trim()
  
  reviews = tibble(
    title = review_titles,
    stars = review_stars,
    text = review_text
  )
  
  reviews
}
```

Let’s try with a URL

``` r
url = "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=2"

read_page_reviews(url)
```

    ## # A tibble: 10 × 3
    ##    title                                         stars text                     
    ##    <chr>                                         <dbl> <chr>                    
    ##  1 Sweet                                             5 Timeless Movie. My Grand…
    ##  2 Cute                                              4 Fun                      
    ##  3 great collectible                                 5 one of the greatest movi…
    ##  4 Iconic, hilarious flick ! About friend ship .     5 Who doesn’t love this mo…
    ##  5 Funny                                             5 Me and my dad watched th…
    ##  6 Low budget but okay                               3 This has been a classic …
    ##  7 Disappointing                                     2 We tried to like this, b…
    ##  8 Favorite movie 🍿                                 5 This is one of my favori…
    ##  9 none                                              5 this movie was great Nap…
    ## 10 Great movie                                       5 Vote for pedro

What good does this do?

``` r
base_url <- "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber="

vec_url = str_c(base_url, c(1, 2, 4, 5))

dynamite_reviews <- 
  bind_rows(
    read_page_reviews(vec_url[1]),
    read_page_reviews(vec_url[2]),
    read_page_reviews(vec_url[4])
  )
```