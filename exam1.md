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

### Task 1


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

### Task 2

#### Part 1

Fix the time variables (time, young_rider_time) in your tidy data frame so each cyclist's stage time is given rather than just the winner's time and time back from the winner. For example, rather than "04:22.47", "+00:00.00", "+00:00.00", "+00:00.00", ... in stage 1, it should be changed to "04:22.47", "04:22.47", "04:22.47", "04:22.47", .... You may keep the result as type character or change it to a reasonable date/time data type.


```r
tdf_clean %>%
  filter(!is.na(young_rider_rank)) #seems to be an error, time is greater for rank 27 than 28 in stage 1
```

```
# A tibble: 501 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 2     1 Jansen Gr… Norway    Team Jum… Netherl… Brussels Brussels
 3     1 Van Aert,… Belgium   Team Jum… Netherl… Brussels Brussels
 4     1 Asgreen, … Denmark   Deceunin… Belgium  Brussels Brussels
 5     1 Bol, Cees  Netherla… Team Sun… Netherl… Brussels Brussels
 6     1 Garcia Co… Spain     Bahrain … Bahrain  Brussels Brussels
 7     1 Philipsen… Belgium   UAE Team… United … Brussels Brussels
 8     1 Mas Nicol… Spain     Deceunin… Belgium  Brussels Brussels
 9     1 Benoot, T… Belgium   Lotto So… Belgium  Brussels Brussels
10     1 Politt, N… Germany   Team Kat… Switzer… Brussels Brussels
# … with 491 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
```


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


compile_winners <- function(time_var, rank_var) {
  
  winning_times <- tdf_clean %>%
  filter(deparse(substitute(rank_var)) == 1) %>%
  select(stage, substitute(time_var))

  two <- c(stage = 2, deparse(substitute(time_var)) = NA)
  nineteen <- c(stage = 19, deparse(substitute(time_var)) = NA)

  winning_times <- rbind_list(winning_times, two, nineteen) %>%
    arrange(stage)
  
  return (winning_times)
}

compile_winners(tdf_clean$time, tdf_clean$time_rank)


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
tdf_clean <- tdf_clean %>%
  mutate(time = case_when(
    stage == 1 & time_rank == 1 ~ time,
    stage == 1 & time_rank != 1 ~ winning_times[[1, 2]] + time,
    stage == 2 & time_rank == 1 ~ time,
    stage == 2 & time_rank != 1 ~ winning_times[[2, 2]] + time,
    stage == 3 & time_rank == 1 ~ time,
    stage == 3 & time_rank != 1 ~ winning_times[[3, 2]] + time,
    stage == 4 & time_rank == 1 ~ time,
    stage == 4 & time_rank != 1 ~ winning_times[[4, 2]] + time,
    stage == 5 & time_rank == 1 ~ time,
    stage == 5 & time_rank != 1 ~ winning_times[[5, 2]] + time,
    stage == 6 & time_rank == 1 ~ time,
    stage == 6 & time_rank != 1 ~ winning_times[[6, 2]] + time,
    stage == 7 & time_rank == 1 ~ time,
    stage == 7 & time_rank != 1 ~ winning_times[[7, 2]] + time,
    stage == 8 & time_rank == 1 ~ time,
    stage == 8 & time_rank != 1 ~ winning_times[[8, 2]] + time,
    stage == 9 & time_rank == 1 ~ time,
    stage == 9 & time_rank != 1 ~ winning_times[[9, 2]] + time,
    stage == 10 & time_rank == 1 ~ time,
    stage == 10 & time_rank != 1 ~ winning_times[[10, 2]] + time,
    stage == 11 & time_rank == 1 ~ time,
    stage == 11 & time_rank != 1 ~ winning_times[[11, 2]] + time,
    stage == 12 & time_rank == 1 ~ time,
    stage == 12 & time_rank != 1 ~ winning_times[[12, 2]] + time,
    stage == 13 & time_rank == 1 ~ time,
    stage == 13 & time_rank != 1 ~ winning_times[[13, 2]] + time,
    stage == 14 & time_rank == 1 ~ time,
    stage == 14 & time_rank != 1 ~ winning_times[[14, 2]] + time,
    stage == 15 & time_rank == 1 ~ time,
    stage == 15 & time_rank != 1 ~ winning_times[[15, 2]] + time,
    stage == 16 & time_rank == 1 ~ time,
    stage == 16 & time_rank != 1 ~ winning_times[[16, 2]] + time,
    stage == 17 & time_rank == 1 ~ time,
    stage == 17 & time_rank != 1 ~ winning_times[[17, 2]] + time,
    stage == 18 & time_rank == 1 ~ time,
    stage == 18 & time_rank != 1 ~ winning_times[[18, 2]] + time,
    stage == 19 & time_rank == 1 ~ time,
    stage == 19 & time_rank != 1 ~ winning_times[[19, 2]] + time,
    stage == 20 & time_rank == 1 ~ time,
    stage == 20 & time_rank != 1 ~ winning_times[[20, 2]] + time,
    stage == 21 & time_rank == 1 ~ time,
    stage == 21 & time_rank != 1 ~ winning_times[[21, 2]] + time,
    TRUE ~ time
  ))

