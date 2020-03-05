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

#### Part 2


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

rank <- c(1:30)

mountain_king <- cbind(mountains, rank)
mountain_king <- mountain_king[,c(1, 24, 2:23)]
```


```r
mountain_king %>%
  mutate(rank = as.numeric(rank))
```

```
            rider_name rank stage_1 stage_2 stage_3 stage_4 stage_5 stage_6
1       Bardet, Romain    1       0       0       0       0       0       0
2         Bernal, Egan    2       0       0       0       0       0       0
3         Wellens, Tim    3       0       0       7       0      10      26
4      Caruso, Damiano    4       0       0       0       0       0       0
5     Nibali, Vincenzo    5       0       0       0       0       0       0
6         Yates, Simon    6       0       0       0       0       0       0
7      Quintana, Nairo    7       0       0       1       0       0       0
8       Pinot, Thibaut    8       0       0       0       0       0       2
9     Lutsenko, Alexey    9       0       0       0       0       0       0
10  Kruijswijk, Steven   10       0       0       0       0       0       0
11  Landa Meana, Mikel   11       0       0       0       0       0       0
12   Buchmann, Emanuel   12       0       0       0       0       0       0
13    De Gendt, Thomas   13       0       0       0       0       0       8
14     Thomas, Geraint   14       0       0       0       0       0       4
15 Alaphilippe, Julian   15       0       0       1       0       0       1
16      Woods, Michael   16       0       0       0       0       0       0
17     Ciccone, Giulio   17       0       0       0       0       0      30
18 Valverde, Alejandro   18       0       0       0       0       0       0
19       Benoot, Tiesj   19       0       0       0       0       0       0
20    Meurisse, Xandro   20       2       0       1       0       3      21
21     Bernard, Julien   21       0       0       0       0       0       2
22     Barguil, Warren   22       0       0       0       0       0       0
23      Kamna, Lennard   23       0       0       0       0       1       0
24         Yates, Adam   24       0       0       0       0       0       0
25     Uran, Rigoberto   25       0       0       0       0       0       0
26    de Plus, Laurens   26       0       0       0       0       0       0
27    Berhane, Natnael   27       0       0       0       0       0      13
28      Geschke, Simon   28       0       0       0       0       0       0
29      Pauwels, Serge   29       0       0       0       0       0       1
30        Teuns, Dylan   30       0       0       0       0       0      13
   stage_7 stage_8 stage_9 stage_10 stage_11 stage_12 stage_13 stage_14
1        0       0       0        0        0        0        0        0
2        0       0       0        0        0        0        0       16
3        0       0       0        0        0       11        0       10
4        0       0       0        0        0        0        0        0
5        0       0       0        0        0        0        0        9
6        0       0       0        0        0       10        0        0
7        0       0       0        0        0        0        0        0
8        0       0       0        0        0        0        0       40
9        0       0       0        0        0        0        0        0
10       0       0       0        0        0        0        0       24
11       0       0       0        0        0        0        0       12
12       0       0       0        0        0        0        0       20
13       0      29       0        0        0        0        0        0
14       0       0       0        0        0        0        0        4
15       0       1       0        0        0        0        0       30
16       0       0       0        0        0        0        0        0
17       0       0       0        0        0        0        0        0
18       0       0       0        0        0        0        0        0
19       0       0      12        0        0        4        0        0
20       0       0       0        0        0        0        0        0
21       0       0       0        0        0        0        0        0
22       0       0       0        0        0        0        0        0
23       0       0       0        0        0        0        0        0
24       0       0       0        0        0        0        0        0
25       0       0       0        0        0        0        0        8
26       0       0       0        0        0        0        0        0
27       0       0       0        7        0        0        0        0
28       0       0       0        0        0        0        0        0
29       0       0       0        0        0       12        0        0
30       0       0       0        0        0        0        0        0
   stage_15 stage_16 stage_17 stage_18 stage_19 stage_20 stage_21
1        18        0        0       68        0        0        0
2         2        0        0        0       40       20        0
3         0        0        0       10        0        0        1
4         0        0        0       60        7        0        0
5         3        0        0        0        7       40        0
6        19        0        0        0       30        0        0
7         1        0        0       56        0        0        0
8         8        0        0        0        0        0        0
9         5        0        0       40        0        0        0
10        0        0        0        0       16        4        0
11        6        0        0        0        0       24        0
12        4        0        0        0        8        8        0
13        0        0        1        0        0        0        0
14        0        0        0        0       12       16        0
15        0        0        0        0        0        0        0
16        7        0        0       24        0        0        0
17        0        0        0        0        0        0        0
18        0        0        0        0        0       30        0
19        0        0        0       12        0        0        0
20        0        0        0        0        0        0        0
21        0        0        0       24        0        0        0
22        0        0        0        0       24        0        0
23        1        0        0       20        0        0        0
24        0        0        0       20        0        0        0
25        0        0        0        0        0       12        0
26        0        0        0        0       20        0        0
27        0        0        0        0        0        0        0
28       18        0        0        0        0        0        0
29        0        0        0        4        0        0        0
30        0        0        0        0        0        0        0
   total_climb_pts
1               86
2               78
3               75
4               67
5               59
6               59
7               58
8               50
9               45
10              44
11              42
12              40
13              38
14              36
15              33
16              31
17              30
18              30
19              28
20              27
21              26
22              24
23              22
24              20
25              20
26              20
27              20
28              18
29              17
30              13
```

 Only include the top 30 climbers sorted by total_climb_points in your final data frame. You may decide how to account for ties. Explain your choice.

### References 

Converting to decimal hours:
https://www.r-bloggers.com/using-dates-and-times-in-r/

deparse thang
https://stackoverflow.com/questions/14577412/how-to-convert-variable-object-name-into-string

row sums
https://stackoverflow.com/questions/29006056/efficiently-sum-across-multiple-columns-in-r

