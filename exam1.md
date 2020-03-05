---
title: "Exam 1"
author: "Lilly Clark"
date: "03-06-20"
output: 
  html_document:
    keep_md: yes
---



## Packages


```r
library(tidyverse)
library(purrr)
library(dplyr)
library(lubridate)
library(stringr)
```

## Data


```r
tdf <- readRDS(file = "data/tdf_2019.rds")
```

## Task 1


```r
compile_stage <- function(n){
  stage_info <- data.frame(tdf[[n]]$stage) %>%
    select(description:single_event)
  
  people <- lapply(tdf[[n]]$stage$competitors, data.frame) %>%
    bind_rows() %>%
    mutate(description = (str_c("Stage ", n)))
  
  team_info <- lapply(tdf[[n]]$stage$teams, data.frame) %>%
    bind_rows() %>%
    rename(team.id = id)
  
  people_teams <- full_join(people, team_info, by = "team.id")
  
  whole_stage <- full_join(people_teams, stage_info, by = "description") 

  return (whole_stage)
}

messy_tdf <- lapply(1:21, compile_stage) %>%
  rbind_list()
```


```r
messy_tdf <- messy_tdf %>%
  select(stage = description, rider_name = name.x, rider_nat = nationality.x, team_name = team.name, team_nat = team.nationality, dep_city = departure_city, arr_city = arrival_city, classification, distance, start_date = scheduled, time = result.time, time_rank = result.time_ranking, sprint_pts = result.sprint, sprint_rank = result.sprint_ranking, climb_pts = result.climber, climb_rank = result.climber_ranking, young_rider_time = result.young_rider, young_rider_rank = result.young_rider_ranking)
```


```r
tdf_clean <- messy_tdf %>%
  mutate(stage = as.integer(str_extract(stage, "\\d.*")),
         distance = as.numeric(str_replace(distance, ",", ".")), 
         start_date = date(str_extract(start_date, "\\d{4}-\\d{2}-\\d{2}")),
         time_rank = as.integer(time_rank), 
         sprint_pts = as.numeric(sprint_pts),
         sprint_rank = as.integer(sprint_rank),
         climb_pts = as.numeric(climb_pts),
         climb_rank = as.integer(climb_rank),
         young_rider_rank = as.integer(young_rider_rank)
         )
```



```r
saveRDS(tdf_clean, "results/tdf_clean.rds")
```

## Task 2

### Part 1


```r
convert_seconds <- function(time) {
  
  time <- str_remove(time, "\\+")
  
  minutes <- as.numeric(str_extract(time, "\\d{2}"))
  
  seconds <- str_extract(time, ":\\d{2}\\.") %>%
    str_extract(., "\\d{2}") %>%
    as.numeric()
  
  milliseconds <- str_extract(time, "\\.\\d{2}") %>%
    str_extract(., "\\d{2}") %>%
    as.numeric()
  
  time_in_seconds <- 60 * minutes + seconds + milliseconds / 100
  
  return (time_in_seconds)
}

tdf_clean <- tdf_clean %>%
  mutate(time = convert_seconds(time),
         young_rider_time = convert_seconds(young_rider_time))
```


```r
winning_times <- tdf_clean %>%
filter(time_rank == 1) %>%
select(stage, time)

two <- c(stage = 2, time = NA)
nineteen <- c(stage = 19, time = NA)

winning_times <- rbind_list(winning_times, two, nineteen) %>%
  arrange(stage)

yr_winning_times <- tdf_clean %>%
filter(young_rider_rank == 1) %>%
select(stage, young_rider_time)

yr_two <- c(stage = 2, young_rider_time = NA)
yr_nineteen <- c(stage = 19, young_rider_time = NA)

yr_winning_times <- rbind_list(yr_winning_times, yr_two, yr_nineteen) %>%
  arrange(stage)
```


```r
make_time_absolute <- function(n){
  updated_stage_df <- tdf_clean %>%
    filter(stage == n) %>%
    mutate(time = case_when(
      time_rank == 1 ~ time,
      time_rank != 1 ~ winning_times[[n, 2]] + time,
      TRUE ~ time
    ))
  return (updated_stage_df)
}

tdf_clean <- lapply(1:21, make_time_absolute) %>%
  rbind_list()
```


```r
make_yr_time_absolute <- function(n){
  updated_stage_df <- tdf_clean %>%
    filter(stage == n) %>%
    mutate(young_rider_time = case_when(
      young_rider_rank == 1 ~ young_rider_time,
      young_rider_rank != 1 ~ yr_winning_times[[n, 2]] + young_rider_time,
      TRUE ~ young_rider_time
    ))
  return (updated_stage_df)
}

tdf_clean <- lapply(1:21, make_yr_time_absolute) %>%
  rbind_list()
```


```r
tdf_clean <- tdf_clean %>%
  mutate(time = round(seconds_to_period(time), 2),
         young_rider_time = round(seconds_to_period(young_rider_time), 2))
```

