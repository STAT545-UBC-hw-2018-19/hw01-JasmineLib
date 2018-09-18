STAT545\_Gapminder\_Updated
================

Updated Gapminder Homework Assignment
-------------------------------------

**Note:** A previous file shows a data analysis I attempted using a dataset that I created myself. I misunderstood the homework instructions, so I am performing the correct data analysis here. In the original file [STAT545\_gapminder\_hw01](https://github.com/STAT545-UBC-students/hw01-JasmineLib/blob/master/STAT545_Gapminder_hw01.md) I performed a t-test on two of my own data sets, and studied the resulting p-values (I included links on how I learned to do this in the document), which may be useful to some of you reading this now!

### Explore the iris dataframe

#### Part 1: Explore the dataframe itself

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

**Conclusion:** There are 5 columns and 150 rows in this dataset. We see from the head function that the dataframe contains information on length and width of petals and sepals of different iris species. The summary function gives information on the mean and quartile values of the overall length and widths of all irises.

### Explore variables in the iris dataframe.

#### Part 2: Explore the species and sepal length variables in the iris dataframe.

##### Look at what species are present:

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

##### Compare sepal length (Sepal.Length) of setosa and versicolor species

To do this, I used the [cm005 notes on piping](http://stat545.com/Classroom/notes/cm005.nb.html) as well as a tutorial on finding the [mean of a column in r](https://stackoverflow.com/questions/23163863/mean-of-a-column-in-a-data-frame-given-the-columns-name)

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

##### I can calculate the variance of the sepal length in the setosa species using the var function:

``` r
var(setosa)
```

    ##              Sepal.Length
    ## Sepal.Length     0.124249

##### I can check this result manually, by calculating the variance. The equation for variance can be found [here](http://www.r-tutor.com/elementary-statistics/numerical-measures/variance)

###### breaking down the equation:

1.  find the differences between each entry in setosa compared to the mean: (setosa$Sepal.Length - 5.006)
2.  Take the square of resulting vector: (setosa$Sepal.Length - 5.006)^2
3.  Take the sum of the squared vector: sum((setosa$Sepal.Length - 5.006)^2)
4.  Divide by the number of rows in setosa -1 sum((setosa$Sepal.Length - 5.006)^2)/(nrow(setosa)-1)

Overall, the equation becomes:

``` r
sum((setosa$Sepal.Length-5.006)^2)/(nrow(setosa)-1)
```

    ## [1] 0.124249

**6. Conclusion:The result is the same for both the manual variance calculation as well as the result from the var function!**
