# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data

1.Unzip and load the data.

```r
unzip("activity.zip")
dt <- read.csv("activity.csv", na.strings = "NA", stringsAsFactors = FALSE)
```

2.Process the data.

```r
dt[,2] <- as.Date(dt[,2])
```

## What is mean total number of steps taken per day?

1.Make a histogram of the total number of steps taken each day.

```r
dt1 <- dt[complete.cases(dt), ]
result1 <- data.frame(aggregate(dt1$steps, by = list(as.factor(dt1$date)), FUN=sum))
hist(result1[, 2], labels = TRUE, col = "steelblue", main = "Histogram of Total Steps Taken Each Day", 
     xlab = "Total Steps Taken Each Day")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

2.Calculate and report the mean and median total number of steps taken per day.

```r
mean(result1[, 2])
```

```
## [1] 10766
```

```r
median(result1[, 2])
```

```
## [1] 10765
```



* The mean total number of steps taken per day is 10766.
* The median total number of steps taken per day is 10765.

## What is the average daily activity pattern?

1.Make a time series plot of the 5-minute interval (x-axis) and the average number 
  of steps taken, averaged across all days (y-axis).

```r
library(plyr)
result2 <- ddply(dt1, .(interval), summarize, avg_steps = mean(steps))
plot(result2[,1],result2[,2],  type="l", main = "Average Number of Steps Taken Along 5-minute Interval",
     xlab = "5-Minute Interval", ylab = "Average Number of Steps Taken", col = "steelblue")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

2.Find which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps.

```r
result2[which.max(result2$avg_steps), 1]
```

```
## [1] 835
```



Interval 835 contains the maximum number of steps.

## Imputing missing values

1.Calculate and report the total number of missing values in the dataset.

```r
sum(!complete.cases(dt))
```

```
## [1] 2304
```



There are 2304 missing values in the dataset.

2.Devise a strategy for filling in all of the missing values in the dataset.













## Are there differences in activity patterns between weekdays and weekends?