### Part 2


```r
mountains <- tdf_clean %>%
  select(stage, rider_name, climb_pts) %>%
  mutate(climb_pts = case_when(
    is.na(climb_pts) ~ 0,
    TRUE ~ climb_pts
  ),
  stage = str_c("stage_", stage))

mountains <- pivot_wider(mountains, id_cols = rider_name, names_from = stage, values_from = climb_pts)
```


```r
mountains <- mountains %>%
  mutate(total_climb_pts = select(., stage_1:stage_21) %>% 
           rowSums()) %>%
  arrange(desc(total_climb_pts)) %>%
  head(30)
```


```r
mountain_king <- mountains %>%
  mutate(rank = rank(-total_climb_pts, ties.method = "min"))
```


```r
mountain_king <- mountain_king[,c(1, 24, 2:23)]

mountain_king <- mountain_king %>%
  mutate(rank = as.numeric(rank))
```


```r
glimpse(mountain_king)
```

```
Observations: 30
Variables: 24
$ rider_name      <chr> "Bardet, Romain", "Bernal, Egan", "Wellens, Tim", "Ca…
$ rank            <dbl> 1, 2, 3, 4, 5, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16…
$ stage_1         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_2         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_3         <dbl> 0, 0, 7, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0,…
$ stage_4         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_5         <dbl> 0, 0, 10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
$ stage_6         <dbl> 0, 0, 26, 0, 0, 0, 0, 2, 0, 0, 0, 0, 8, 4, 1, 0, 30, …
$ stage_7         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_8         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 29, 0, 1, 0, 0, 0…
$ stage_9         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_10        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_11        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_12        <dbl> 0, 0, 11, 0, 0, 10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
$ stage_13        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_14        <dbl> 0, 16, 10, 0, 9, 0, 0, 40, 0, 24, 12, 20, 0, 4, 30, 0…
$ stage_15        <dbl> 18, 2, 0, 0, 3, 19, 1, 8, 5, 0, 6, 4, 0, 0, 0, 7, 0, …
$ stage_16        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ stage_17        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0,…
$ stage_18        <dbl> 68, 0, 10, 60, 0, 0, 56, 0, 40, 0, 0, 0, 0, 0, 0, 24,…
$ stage_19        <dbl> 0, 40, 0, 7, 7, 30, 0, 0, 0, 16, 0, 8, 0, 12, 0, 0, 0…
$ stage_20        <dbl> 0, 20, 0, 0, 40, 0, 0, 0, 0, 4, 24, 8, 0, 16, 0, 0, 0…
$ stage_21        <dbl> 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
$ total_climb_pts <dbl> 86, 78, 75, 67, 59, 59, 58, 50, 45, 44, 42, 40, 38, 3…
```

```r
mountain_king
```

```
# A tibble: 30 x 24
   rider_name  rank stage_1 stage_2 stage_3 stage_4 stage_5 stage_6 stage_7
   <chr>      <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
 1 Bardet, R…     1       0       0       0       0       0       0       0
 2 Bernal, E…     2       0       0       0       0       0       0       0
 3 Wellens, …     3       0       0       7       0      10      26       0
 4 Caruso, D…     4       0       0       0       0       0       0       0
 5 Nibali, V…     5       0       0       0       0       0       0       0
 6 Yates, Si…     5       0       0       0       0       0       0       0
 7 Quintana,…     7       0       0       1       0       0       0       0
 8 Pinot, Th…     8       0       0       0       0       0       2       0
 9 Lutsenko,…     9       0       0       0       0       0       0       0
10 Kruijswij…    10       0       0       0       0       0       0       0
# … with 20 more rows, and 15 more variables: stage_8 <dbl>, stage_9 <dbl>,
#   stage_10 <dbl>, stage_11 <dbl>, stage_12 <dbl>, stage_13 <dbl>,
#   stage_14 <dbl>, stage_15 <dbl>, stage_16 <dbl>, stage_17 <dbl>,
#   stage_18 <dbl>, stage_19 <dbl>, stage_20 <dbl>, stage_21 <dbl>,
#   total_climb_pts <dbl>
```

I decided to account for ties using the "minimum" method of function `rank()`, a technique commonly used in sports. As an example of how this works, if two competitors tie for 5th place, they will both receive rank 5, and the next competitor will receive rank 7, skipping over 6th place. This way, the ranks of competitors following ties are not unduly inflated, and competitors within tied groups are not arbitrarily or randomly assigned rankings.

## Task 3



## References 

Converting to decimal hours:
https://www.r-bloggers.com/using-dates-and-times-in-r/

deparse thang
https://stackoverflow.com/questions/14577412/how-to-convert-variable-object-name-into-string

row sums
https://stackoverflow.com/questions/29006056/efficiently-sum-across-multiple-columns-in-r

https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/rank
rank function
