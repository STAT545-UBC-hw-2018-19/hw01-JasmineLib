STAT545\_Gapminder\_Updated
================

Updated Gapminder Homework Assignment
-------------------------------------

**Note:** A previous file shows a data analysis I attempted using a dataset that I created myself. I misunderstood the homework instructions, so I am performing the correct data analysis here. In the original file [STAT545\_gapminder\_hw01](https://github.com/STAT545-UBC-students/hw01-JasmineLib/blob/master/STAT545_Gapminder_hw01.md) I performed a t-test on two of my data sets, and studied the resulting p-values (with links on how I learned to do this), which may be useful to some of you reading this now!

1.  Load the gapminder package and explore the data inside it using the head() function

``` r
library(gapminder)
head(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fctr>      <fctr>    <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333       779
    ## 2 Afghanistan Asia       1957    30.3  9240934       821
    ## 3 Afghanistan Asia       1962    32.0 10267083       853
    ## 4 Afghanistan Asia       1967    34.0 11537966       836
    ## 5 Afghanistan Asia       1972    36.1 13079460       740
    ## 6 Afghanistan Asia       1977    38.4 14880372       786

1.