tdf_clean <- tdf_clean %>%
  mutate(young_rider_time = case_when(
    stage == 1 & young_rider_rank == 1 ~ young_rider_time,
    stage == 1 & young_rider_rank != 1 ~ yr_winning_times[[1, 2]] + young_rider_time,
    stage == 2 & young_rider_rank == 1 ~ young_rider_time,
    stage == 2 & young_rider_rank != 1 ~ yr_winning_times[[2, 2]] + young_rider_time,
    stage == 3 & young_rider_rank == 1 ~ young_rider_time,
    stage == 3 & young_rider_rank != 1 ~ yr_winning_times[[3, 2]] + young_rider_time,
    stage == 4 & young_rider_rank == 1 ~ young_rider_time,
    stage == 4 & young_rider_rank != 1 ~ yr_winning_times[[4, 2]] + young_rider_time,
    stage == 5 & young_rider_rank == 1 ~ young_rider_time,
    stage == 5 & young_rider_rank != 1 ~ yr_winning_times[[5, 2]] + young_rider_time,
    stage == 6 & young_rider_rank == 1 ~ young_rider_time,
    stage == 6 & young_rider_rank != 1 ~ yr_winning_times[[6, 2]] + young_rider_time,
    stage == 7 & young_rider_rank == 1 ~ young_rider_time,
    stage == 7 & young_rider_rank != 1 ~ yr_winning_times[[7, 2]] + young_rider_time,
    stage == 8 & young_rider_rank == 1 ~ young_rider_time,
    stage == 8 & young_rider_rank != 1 ~ yr_winning_times[[8, 2]] + young_rider_time,
    stage == 9 & young_rider_rank == 1 ~ young_rider_time,
    stage == 9 & young_rider_rank != 1 ~ yr_winning_times[[9, 2]] + young_rider_time,
    stage == 10 & young_rider_rank == 1 ~ young_rider_time,
    stage == 10 & young_rider_rank != 1 ~ yr_winning_times[[10, 2]] + young_rider_time,
    stage == 11 & young_rider_rank == 1 ~ young_rider_time,
    stage == 11 & young_rider_rank != 1 ~ yr_winning_times[[11, 2]] + young_rider_time,
    stage == 12 & young_rider_rank == 1 ~ young_rider_time,
    stage == 12 & young_rider_rank != 1 ~ yr_winning_times[[12, 2]] + young_rider_time,
    stage == 13 & young_rider_rank == 1 ~ young_rider_time,
    stage == 13 & young_rider_rank != 1 ~ yr_winning_times[[13, 2]] + young_rider_time,
    stage == 14 & young_rider_rank == 1 ~ young_rider_time,
    stage == 14 & young_rider_rank != 1 ~ yr_winning_times[[14, 2]] + young_rider_time,
    stage == 15 & young_rider_rank == 1 ~ young_rider_time,
    stage == 15 & young_rider_rank != 1 ~ yr_winning_times[[15, 2]] + young_rider_time,
    stage == 16 & young_rider_rank == 1 ~ young_rider_time,
    stage == 16 & young_rider_rank != 1 ~ yr_winning_times[[16, 2]] + young_rider_time,
    stage == 17 & young_rider_rank == 1 ~ young_rider_time,
    stage == 17 & young_rider_rank != 1 ~ yr_winning_times[[17, 2]] + young_rider_time,
    stage == 18 & young_rider_rank == 1 ~ young_rider_time,
    stage == 18 & young_rider_rank != 1 ~ yr_winning_times[[18, 2]] + young_rider_time,
    stage == 19 & young_rider_rank == 1 ~ young_rider_time,
    stage == 19 & young_rider_rank != 1 ~ yr_winning_times[[19, 2]] + young_rider_time,
    stage == 20 & young_rider_rank == 1 ~ young_rider_time,
    stage == 20 & young_rider_rank != 1 ~ yr_winning_times[[20, 2]] + young_rider_time,
    stage == 21 & young_rider_rank == 1 ~ young_rider_time,
    stage == 21 & young_rider_rank != 1 ~ yr_winning_times[[21, 2]] + young_rider_time,
    TRUE ~ young_rider_time
  ))
```


minutes_and_seconds <- function(time) {
  min <- time %/% 60
  sec <- time %% 60
  return (str_c(min, ":", sec))
  as.POSIXlt(., tz = "", format = "%M:%S\\.%S")
}


```r
tdf_clean <- tdf_clean %>%
  mutate(time = round(seconds_to_period(time), 2),
         young_rider_time = round(seconds_to_period(young_rider_time), 2))
```


### References 

Converting to decimal hours:
https://www.r-bloggers.com/using-dates-and-times-in-r/

deparse thang
https://stackoverflow.com/questions/14577412/how-to-convert-variable-object-name-into-string
