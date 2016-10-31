R Notebook - Data Wrangling - dplyr
================

dplyr agenda
------------

--Basics
--select()
--filter()
--arrange()
--mutate()
--summarize()
--group\_by()

------------------------------------------------------------------------

### Prerequisites

``` r
library(dplyr)
library(ggplot2)
```

------------------------------------------------------------------------

### Basics

``` r
tibble <- tbl_df(diamonds) #Convert diamonds dataset into tbl_df
head(tibble) #View first 6 rows
```

    ## # A tibble: 6 × 10
    ##   carat       cut color clarity depth table price     x     y     z
    ##   <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1  0.23     Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
    ## 2  0.21   Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 3  0.23      Good     E     VS1  56.9    65   327  4.05  4.07  2.31
    ## 4  0.29   Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 5  0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 6  0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48

``` r
dim(tibble) #Check the dimensions of the dataset
```

    ## [1] 53940    10

------------------------------------------------------------------------

### select()

##### select a subset of columns, and in a specified order

``` r
select(tibble, color, cut)
```

    ## # A tibble: 53,940 × 2
    ##    color       cut
    ##    <ord>     <ord>
    ## 1      E     Ideal
    ## 2      E   Premium
    ## 3      E      Good
    ## 4      I   Premium
    ## 5      J      Good
    ## 6      J Very Good
    ## 7      I Very Good
    ## 8      H Very Good
    ## 9      E      Fair
    ## 10     H Very Good
    ## # ... with 53,930 more rows

##### select a subset of columns, and by specifying a sequence of columns by name

``` r
select(tibble, clarity:price)
```

    ## # A tibble: 53,940 × 4
    ##    clarity depth table price
    ##      <ord> <dbl> <dbl> <int>
    ## 1      SI2  61.5    55   326
    ## 2      SI1  59.8    61   326
    ## 3      VS1  56.9    65   327
    ## 4      VS2  62.4    58   334
    ## 5      SI2  63.3    58   335
    ## 6     VVS2  62.8    57   336
    ## 7     VVS1  62.3    57   336
    ## 8      SI1  61.9    55   337
    ## 9      VS2  65.1    61   337
    ## 10     VS1  59.4    61   338
    ## # ... with 53,930 more rows

##### select a subset of columns, and by specifying columns to omit from the full dataset

``` r
select(tibble, -carat) #Select all columns except the carat column
```

    ## # A tibble: 53,940 × 9
    ##          cut color clarity depth table price     x     y     z
    ##        <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1      Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
    ## 2    Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 3       Good     E     VS1  56.9    65   327  4.05  4.07  2.31
    ## 4    Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 5       Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 6  Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
    ## 7  Very Good     I    VVS1  62.3    57   336  3.95  3.98  2.47
    ## 8  Very Good     H     SI1  61.9    55   337  4.07  4.11  2.53
    ## 9       Fair     E     VS2  65.1    61   337  3.87  3.78  2.49
    ## 10 Very Good     H     VS1  59.4    61   338  4.00  4.05  2.39
    ## # ... with 53,930 more rows

``` r
select(tibble, -(carat:clarity)) #Select all columns except the named sequence of columns carat:clarity
```

    ## # A tibble: 53,940 × 6
    ##    depth table price     x     y     z
    ##    <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   61.5    55   326  3.95  3.98  2.43
    ## 2   59.8    61   326  3.89  3.84  2.31
    ## 3   56.9    65   327  4.05  4.07  2.31
    ## 4   62.4    58   334  4.20  4.23  2.63
    ## 5   63.3    58   335  4.34  4.35  2.75
    ## 6   62.8    57   336  3.94  3.96  2.48
    ## 7   62.3    57   336  3.95  3.98  2.47
    ## 8   61.9    55   337  4.07  4.11  2.53
    ## 9   65.1    61   337  3.87  3.78  2.49
    ## 10  59.4    61   338  4.00  4.05  2.39
    ## # ... with 53,930 more rows

------------------------------------------------------------------------

### filter()

