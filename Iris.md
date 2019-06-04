Iris
================
Zen
June 3, 2019

``` r
library(readr)
```

    ## Warning: package 'readr' was built under R version 3.5.2

``` r
#IrisDataSet <- read.csv(iris.csv)

# attributes(iris)
# summary(iris)
# str(iris)
# names(iris)
# hist(iris$Sepal.Length)
# plot(iris$Sepal.Width, iris$Petal.Width)
# plot(iris$Sepal.Length, iris$Petal.Length)
# qqnorm(iris$Petal.Length)
# qqnorm(iris$Sepal.Length)
# 

iris$Species = factor(iris$Species,
                      levels = c('setosa', 'versicolor', 'virginica'),
                      labels = c(1, 2, 3))

set.seed(123)
trainSize <- round(nrow(iris) * 0.8)
testSize <- nrow(iris)-trainSize

trainSize
```

    ## [1] 120

``` r
testSize
```

    ## [1] 30

``` r
training_indices <- sample(seq_len(nrow(iris)), size = trainSize)
trainSet <- iris[training_indices,]
testSet <- iris[-training_indices,]

lmfit1 <- lm(`Petal.Length` ~ `Petal.Width`, trainSet)
summary(lmfit1)
```

    ## 
    ## Call:
    ## lm(formula = Petal.Length ~ Petal.Width, data = trainSet)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.39883 -0.32153 -0.00922  0.30938  1.36918 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  1.05562    0.08445   12.50   <2e-16 ***
    ## Petal.Width  2.26800    0.06136   36.96   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5004 on 118 degrees of freedom
    ## Multiple R-squared:  0.9205, Adjusted R-squared:  0.9198 
    ## F-statistic:  1366 on 1 and 118 DF,  p-value: < 2.2e-16

``` r
plot (lmfit1)
```

![](Iris_files/figure-markdown_github/unnamed-chunk-1-1.png)![](Iris_files/figure-markdown_github/unnamed-chunk-1-2.png)![](Iris_files/figure-markdown_github/unnamed-chunk-1-3.png)![](Iris_files/figure-markdown_github/unnamed-chunk-1-4.png)

``` r
TestPetal <- predict(lmfit1, testSet)

showmeName = (testSet$Species)
showmePetalLength = (testSet$Petal.Length)
showmePetalWidth = (testSet$Petal.Width)

showmeName
```

    ##  [1] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3 3 3 3 3 3 3
    ## Levels: 1 2 3

``` r
showmePetalLength
```

    ##  [1] 1.4 1.5 1.5 1.7 1.5 1.6 1.3 1.5 4.5 3.3 4.6 4.2 4.4 4.4 4.2 4.3 3.0
    ## [18] 5.1 5.9 5.8 4.5 5.8 6.1 5.7 5.6 5.6 6.1 5.4 5.6 5.9

``` r
showmePetalWidth
```

    ##  [1] 0.2 0.2 0.1 0.2 0.4 0.2 0.3 0.2 1.5 1.0 1.3 1.5 1.4 1.2 1.2 1.3 1.1
    ## [18] 1.9 2.1 2.2 1.7 1.8 2.5 2.1 2.1 2.2 2.3 2.1 2.4 2.3

``` r
TestPetal
```

    ##        2        4       10       21       22       31       42       49 
    ## 1.509220 1.509220 1.282420 1.509220 1.962821 1.509220 1.736021 1.509220 
    ##       52       58       59       62       76       91       96       98 
    ## 4.457624 3.323623 4.004024 4.457624 4.230824 3.777223 3.777223 4.004024 
    ##       99      102      103      105      107      109      110      125 
    ## 3.550423 5.364826 5.818426 6.045226 4.911225 5.138025 6.725627 5.818426 
    ##      129      133      136      140      141      144 
    ## 5.818426 6.045226 6.272027 5.818426 6.498827 6.272027

``` r
plot (TestPetal)
```

![](Iris_files/figure-markdown_github/unnamed-chunk-1-5.png)

``` r
summary (TestPetal)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   1.282   2.303   4.344   4.155   5.818   6.726

``` r
iris$ratio <- iris$Sepal.Length / iris$Sepal.Width

range (iris$ratio)
```

    ## [1] 1.268293 2.961538

R Markdown
----------

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

Including Plots
---------------

You can also embed plots, for example:

![](Iris_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
