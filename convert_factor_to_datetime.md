Convert factor to datetime object
================

Use `as.POSIXct()` with your data's strptime format and timezone

``` r
times <- factor(c('2007-10-16 10:00:00', '2007-10-16 21:00:00', '2007-10-16 17:00:00'))
str(times)
```

    ##  Factor w/ 3 levels "2007-10-16 10:00:00",..: 1 3 2

``` r
times_dt <- as.POSIXct(times, format="%Y-%m-%d %H:%M", tz="GMT")
str(times_dt)
```

    ##  POSIXct[1:3], format: "2007-10-16 10:00:00" "2007-10-16 21:00:00" ...
