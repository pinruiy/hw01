hw01-pinrui-yu.Rmd
================
Pinrui Yu
2/17/2018

2.Data Import(20 pt)

-   

``` r
column_names <- c(
    'symboling',
    'normalized_losses',
    'make',
    'fuel_type',
    'aspiration',
    'num_of_doors',
    'body_style',
    'drive_wheels',
    'engine_location',
    'wheel_base',
    'length',
    'width',
    'height',
    'curb_weight',
    'engine_type',
    'num_of_cylinders',
    'engine_size',
    'fuel_system',
    'bore',
    'stroke',
    'compression_ratio',
    'horsepower',
    'peak_rpm',
    'city_mpg',
    'highway_mpg',
    'price'
)

column_types <- c(
  'real',
  'real',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'real',
  'real',
  'real',
  'real',
  'integer',
  'character',
  'character',
  'integer',
  'character',
  'real',
  'real',
  'real',
  'integer',
  'integer',
  'integer',
  'integer',
  'integer'
)
```

-   

``` r
dat <- read.csv(
    'import-85.data',
    col.names = column_names,
    colClasses = column_types,
    na.string = "?",
    sep = ","
)
str(dat, vec.len = 1)
```

    ## 'data.frame':    204 obs. of  26 variables:
    ##  $ symboling        : num  3 1 ...
    ##  $ normalized_losses: num  NA NA ...
    ##  $ make             : chr  "alfa-romero" ...
    ##  $ fuel_type        : chr  "gas" ...
    ##  $ aspiration       : chr  "std" ...
    ##  $ num_of_doors     : chr  "two" ...
    ##  $ body_style       : chr  "convertible" ...
    ##  $ drive_wheels     : chr  "rwd" ...
    ##  $ engine_location  : chr  "front" ...
    ##  $ wheel_base       : num  88.6 94.5 ...
    ##  $ length           : num  169 ...
    ##  $ width            : num  64.1 65.5 ...
    ##  $ height           : num  48.8 52.4 ...
    ##  $ curb_weight      : int  2548 2823 ...
    ##  $ engine_type      : chr  "dohc" ...
    ##  $ num_of_cylinders : chr  "four" ...
    ##  $ engine_size      : int  130 152 ...
    ##  $ fuel_system      : chr  "mpfi" ...
    ##  $ bore             : num  3.47 2.68 ...
    ##  $ stroke           : num  2.68 3.47 ...
    ##  $ compression_ratio: num  9 9 ...
    ##  $ horsepower       : int  111 154 ...
    ##  $ peak_rpm         : int  5000 5000 ...
    ##  $ city_mpg         : int  21 19 ...
    ##  $ highway_mpg      : int  27 26 ...
    ##  $ price            : int  16500 16500 ...

-   

``` r
library(readr)
dat1 <- data.frame(
read_csv("./imports-85.data",
col_types = cols(symboling = col_double(),
normalized.losses = col_character(), 
make = col_character(), 
fuel_type = col_character(), 
aspiration = col_character(), 
num_of_doors = col_character(), 
body_style = col_character(), 
drive_wheel = col_character(), 
wheel_base = col_double(), 
length = col_double(), 
width = col_double(), 
height = col_double(), 
curb_weight = col_integer(), 
engine_type = col_character(), 
num_of_cylinders = col_character(), 
engine_size = col_integer(), 
fuel_system = col_character(), 
bore = col_double(), 
stroke = col_double(), 
compression_ratio = col_double(), 
horsepower = col_integer(), 
peak_rpm = col_integer(), 
city_mpg = col_integer(), 
highway_mpg = col_integer(), 
price = col_integer())  )
  )
```

    ## Warning: The following named parsers don't match the column names:
    ## symboling, normalized.losses, make, fuel_type, aspiration, num_of_doors,
    ## body_style, drive_wheel, wheel_base, length, width, height, curb_weight,
    ## engine_type, num_of_cylinders, engine_size, fuel_system, bore, stroke,
    ## compression_ratio, horsepower, peak_rpm, city_mpg, highway_mpg, price

``` r
str(dat1)
```

    ## 'data.frame':    432 obs. of  1 variable:
    ##  $ X..DOCTYPE.HTML.PUBLIC.....W3C..DTD.HTML.3.2.Final..EN..: chr  "<html>" "<head>" "<title>Index of /ml/machine-learning-databases</title>" "</head>" ...

3.Technical questions about importing data

1.  The column name of the import data will be its first line. Because if we use read.csv('import-85.data'), the 'header' will default as 'TRUE', which means the file contains the names of the variables as its first line.

2.  The column name of the import data will default as "V1","V2","V3",...,"Vn", where n is the number of columns.

3.  Error.

4.  The first option is smaller because it will assume all the data type is charactor and every column is a character vector (only one byte per character). However, if it with the specifying data type, the integer uses 4 bytes and real number uses 8 bytes. Then the second option will be bigger in storage.

5.  Then all the date type will be character, because it follows one of two rules - that is, if there is a character type vector in the columns, then other columns will turn into a character type vector as well.