##### filter dataset to return a subset of rows

``` r
filter(tibble, cut == "Premium") #Select rows representing only Premium cut diamonds
```

    ## # A tibble: 13,791 × 10
    ##    carat     cut color clarity depth table price     x     y     z
    ##    <dbl>   <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.21 Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 2   0.29 Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 3   0.22 Premium     F     SI1  60.4    61   342  3.88  3.84  2.33
    ## 4   0.20 Premium     E     SI2  60.2    62   345  3.79  3.75  2.27
    ## 5   0.32 Premium     E      I1  60.9    58   345  4.38  4.42  2.68
    ## 6   0.24 Premium     I     VS1  62.5    57   355  3.97  3.94  2.47
    ## 7   0.29 Premium     F     SI1  62.4    58   403  4.24  4.26  2.65
    ## 8   0.22 Premium     E     VS2  61.6    58   404  3.93  3.89  2.41
    ## 9   0.22 Premium     D     VS2  59.3    62   404  3.91  3.88  2.31
    ## 10  0.30 Premium     J     SI2  59.3    61   405  4.43  4.38  2.61
    ## # ... with 13,781 more rows

##### filter dataset to return subset of rows based on multiple conditions

``` r
filter(tibble, cut == "Premium", color == "D") #Select rows representing only diamonds of Premium cut AND D color classification 
```

    ## # A tibble: 1,603 × 10
    ##    carat     cut color clarity depth table price     x     y     z
    ##    <dbl>   <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.22 Premium     D     VS2  59.3    62   404  3.91  3.88  2.31
    ## 2   0.30 Premium     D     SI1  62.6    59   552  4.23  4.27  2.66
    ## 3   0.71 Premium     D     SI2  61.7    59  2768  5.71  5.67  3.51
    ## 4   0.71 Premium     D     VS2  62.5    60  2770  5.65  5.61  3.52
    ## 5   0.70 Premium     D     VS2  58.0    62  2773  5.87  5.78  3.38
    ## 6   0.72 Premium     D     SI1  62.7    59  2782  5.73  5.69  3.58
    ## 7   0.70 Premium     D     SI1  62.8    60  2782  5.68  5.66  3.56
    ## 8   0.72 Premium     D     SI2  62.0    60  2795  5.73  5.69  3.54
    ## 9   0.71 Premium     D     SI1  62.7    60  2797  5.67  5.71  3.57
    ## 10  0.71 Premium     D     SI1  61.3    58  2797  5.73  5.75  3.52
    ## # ... with 1,593 more rows

``` r
filter(tibble, carat > 1.0000, price < 5000) #Select rows representing only diamonds of carat over 1.0000 AND price less than 5000
```

    ## # A tibble: 3,756 × 10
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   1.17 Very Good     J      I1  60.2    61  2774  6.83  6.90  4.13
    ## 2   1.01   Premium     F      I1  61.8    60  2781  6.39  6.36  3.94
    ## 3   1.01      Fair     E      I1  64.5    58  2788  6.29  6.21  4.03
    ## 4   1.01   Premium     H     SI2  62.7    59  2788  6.31  6.22  3.93
    ## 5   1.05 Very Good     J     SI2  63.2    56  2789  6.49  6.45  4.09
    ## 6   1.05      Fair     J     SI2  65.8    59  2789  6.41  6.27  4.18
    ## 7   1.01      Fair     E     SI2  67.4    60  2797  6.19  6.05  4.13
    ## 8   1.04   Premium     G      I1  62.2    58  2801  6.46  6.41  4.00
    ## 9   1.20      Fair     F      I1  64.6    56  2809  6.73  6.66  4.33
    ## 10  1.02   Premium     G      I1  60.3    58  2815  6.55  6.50  3.94
    ## # ... with 3,746 more rows

