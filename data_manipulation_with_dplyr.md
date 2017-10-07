Data Manipulation with dplyr
================

Working with data using the [dplyr package](https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html).

### Load packages and the iris data set

``` r
library(dplyr); library(datasets)
data(iris)
```

### Glimpse at iris data

``` r
glimpse(iris)
```

    ## Observations: 150
    ## Variables: 5
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...
    ## $ Species      <fctr> setosa, setosa, setosa, setosa, setosa, setosa, ...

### filter()

Select rows based on logical criteria

``` r
filtered <- filter(iris, Sepal.Length > 5.1 | Sepal.Width > 3.5)
head(filtered, 10)
```

    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1           5.0         3.6          1.4         0.2  setosa
    ## 2           5.4         3.9          1.7         0.4  setosa
    ## 3           5.4         3.7          1.5         0.2  setosa
    ## 4           5.8         4.0          1.2         0.2  setosa
    ## 5           5.7         4.4          1.5         0.4  setosa
    ## 6           5.4         3.9          1.3         0.4  setosa
    ## 7           5.7         3.8          1.7         0.3  setosa
    ## 8           5.1         3.8          1.5         0.3  setosa
    ## 9           5.4         3.4          1.7         0.2  setosa
    ## 10          5.1         3.7          1.5         0.4  setosa