4.Practice base plotting

-   

``` r
hist(dat$price, col = 'blue')
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-4-1.png) \*

``` r
boxplot(dat$horsepower, horizontal = TRUE)
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-5-1.png) \*

``` r
body_style1 <- table(dat$body_style)
barplot(sort(body_style1, decreasing = TRUE))
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-6-1.png) \*

``` r
asp_turbo <- subset(dat, dat$aspiration == 'turbo' )
stars(asp_turbo[,c('wheel_base','length','width','price')])
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-7-1.png)

1.  Summaries

<!-- -->

1.  

``` r
mean(subset(dat$price, dat$fuel_type == 'gas'), na.rm = TRUE)
```

    ## [1] 12913.19

``` r
mean(subset(dat$price, dat$fuel_type == 'diesel'))
```

    ## [1] 15838.15

``` r
?mean
```

1.  

``` r
subset(dat$make, dat$num_of_cylinders == 'twelve')
```

    ## [1] "jaguar"

1.  

``` r
names(which.max(table(dat$make[dat$fuel_type == 'diesel'])))[1]
```

    ## [1] "peugot"

1.  

``` r
subset(dat$price, dat$horsepower == max(dat$horsepower, na.rm = TRUE))
```

    ## [1] NA

1.  

``` r
dat$city_mpg[dat$city_mpg <= quantile(dat$city_mpg, prob = 0.1)]
```

    ##  [1] 17 16 16 16 15 15 15 13 17 17 17 16 16 16 14 14 17 17 17 17 17 17 17
    ## [24] 17 17

1.  

``` r
dat$highway_mpg[dat$highway_mpg >= quantile(dat$highway_mpg, prob = 0.9)]
```

    ##  [1] 53 43 43 41 38 38 38 38 54 38 42 43 43 38 38 38 38 42 39 41 38 38 50
    ## [24] 41 38 38 38 39 38 38 47 47 46 46 42 38

1.  

``` r
median(dat[dat$highway_mpg >= quantile(dat$highway_mpg, prob = 0.9), 'price'], na.rm = TRUE)
```

    ## [1] 6680.5

1.  Technical Questions about data frame

<!-- -->

1.  It will appear error and 'NULL'.

2.  4

3.  Because we need a string here, mpg is not a string but "mpg" is a string.

4.  YES. A data.frame is a list of vectors, each of the same length, and a list is a type of vector.

5.  It converts a data frame to a list and every column becomes the list's element, it also returns every column's name with its values included.

6.  data.frame(abc)

<!-- -->

1.  Correlations of quantitative variables

``` r
qdat <- na.omit(data.frame(dat$wheel_base,
dat$length,
dat$width,
dat$height,
dat$curb_weight,
dat$engine_size,
dat$bore,
dat$stroke,
dat$compression_ratio,
dat$horsepower,
dat$peak_rpm,
dat$city_mpg,
dat$highway_mpg,
dat$price
))

R <- cor(qdat)

library(corrplot)
```

    ## corrplot 0.84 loaded

``` r
corrplot(R, method = "circle", type = "upper", pch.col = "yellow")
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-15-1.png)

``` r
corrplot(R, method = "pie", type = "full", outline = TRUE)
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-15-2.png)

``` r
?corrplot
```

8.Principal Components Analysis

8.1) Run PCA

