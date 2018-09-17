STAT 545 Gapminder Homework
================

Goal: Compare average fluorescence intensity of two Mutant reporter proteins to that of Wildtype reporter
---------------------------------------------------------------------------------------------------------

### Create datasets:

Create three vectors containing values of fluorescence intensity values from independent experiments for two different mutants (m1 and m2) as well as the wildtype

``` r
fluor_m1 = c(55.74, 70.81, 36.74, 65.1, 57.22, 77.69, 53.58, 63.94, 50.8, 64.05, 45.09, 58.86)
fluor_m2 = c(43.37, 35.23, 67.87, 53.3, 63.4, 56.01, 66.81, 58.51, 67.98, 53.34, 66.42, 45.71)
fluor_wt = c(12.23, 10.72, 17.28, 16.55, 22.25, 15.81, 17.32, 12.8, 16.5, 14.71, 19.71, 17.86)
```

### Compute the mean of each dataset:

Compute the average of the values in each vector using the 'mean' function Note: to remove missing values, use na.rm (see ?mean in search.)

``` r
(mean_fluorm1 = mean(fluor_m1))
```

    ## [1] 58.30167

``` r
(mean_fluorm2 = mean(fluor_m2))
```

    ## [1] 56.49583

``` r
(mean_fluorwt = mean(fluor_wt))
```

    ## [1] 16.145

Conclusion: The means of the mutants appear to be different from that of the wildtype. Will perform a t-test using the t-test function in R.

### Perform a t-test

A useful link to find out what t-test to use: <https://researchbasics.education.uconn.edu/t-test/>

#### Compare fluorescence of mutant 1 to that of wildtype:

``` r
(fluor_m1wt_ttest = t.test(fluor_m1, fluor_wt))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  fluor_m1 and fluor_wt
    ## t = 12.575, df = 12.819, p-value = 1.391e-08
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  34.90385 49.40949
    ## sample estimates:
    ## mean of x mean of y 
    ##  58.30167  16.14500

I can now save and print the p-value from a t-test as a variable: Useful link for learning how to do this: <https://stackoverflow.com/questions/31205554/output-p-value-from-a-t-test-in-r>

``` r
(m1wt_ttest_pval = fluor_m1wt_ttest$p.value)
```

    ## [1] 1.391261e-08

``` r
(typeof(m1wt_ttest_pval))
```

    ## [1] "double"

Is the p-value below 0.05? Visually yes, but I can check this using an if/else statement Useful link for if-else statements: <https://stackoverflow.com/questions/25885358/if-else-if-else-statement-and-brackets>

``` r
if (m1wt_ttest_pval < 0.05) {
  print("Accept alternate hypothesis")
} else if (m1wt_ttest_pval >= 2) {
  print("Accept null hypothesis")
} else {
  print("Error")
}
```

    ## [1] "Accept alternate hypothesis"

Given these results, I accept the null hypothesis, and I conclude that the mean of M1 is significantly different from that of the wildtype.

Now I can repeat the analysis for mutant 2:

``` r
(fluor_m2wt_ttest = t.test(fluor_m2, fluor_wt))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  fluor_m2 and fluor_wt
    ## t = 12.421, df = 12.945, p-value = 1.447e-08
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  33.32947 47.37220
    ## sample estimates:
    ## mean of x mean of y 
    ##  56.49583  16.14500

``` r
(m2wt_ttest_pval = fluor_m2wt_ttest$p.value)
```

    ## [1] 1.4467e-08

``` r
if (m2wt_ttest_pval < 0.05) {
  print("Accept alternate hypothesis")
} else if (m2wt_ttest_pval >= 2) {
  print("Accept null hypothesis")
} else {
  print("Error")
}
```

    ## [1] "Accept alternate hypothesis"

Again, for the second mutant, we conclude that the mean is significantly different from that of the wildtype.
