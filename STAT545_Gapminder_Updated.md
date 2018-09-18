STAT545\_Gapminder\_Updated
================

Updated Gapminder Homework Assignment
-------------------------------------

**Note:** A previous file shows a data analysis I attempted using a dataset that I created myself. I misunderstood the homework instructions, so I am performing the correct data analysis here. In the original file [STAT545\_gapminder\_hw01](https://github.com/STAT545-UBC-students/hw01-JasmineLib/blob/master/STAT545_Gapminder_hw01.md) I performed a t-test on two of my own data sets, and studied the resulting p-values (I included links on how I learned to do this in the document), which may be useful to some of you reading this now!

### Explore the iris dataframe

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.1     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.7.2     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.2.0

    ## ── Conflicts ──────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
data(iris)
head(iris)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.1         3.5          1.4         0.2  setosa
    ## 2          4.9         3.0          1.4         0.2  setosa
    ## 3          4.7         3.2          1.3         0.2  setosa
    ## 4          4.6         3.1          1.5         0.2  setosa
    ## 5          5.0         3.6          1.4         0.2  setosa
    ## 6          5.4         3.9          1.7         0.4  setosa

``` r
ncol(iris)
```

    ## [1] 5

``` r
nrow(iris)
```

    ## [1] 150

``` r
summary(iris)
```

    ##   Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
    ##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
    ##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
    ##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
    ##  Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
    ##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
    ##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
    ##        Species  
    ##  setosa    :50  
    ##  versicolor:50  
    ##  virginica :50  
    ##                 
    ##                 
    ## 

There are 5 columns and 150 rows in this dataset.

### Explore variables in the iris dataframe.

1.  In particular, I want to observe the species in this dataframe.

``` r
iris$Species
```

    ##   [1] setosa     setosa     setosa     setosa     setosa     setosa    
    ##   [7] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [13] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [19] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [25] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [31] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [37] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [43] setosa     setosa     setosa     setosa     setosa     setosa    
    ##  [49] setosa     setosa     versicolor versicolor versicolor versicolor
    ##  [55] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [61] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [67] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [73] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [79] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [85] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [91] versicolor versicolor versicolor versicolor versicolor versicolor
    ##  [97] versicolor versicolor versicolor versicolor virginica  virginica 
    ## [103] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [109] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [115] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [121] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [127] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [133] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [139] virginica  virginica  virginica  virginica  virginica  virginica 
    ## [145] virginica  virginica  virginica  virginica  virginica  virginica 
    ## Levels: setosa versicolor virginica

I conclude there are 3 different species (by looking at the outpud "levels"): setosa, versicolor and virginica

1.  Compare sepal length (Sepal.Length) of setosa and versicolor species To do this, I used the [cm005 notes on piping](http://stat545.com/Classroom/notes/cm005.nb.html) as well as a tutorial on finding the [mean of a column in r](https://stackoverflow.com/questions/23163863/mean-of-a-column-in-a-data-frame-given-the-columns-name)

``` r
library(tidyverse)
setosa = iris %>% 

  filter(Species == "setosa") %>% 
  select(Sepal.Length)
  

versicolor = iris %>% 
  filter(Species == "versicolor") %>% 
  select(Sepal.Length)

# I can check the mean of the Sepal length for setosa and versicolor species using the mean function:
mean(setosa[["Sepal.Length"]])
```

    ## [1] 5.006

``` r
mean(versicolor[["Sepal.Length"]])
```

    ## [1] 5.936

1.  I can calculate the variance of the sepal length in the setosa species using the var function:

``` r
var(setosa)
```

    ##              Sepal.Length
    ## Sepal.Length     0.124249

1.  I can check this result manually, by calculating the variance. The equation for variance can be found [here](http://www.r-tutor.com/elementary-statistics/numerical-measures/variance)

breaking down the equation: 1. find the differences between each entry in setosa compared to the mean: (setosa*S**e**p**a**l*.*L**e**n**g**t**h* − 5.006)2.*T**a**k**e**t**h**e**s**q**u**a**r**e**o**f**r**e**s**u**l**t**i**n**g**v**e**c**t**o**r* : (*s**e**t**o**s**a*Sepal.Length - 5.006)^2 3. Take the sum of the squared vector: sum((setosa*S**e**p**a**l*.*L**e**n**g**t**h* − 5.006)<sup>2</sup>)4.*D**i**v**i**d**e**b**y**t**h**e**n**u**m**b**e**r**o**f**r**o**w**s**i**n**s**e**t**o**s**a* − 1*s**u**m*((*s**e**t**o**s**a*Sepal.Length - 5.006)^2)/(nrow(setosa)-1)

``` r
#overall, the equation comes to:
sum((setosa$Sepal.Length-5.006)^2)/(nrow(setosa)-1)
```

    ## [1] 0.124249

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

1.  Load tidyverse and explore the average life expectancy in 1952 in the continent with the most entries.

``` r
library(tidyverse)
gapminder %>% 
  select(continent, lifeExp, year) %>% 
  filter(year =="1952") %>% 
  summary() #this outputs the 5 continents, so I can ensure there are values in each one, and there are.
```

    ##     continent     lifeExp           year     
    ##  Africa  :52   Min.   :28.80   Min.   :1952  
    ##  Americas:25   1st Qu.:39.06   1st Qu.:1952  
    ##  Asia    :33   Median :45.14   Median :1952  
    ##  Europe  :30   Mean   :49.06   Mean   :1952  
    ##  Oceania : 2   3rd Qu.:59.77   3rd Qu.:1952  
    ##                Max.   :72.67   Max.   :1952

1.  From above, I can see that there are the most entries in the continent of Africa, so I will explore Asia's average life expectancy in 1952.

``` r
gapminder %>% 
  select(continent, lifeExp, year) %>% 
  filter(continent== "Asia" & year =="1952") %>% 
  summary()
```

    ##     continent     lifeExp           year     
    ##  Africa  : 0   Min.   :28.80   Min.   :1952  
    ##  Americas: 0   1st Qu.:39.42   1st Qu.:1952  
    ##  Asia    :33   Median :44.87   Median :1952  
    ##  Europe  : 0   Mean   :46.31   Mean   :1952  
    ##  Oceania : 0   3rd Qu.:50.94   3rd Qu.:1952  
    ##                Max.   :65.39   Max.   :1952

``` r
#using the summary function, I determine that the mean life expectancy in Africa in 1952 is 46.31 years. 
```
