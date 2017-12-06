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

### select()

``` r
sepal_measurments <- select(iris, Sepal.Length, Sepal.Width)
glimpse(sepal_measurments)
```

    ## Observations: 150
    ## Variables: 2
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...

#### select() with built-in filters

``` r
petal_measurements <- select(iris, starts_with("Petal"))
glimpse(petal_measurements)
```

    ## Observations: 150
    ## Variables: 2
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...

Other built-in column filters:
1. `starts_with("X")`: every name that starts with "X"
2. `ends_with("X")`: every name that ends with "X"
3. `contains("X")`: every name that contains "X"
4. `matches("X")`: every name that matches "X", where "X" can be a regular expression
5. `num_range("x", 1:5)`: the variables named x01, x02, x03, x04 and x05
6. `one_of(x)`: every name that appears in x, which should be a character vector.

### mutate()

Add new columns based on existing

``` r
df <- mutate(iris, Petal.Sum = Petal.Length + Petal.Width)
glimpse(df)
```

    ## Observations: 150
    ## Variables: 6
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...
    ## $ Species      <fctr> setosa, setosa, setosa, setosa, setosa, setosa, ...
    ## $ Petal.Sum    <dbl> 1.6, 1.6, 1.5, 1.7, 1.6, 2.1, 1.7, 1.7, 1.6, 1.6,...

You can create more than one new column, even using newly created columns:

``` r
df <- mutate(iris, Sepal.Sum = Sepal.Length + Sepal.Width, Petal.Sum = Petal.Length + Petal.Width, Mean.Sum = (Sepal.Sum + Petal.Sum)/2)
glimpse(df)
```

    ## Observations: 150
    ## Variables: 8
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...
    ## $ Species      <fctr> setosa, setosa, setosa, setosa, setosa, setosa, ...
    ## $ Sepal.Sum    <dbl> 8.6, 7.9, 7.9, 7.7, 8.6, 9.3, 8.0, 8.4, 7.3, 8.0,...
    ## $ Petal.Sum    <dbl> 1.6, 1.6, 1.5, 1.7, 1.6, 2.1, 1.7, 1.7, 1.6, 1.6,...
    ## $ Mean.Sum     <dbl> 5.10, 4.75, 4.70, 4.70, 5.10, 5.70, 4.85, 5.05, 4...

### filter()

Select rows based on logical criteria

``` r
filtered <- filter(iris, Sepal.Length > 5.1 | Sepal.Width > 3.5)
glimpse(filtered)
```

    ## Observations: 116
    ## Variables: 5
    ## $ Sepal.Length <dbl> 5.0, 5.4, 5.4, 5.8, 5.7, 5.4, 5.7, 5.1, 5.4, 5.1,...
    ## $ Sepal.Width  <dbl> 3.6, 3.9, 3.7, 4.0, 4.4, 3.9, 3.8, 3.8, 3.4, 3.7,...
    ## $ Petal.Length <dbl> 1.4, 1.7, 1.5, 1.2, 1.5, 1.3, 1.7, 1.5, 1.7, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.4, 0.2, 0.2, 0.4, 0.4, 0.3, 0.3, 0.2, 0.4,...
    ## $ Species      <fctr> setosa, setosa, setosa, setosa, setosa, setosa, ...

The usual logical operators are available inside `filter()`:

-   `x < y`
-   `x <= y`
-   `x == y`
-   `x != y`
-   `x >= y`
-   `x > y`
-   `x %in% c(a, b, c)` ,TRUE if `x` is in the vector `c(a, b, c)`
-   `is.na()`

Similarly, the usual boolean operators work inside filter():
\* `&` (and)
\* `|` (or)
\* `!` (not)

Note `&` can be replaced by commas. The following are equivalent:
`filter(df, a > 0 & b > 0)`
`filter(df, a > 0, b > 0)`

### summarise()

Apply functions to columns of a dataframe.

``` r
summarise(iris, mean_petal_length = mean(Petal.Length), sd_petal_length = sd(Petal.Length))
```

    ##   mean_petal_length sd_petal_length
    ## 1             3.758        1.765298

### arrange()

Sorts a dataframe on one or more column, by defualt in ascending order. To sort from highest to lowest, wrap the variable of interest in `desc()`.

``` r
sorted <- arrange(iris, desc(Sepal.Length))
head(sorted)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
    ## 1          7.9         3.8          6.4         2.0 virginica
    ## 2          7.7         3.8          6.7         2.2 virginica
    ## 3          7.7         2.6          6.9         2.3 virginica
    ## 4          7.7         2.8          6.7         2.0 virginica
    ## 5          7.7         3.0          6.1         2.3 virginica
    ## 6          7.6         3.0          6.6         2.1 virginica

Break ties with a second variable:

``` r
sorted2 <- arrange(iris, desc(Sepal.Length), desc(Petal.Width))
head(sorted2)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
    ## 1          7.9         3.8          6.4         2.0 virginica
    ## 2          7.7         2.6          6.9         2.3 virginica
    ## 3          7.7         3.0          6.1         2.3 virginica
    ## 4          7.7         3.8          6.7         2.2 virginica
    ## 5          7.7         2.8          6.7         2.0 virginica
    ## 6          7.6         3.0          6.6         2.1 virginica

### Pipe Operator

The pipe operator, `%>%` enables the chaining together of functions by supplying the output of one function as the first argument to another. It makes code more intuitive to both read and write.

``` r
iris %>%
  filter(Sepal.Length > 7) %>%
  mutate(Approx.Petal.Area = Petal.Length * Petal.Width) %>%
  summarise(mean = mean(Approx.Petal.Area),
            sd = sd(Approx.Petal.Area), 
            max = max(Approx.Petal.Area),
            min = min(Approx.Petal.Area))
```

    ##       mean       sd   max  min
    ## 1 12.94583 1.956028 15.87 9.28
