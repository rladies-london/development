R Notebook - Data Viz - ggplot2
================

``` r
library(ggplot2)
```

``` r
ggplot(diamonds, aes(x=cut)) + geom_bar()
```

![](notebook_ggplot2_files/figure-markdown_github/2-1.png)

``` r
ggplot(diamonds, aes(price, depth)) + geom_point()
```

![](notebook_ggplot2_files/figure-markdown_github/3-1.png)
