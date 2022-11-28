final test
================
Troy Zhou

## load state people wearing mask last 5 days

``` r
mask_5d <- read.csv("data/covidcast-fb-survey-smoothed_wwearing_mask-2021-01-01-to-2022-11-27.csv")

count_table<-mask_5d %>% group_by(geo_value) %>% 
  summarize(count=n()) %>% 
  knitr::kable(digits = 2)

# test_df<-mask_5d %>% nest_by(geo_value)
mask_5d[1:5,]
```

    ##   X geo_value                 signal time_value      issue lag    value
    ## 1 0        ak smoothed_wwearing_mask 2021-01-01 2021-01-06   5 86.06442
    ## 2 1        al smoothed_wwearing_mask 2021-01-01 2021-01-06   5 88.15571
    ## 3 2        ar smoothed_wwearing_mask 2021-01-01 2021-01-06   5 88.49071
    ## 4 3        az smoothed_wwearing_mask 2021-01-01 2021-01-06   5 91.30980
    ## 5 4        ca smoothed_wwearing_mask 2021-01-01 2021-01-06   5 95.18227
    ##      stderr sample_size geo_type data_source
    ## 1 1.2108704     818.000    state   fb-survey
    ## 2 0.4992502    4189.123    state   fb-survey
    ## 3 0.5797698    3029.946    state   fb-survey
    ## 4 0.3723170    5724.288    state   fb-survey
    ## 5 0.1328115   25997.249    state   fb-survey

- variable list
  `X, geo_value, signal, time_value, issue, lag, value, stderr, sample_size, geo_type, data_source`

- long format with state code and all dates

## load state people wearing mask last 5 days unweighted

``` r
mask_5d_unweighted <- read.csv("data/covidcast-fb-survey-smoothed_wearing_mask-2021-01-01-to-2022-11-27.csv")
```

- Sampling weights are non-negative values associated with survey
  responses that usually exist in any publicly available survey data.
  Sampling weights are supposed to be inversely proportional to the
  selection probabilities of sample units in the target population,
  whose main goal is to improve the representativeness of the sample
  with respect to a target population. Naive analyses of the data under
  a complex sample design are expected to result in biased estimates.
  For instance, unweighted inference based on CTIS data tends to
  overestimate vaccination rates among adult Facebook users. In the
  following section, we further explain why it is necessary to use the
  sampling weights in our statistical analysis

## load state people wearing mask last 7 days

``` r
mask_7d <- read.csv("data/covidcast-fb-survey-smoothed_wwearing_mask_7d-2021-01-01-to-2022-11-27.csv")
```

- maybe use 7 days data since corresponds with HHS data

## load flu 7 day hhs

``` r
flu_7d <- read.csv("data/covidcast-hhs-confirmed_admissions_influenza_1d_7dav-2021-01-01-to-2022-11-27.csv")

flu_7d[1:5,]
```

    ##   X geo_value                                 signal time_value      issue lag
    ## 1 0         1 confirmed_admissions_influenza_1d_7dav 2021-01-01 2021-10-28 300
    ## 2 1        10 confirmed_admissions_influenza_1d_7dav 2021-01-01 2021-10-28 300
    ## 3 2         2 confirmed_admissions_influenza_1d_7dav 2021-01-01 2021-10-28 300
    ## 4 3         3 confirmed_admissions_influenza_1d_7dav 2021-01-01 2021-10-28 300
    ## 5 4         4 confirmed_admissions_influenza_1d_7dav 2021-01-01 2021-10-28 300
    ##        value stderr sample_size geo_type data_source
    ## 1  1.8571429     NA          NA      hhs         hhs
    ## 2  0.8571429     NA          NA      hhs         hhs
    ## 3  5.8571429     NA          NA      hhs         hhs
    ## 4 12.2857143     NA          NA      hhs         hhs
    ## 5 27.7142857     NA          NA      hhs         hhs

- hhs geovalue; need reference

## load flu like syptoms 7 day weighted state level from delphi survey

``` r
flu_like_7d<-read.csv("data/covidcast-fb-survey-smoothed_wili-2021-01-01-to-2022-11-27.csv")

flu_like_7d[1:5,]
```

    ##   X geo_value        signal time_value      issue lag     value    stderr
    ## 1 0        ak smoothed_wili 2021-01-01 2021-01-06   5 0.7064144 0.2597328
    ## 2 1        al smoothed_wili 2021-01-01 2021-01-06   5 2.5123933 0.2369504
    ## 3 2        ar smoothed_wili 2021-01-01 2021-01-06   5 1.4005256 0.1741507
    ## 4 3        az smoothed_wili 2021-01-01 2021-01-06   5 1.6023790 0.1561577
    ## 5 4        ca smoothed_wili 2021-01-01 2021-01-06   5 1.5720634 0.0788880
    ##   sample_size geo_type data_source
    ## 1     964.000    state   fb-survey
    ## 2    5214.153    state   fb-survey
    ## 3    3725.021    state   fb-survey
    ## 4    6893.958    state   fb-survey
    ## 5   31788.335    state   fb-survey

- match mask rate geo values, same time interval