``` r
filter(tibble, carat > 1.0000 | price < 5000) #Select rows representing only diamonds of carat over 1.0000 OR price less than 50000
```

    ## # A tibble: 52,959 × 10
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.23     Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
    ## 2   0.21   Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 3   0.23      Good     E     VS1  56.9    65   327  4.05  4.07  2.31
    ## 4   0.29   Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 5   0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 6   0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
    ## 7   0.24 Very Good     I    VVS1  62.3    57   336  3.95  3.98  2.47
    ## 8   0.26 Very Good     H     SI1  61.9    55   337  4.07  4.11  2.53
    ## 9   0.22      Fair     E     VS2  65.1    61   337  3.87  3.78  2.49
    ## 10  0.23 Very Good     H     VS1  59.4    61   338  4.00  4.05  2.39
    ## # ... with 52,949 more rows

##### filter dataset to return rows which with/out NA values

``` r
filter(tibble, is.na(cut)) #Select rows representing diamonds which have NA values for cut
```

    ## # A tibble: 0 × 10
    ## # ... with 10 variables: carat <dbl>, cut <ord>, color <ord>,
    ## #   clarity <ord>, depth <dbl>, table <dbl>, price <int>, x <dbl>,
    ## #   y <dbl>, z <dbl>

``` r
filter(tibble, !is.na(cut)) #Select rows representing diamonds which do NOT have NA values for cut
```

    ## # A tibble: 53,940 × 10
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.23     Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
    ## 2   0.21   Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 3   0.23      Good     E     VS1  56.9    65   327  4.05  4.07  2.31
    ## 4   0.29   Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 5   0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 6   0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
    ## 7   0.24 Very Good     I    VVS1  62.3    57   336  3.95  3.98  2.47
    ## 8   0.26 Very Good     H     SI1  61.9    55   337  4.07  4.11  2.53
    ## 9   0.22      Fair     E     VS2  65.1    61   337  3.87  3.78  2.49
    ## 10  0.23 Very Good     H     VS1  59.4    61   338  4.00  4.05  2.39
    ## # ... with 53,930 more rows

------------------------------------------------------------------------

### arrange()

##### arrange rows based on particular values of a variable

``` r
arrange(tibble, color) #Arrange rows based on their color classification, default order is  ascending 
```

    ## # A tibble: 53,940 × 10
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.23 Very Good     D     VS2  60.5    61   357  3.96  3.97  2.40
    ## 2   0.23 Very Good     D     VS1  61.9    58   402  3.92  3.96  2.44
    ## 3   0.26 Very Good     D     VS2  60.8    59   403  4.13  4.16  2.52
    ## 4   0.26      Good     D     VS2  65.2    56   403  3.99  4.02  2.61
    ## 5   0.26      Good     D     VS1  58.4    63   403  4.19  4.24  2.46
    ## 6   0.22   Premium     D     VS2  59.3    62   404  3.91  3.88  2.31
    ## 7   0.30   Premium     D     SI1  62.6    59   552  4.23  4.27  2.66
    ## 8   0.30     Ideal     D     SI1  62.5    57   552  4.29  4.32  2.69
    ## 9   0.30     Ideal     D     SI1  62.1    56   552  4.30  4.33  2.68
    ## 10  0.24 Very Good     D    VVS1  61.5    60   553  3.97  4.00  2.45
    ## # ... with 53,930 more rows

``` r
arrange(tibble, desc(color)) #Arrange rows based on their color classification, specifying in descending order
```

    ## # A tibble: 53,940 × 10
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 2   0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
    ## 3   0.30      Good     J     SI1  64.0    55   339  4.25  4.28  2.73
    ## 4   0.23     Ideal     J     VS1  62.8    56   340  3.93  3.90  2.46
    ## 5   0.31     Ideal     J     SI2  62.2    54   344  4.35  4.37  2.71
    ## 6   0.30      Good     J     SI1  63.4    54   351  4.23  4.29  2.70
    ## 7   0.30      Good     J     SI1  63.8    56   351  4.23  4.26  2.71
    ## 8   0.30 Very Good     J     SI1  62.7    59   351  4.21  4.27  2.66
    ## 9   0.31 Very Good     J     SI1  59.4    62   353  4.39  4.43  2.62
    ## 10  0.31 Very Good     J     SI1  58.1    62   353  4.44  4.47  2.59
    ## # ... with 53,930 more rows