``` r
pca_prcomp <- prcomp(qdat, scale.= TRUE)
pca_prcomp
```

    ## Standard deviations:
    ##  [1] 2.7475837 1.5060881 1.1104814 0.9415972 0.7816626 0.6453100 0.5683069
    ##  [8] 0.5152131 0.3474131 0.3328790 0.2841045 0.2522710 0.2264319 0.1404923
    ## 
    ## Rotation:
    ##                               PC1         PC2         PC3         PC4
    ## dat.wheel_base         0.28960537 -0.28776469  0.12825722 -0.23652135
    ## dat.length             0.32825371 -0.16291817  0.12443745 -0.15341037
    ## dat.width              0.32385577 -0.12228603 -0.05224038 -0.09116177
    ## dat.height             0.11165134 -0.39825905  0.47877659 -0.38891269
    ## dat.curb_weight        0.35152561 -0.06225292 -0.05555184  0.00962865
    ## dat.engine_size        0.32148857  0.08138399 -0.24801695  0.18681666
    ## dat.bore               0.25933812 -0.00152011  0.15996983  0.39947230
    ## dat.stroke             0.05207944 -0.10140422 -0.70418366 -0.48551771
    ## dat.compression_ratio  0.01457865 -0.52209295 -0.28742497  0.15076971
    ## dat.horsepower         0.29746310  0.30329643 -0.13678214  0.09496034
    ## dat.peak_rpm          -0.08134054  0.45265347  0.06885913 -0.51906416
    ## dat.city_mpg          -0.30933538 -0.27073757 -0.11494937  0.09076060
    ## dat.highway_mpg       -0.31930591 -0.22045403 -0.11542402  0.09394433
    ## dat.price              0.31808522  0.07026628 -0.13208265  0.11144967
    ##                                PC5          PC6          PC7         PC8
    ## dat.wheel_base         0.039823148 -0.094851281  0.312791581 -0.28123376
    ## dat.length             0.008747757 -0.003515893  0.225237742 -0.01689368
    ## dat.width             -0.130898609 -0.126294675  0.465989060 -0.16466049
    ## dat.height             0.004869753  0.086377731 -0.604835396 -0.01364638
    ## dat.curb_weight       -0.057552930 -0.044574905  0.003667024  0.13267017
    ## dat.engine_size       -0.087151685 -0.175013044 -0.257485782 -0.25189551
    ## dat.bore               0.320745737  0.761356525  0.048055342 -0.21690921
    ## dat.stroke             0.428739000  0.193110176 -0.139062703 -0.03536755
    ## dat.compression_ratio -0.497584170  0.319335342  0.041394069  0.48025723
    ## dat.horsepower        -0.132731142  0.066034856 -0.239087112  0.05356797
    ## dat.peak_rpm          -0.488766446  0.441801245  0.129137113 -0.12743928
    ## dat.city_mpg          -0.156781350  0.032403884 -0.001816202 -0.45800063
    ## dat.highway_mpg       -0.142181473  0.061921052 -0.035248376 -0.47139543
    ## dat.price             -0.366988494 -0.107700500 -0.322023824 -0.28676496
    ##                               PC9        PC10         PC11        PC12
    ## dat.wheel_base         0.33133704 -0.40670774  0.323414463 -0.41475361
    ## dat.length             0.43201694  0.30321158 -0.639526649  0.20251002
    ## dat.width             -0.66937391  0.34869062  0.117355593  0.06323667
    ## dat.height            -0.18092287  0.15963483  0.108932518  0.05564054
    ## dat.curb_weight        0.18111238  0.06302285  0.178024108  0.19371022
    ## dat.engine_size        0.21100607 -0.01333982  0.340898924  0.56334113
    ## dat.bore              -0.09432189 -0.07139872  0.005714896  0.03892634
    ## dat.stroke            -0.07401280 -0.02238834 -0.078517768 -0.02658853
    ## dat.compression_ratio  0.03629040 -0.07698872  0.053373838 -0.01814615
    ## dat.horsepower         0.17729357  0.53456772  0.166529419 -0.59094530
    ## dat.peak_rpm           0.07470289 -0.06299820  0.086907351  0.17191680
    ## dat.city_mpg           0.09507528  0.14319387  0.153654290  0.02105384
    ## dat.highway_mpg        0.11825627  0.28788771 -0.156930608 -0.08238237
    ## dat.price             -0.26406147 -0.43219415 -0.469358290 -0.19090356
    ##                               PC13         PC14
    ## dat.wheel_base         0.114513668  0.092130534
    ## dat.length             0.140734004 -0.164908534
    ## dat.width              0.061960310  0.022879981
    ## dat.height             0.040229847  0.012236338
    ## dat.curb_weight       -0.853568596  0.109052120
    ## dat.engine_size        0.373520444  0.088596156
    ## dat.bore              -0.009873853 -0.005714601
    ## dat.stroke            -0.018543375 -0.022580685
    ## dat.compression_ratio  0.169093835  0.030351581
    ## dat.horsepower         0.089734610 -0.087140503
    ## dat.peak_rpm          -0.015222161  0.020783432
    ## dat.city_mpg          -0.183051668 -0.697896165
    ## dat.highway_mpg       -0.093991369  0.665339990
    ## dat.price             -0.117753083 -0.068386662

``` r
eigenvalues <- pca_prcomp$sdev^2
eigenvalues
```

    ##  [1] 7.54921592 2.26830130 1.23316897 0.88660537 0.61099636 0.41642495
    ##  [7] 0.32297279 0.26544451 0.12069583 0.11080841 0.08071539 0.06364068
    ## [13] 0.05127142 0.01973808

``` r
eigenvalues[1]/sum(eigenvalues)
```

    ## [1] 0.5392297

``` r
sum(eigenvalues[2])/sum(eigenvalues)
```

    ## [1] 0.1620215

``` r
sum(eigenvalues[3])/sum(eigenvalues)
```

    ## [1] 0.0880835

``` r
sum(eigenvalues[1:3])/sum(eigenvalues)
```

    ## [1] 0.7893347

8.2) PCA plot of vehicles, and PCA plot of variables

-   

``` r
t<-pca_prcomp$x
plot(t[,1:2])
abline(h=0, v=0)
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-17-1.png)

-   

``` r
rot<-pca_prcomp$rotation
plot(rot[,1],rot[,2])
abline(h=0, v=0)
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-18-1.png)

-   

``` r
biplot(pca_prcomp, scale = 0)
```

![](hw01-pinrui-yu_files/figure-markdown_github/unnamed-chunk-19-1.png)

-   If the arrow points to the similiar direction (angle less than 90), the correlation coefficient will be positive, otherwise, if angle ranges in 90-180, the correlation coefficient will be negative.
