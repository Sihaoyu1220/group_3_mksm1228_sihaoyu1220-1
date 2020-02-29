Milestone 1: Airbnb predictive pricing tool for tourists coming to
Canada
================

  - [Introduction](#introduction)
  - [Research Question](#research-question)
  - [Plan of Action](#plan-of-action)
  - [References](#references)

## Introduction

According to Statistics Canada, a recording breaking **22.1 million
international tourists from abroad visited Canada.** Hotels have always
been the mainstay of accommodations but often the prices are
unaffordable for visitors looking to stay long term for tourism or work.
Airbnb was founded in 2008 and has since been proven to be a successful
online platform to match hosts with unused space and guests looking for
an affordable place to lodge. Although it is often more affordable than
hotels, it appears that the market price varies greatly between Canadian
cities. In this analysis, we want to investigate which factors, ranging
from the location of the listing to the number of bathrooms, are most
likely influencing the price of Airbnb listings for cities in Canada.
This predicitive tool may potentially help visitors understand the
reasoning behind the cost of the listings and help them decide which
listings would best suit their travelling needs.

``` r
data$id<-as.factor(data$id)
nlevels(data$id) 
```

    ## [1] 6181

There are 6181 listings.

``` r
data$host_id<-as.factor(data$host_id)
nlevels(data$host_id) #4261 hosts.
```

    ## [1] 4261

There are 4261 hosts.

Select useful variables.

``` r
data <- data %>% 
  select(id, host_id, host_is_superhost, host_listings_count, neighbourhood_cleansed, property_type, room_type, accommodates, bathrooms, bedrooms, beds, price, weekly_price, monthly_price, security_deposit, cleaning_fee, guests_included, extra_people, minimum_nights, maximum_nights, review_scores_rating)
```

Some EDA.

``` r
barplot(table(data$room_type), main="Room Type Summary")
```

![](Milestone-1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
data$price <- as.numeric(gsub('[$,]', '', data$price))
plot(data$price, data$minimum_nights, main="Minimum Nights vs. Price", xlab="price", ylab="minimum nights")
```

![](Milestone-1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

# Research Question

In this analysis, we aim to investigate the influence of different
factors on the price of Airbnb listings across various Canadian cities.

# Plan of Action

We will first establish that the provided datasets by InsideAirbnb can
be utilized by thoroughly ensuring there is less than 5-10% of missing
data. Next, we will perform a linear regression analysis between the
price of the Airbnb listing and the various factors provided in the
datasets. Using these results, we also plan to perform a
cross-validation analysis to see if we can use this predictive model on
different cities.

# References

<https://www150.statcan.gc.ca/n1/daily-quotidien/200221/dq200221b-eng.htm?indid=3635-2&indgeo=0>