``` r
arrange(tibble, desc(color), desc(carat)) #Arrange rows based first on their color classification, specifying in descending order, and then within the same color classification, ordered by their carat value, specifying in descending order
```

    ## # A tibble: 53,940 × 10
    ##    carat     cut color clarity depth table price     x     y     z
    ##    <dbl>   <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   5.01    Fair     J      I1  65.5    59 18018 10.74 10.54  6.98
    ## 2   4.50    Fair     J      I1  65.8    58 18531 10.23 10.16  6.72
    ## 3   4.01 Premium     J      I1  62.5    62 15223 10.02  9.94  6.24
    ## 4   3.51 Premium     J     VS2  62.5    59 18701  9.66  9.63  6.03
    ## 5   3.11    Fair     J      I1  65.9    57  9823  9.15  9.02  5.98
    ## 6   3.01   Ideal     J     SI2  61.7    58 16037  9.25  9.20  5.69
    ## 7   3.01   Ideal     J      I1  65.4    60 16538  8.99  8.93  5.86
    ## 8   3.01 Premium     J     SI2  60.7    59 18710  9.35  9.22  5.64
    ## 9   3.01 Premium     J     SI2  59.7    58 18710  9.41  9.32  5.59
    ## 10  3.00    Good     J     SI2  59.3    64 14918  9.32  9.19  5.50
    ## # ... with 53,930 more rows

------------------------------------------------------------------------

### mutate()

##### creates & adds new variables

``` r
mutate(tibble, euro_price = price*0.9) #Create new variable euro_price based on existing price variable
```

    ## # A tibble: 53,940 × 11
    ##    carat       cut color clarity depth table price     x     y     z
    ##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1   0.23     Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
    ## 2   0.21   Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
    ## 3   0.23      Good     E     VS1  56.9    65   327  4.05  4.07  2.31
    ## 4   0.29   Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
    ## 5   0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
    ## 6   0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
    ## 7   0.24 Very Good     I    VVS1  62.3    57   336  3.95  3.98  2.47
    ## 8   0.26 Very Good     H     SI1  61.9    55   337  4.07  4.11  2.53
    ## 9   0.22      Fair     E     VS2  65.1    61   337  3.87  3.78  2.49
    ## 10  0.23 Very Good     H     VS1  59.4    61   338  4.00  4.05  2.39
    ## # ... with 53,930 more rows, and 1 more variables: euro_price <dbl>

------------------------------------------------------------------------

### summarize()

###### collapse the dataset into a single row

``` r
summarize(tibble, mean(carat)) #Summarizes mean statistic for carat variable
```

    ## # A tibble: 1 × 1
    ##   `mean(carat)`
    ##           <dbl>
    ## 1     0.7979397

------------------------------------------------------------------------

### group\_by()

##### group dataset by some ^attribute, and then summarize

``` r
grouped <- group_by(tibble, cut) #Group dataset by cut classification and assign to object
summarize(grouped, count = n(), average_price = mean(price)) #Compute a count and average_price value for each cut classification, using the grouped data
```

    ## # A tibble: 5 × 3
    ##         cut count average_price
    ##       <ord> <int>         <dbl>
    ## 1      Fair  1610      4358.758
    ## 2      Good  4906      3928.864
    ## 3 Very Good 12082      3981.760
    ## 4   Premium 13791      4584.258
    ## 5     Ideal 21551      3457.542

``` r
summarize(grouped, no_unique_prices = n_distinct(price)) #Compute the no. of unique prices for each cut classification, using the grouped data
```

    ## # A tibble: 5 × 2
    ##         cut no_unique_prices
    ##       <ord>            <int>
    ## 1      Fair             1267
    ## 2      Good             3086
    ## 3 Very Good             5840
    ## 4   Premium             6014
    ## 5     Ideal             7281
