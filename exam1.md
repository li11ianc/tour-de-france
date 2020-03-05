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
  select(stage = description, rider_name = name.x, rider_nat = nationality.x, team_name = team.name, team_nat = team.nationality, dep_city = departure_city, arr_city = arrival_city, classification, distance, start_date = scheduled, time = result.time, time_rank = result.time_ranking, team_time = result.team_time, team_rank = result.team_time_ranking, sprint_pts = result.sprint, sprint_rank = result.sprint_ranking, climb_pts = result.climber, climb_rank = result.climber_ranking, young_rider_time = result.young_rider, young_rider_rank = result.young_rider_ranking, dns, dnf, dsq)
#keeping dns dnf dsq for now
```


```r
messy_tdf <- messy_tdf %>%
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

tdf_clean <- messy_tdf %>%
  select(-team_time, -team_rank, -dns, -dnf, -dsq)
```

-dns, -dnf, -dsq,


```r
tdf_clean
```

```
# A tibble: 3,696 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Teunissen… Netherla… Team Jum… Netherl… Brussels Brussels
 2     1 Sagan, Pe… Slovakia  Bora - H… Germany  Brussels Brussels
 3     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 4     1 Nizzolo, … Italy     Team Dim… South A… Brussels Brussels
 5     1 Colbrelli… Italy     Bahrain … Bahrain  Brussels Brussels
 6     1 Matthews,… Australia Team Sun… Netherl… Brussels Brussels
 7     1 Trentin, … Italy     Mitchelt… Austral… Brussels Brussels
 8     1 Naesen, O… Belgium   Ag2r La … France   Brussels Brussels
 9     1 Viviani, … Italy     Deceunin… Belgium  Brussels Brussels
10     1 Stuyven, … Belgium   Trek–Seg… USA      Brussels Brussels
# … with 3,686 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
```


```r
# NEED TO FINISH THIS, STOPPED AT time, didnt look at anything past that
names <- tdf_clean %>%
  filter(is.na(time), stage != 2, stage != 19) %>%
  distinct(rider_name)
names
```

```
# A tibble: 21 x 1
   rider_name           
   <chr>                
 1 Bevin, Patrick       
 2 Edet, Nicolas        
 3 Laporte, Christophe  
 4 Van Garderen, Tejay  
 5 de Marchi, Alessandro
 6 Zabel, Rick          
 7 Terpstra, Niki       
 8 Nizzolo, Giacomo     
 9 Philipsen, Jasper    
10 Dennis, Rohan        
# … with 11 more rows
```

```r
tdf_clean %>%
  filter(rider_name == "Bevin, Patrick")
```

```
# A tibble: 21 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Bevin, Pa… New Zeal… CCC Team  Poland   Brussels Brussels
 2     2 Bevin, Pa… New Zeal… CCC Team  Poland   Brussels Brussels
 3     3 Bevin, Pa… New Zeal… CCC Team  Poland   Binche   Epernay 
 4     4 Bevin, Pa… New Zeal… CCC Team  Poland   Reims    Nancy   
 5     5 Bevin, Pa… New Zeal… CCC Team  Poland   Saint-D… Colmar  
 6     6 Bevin, Pa… New Zeal… CCC Team  Poland   Mulhouse Planche…
 7     7 Bevin, Pa… New Zeal… CCC Team  Poland   Belfort  Chalon-…
 8     8 Bevin, Pa… New Zeal… CCC Team  Poland   Macon    Saint E…
 9     9 Bevin, Pa… New Zeal… CCC Team  Poland   Saint E… Brioude 
10    10 Bevin, Pa… New Zeal… CCC Team  Poland   Saint-F… Albi    
# … with 11 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
```


```r
saveRDS(tdf_clean, "results/tdf_clean.rds")
```

### Task 2

#### Part 1

Fix the time variables (time, young_rider_time) in your tidy data frame so each cyclist's stage time is given rather than just the winner's time and time back from the winner. For example, rather than "04:22.47", "+00:00.00", "+00:00.00", "+00:00.00", ... in stage 1, it should be changed to "04:22.47", "04:22.47", "04:22.47", "04:22.47", .... You may keep the result as type character or change it to a reasonable date/time data type.



```r
stage_n <- tdf_clean %>%
#  filter(stage == 3) %>%
  mutate(time = str_remove(time, "\\+"),
         time = time(time))

stage_n
```

```
# A tibble: 3,696 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Teunissen… Netherla… Team Jum… Netherl… Brussels Brussels
 2     1 Sagan, Pe… Slovakia  Bora - H… Germany  Brussels Brussels
 3     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 4     1 Nizzolo, … Italy     Team Dim… South A… Brussels Brussels
 5     1 Colbrelli… Italy     Bahrain … Bahrain  Brussels Brussels
 6     1 Matthews,… Australia Team Sun… Netherl… Brussels Brussels
 7     1 Trentin, … Italy     Mitchelt… Austral… Brussels Brussels
 8     1 Naesen, O… Belgium   Ag2r La … France   Brussels Brussels
 9     1 Viviani, … Italy     Deceunin… Belgium  Brussels Brussels
10     1 Stuyven, … Belgium   Trek–Seg… USA      Brussels Brussels
# … with 3,686 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <dbl>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
```

```r
tdf_clean
```

```
# A tibble: 3,696 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Teunissen… Netherla… Team Jum… Netherl… Brussels Brussels
 2     1 Sagan, Pe… Slovakia  Bora - H… Germany  Brussels Brussels
 3     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 4     1 Nizzolo, … Italy     Team Dim… South A… Brussels Brussels
 5     1 Colbrelli… Italy     Bahrain … Bahrain  Brussels Brussels
 6     1 Matthews,… Australia Team Sun… Netherl… Brussels Brussels
 7     1 Trentin, … Italy     Mitchelt… Austral… Brussels Brussels
 8     1 Naesen, O… Belgium   Ag2r La … France   Brussels Brussels
 9     1 Viviani, … Italy     Deceunin… Belgium  Brussels Brussels
10     1 Stuyven, … Belgium   Trek–Seg… USA      Brussels Brussels
# … with 3,686 more rows, and 11 more variables: classification <chr>,
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
```


```r
tdf_clean <- tdf_clean %>%
  mutate(time = convert_seconds(time))
```


```r
winning_times <- tdf_clean %>%
  filter(time_rank == 1) %>%
  select(stage, time)

two <- c(stage = 2, time = NA)
nineteen <- c(stage = 19, time = NA)

winning_times <- rbind_list(winning_times, two, nineteen) %>%
  arrange(stage)
```


absolute_times <- function(num) {
  n <- 
  woop <- tdf_clean %>%
    filter(stage == n) %>%
    mutate(time = case_when(
      time_rank == 1 ~ time,
      TRUE ~ winning_times[[n,2]] + time
    ))
  
   return (woop)
}
absolute_times(4)



```r
woop <- function(n) {
  yay <- tdf_clean %>%
  mutate(time = case_when(
    stage == n & time_rank == 1 ~ time,
    stage == n & time_rank != 1 ~ winning_times[[n, 2]] + time,
    TRUE ~ time
  ))
  return (yay)
}

woop(2)
```

```
# A tibble: 3,696 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Teunissen… Netherla… Team Jum… Netherl… Brussels Brussels
 2     1 Sagan, Pe… Slovakia  Bora - H… Germany  Brussels Brussels
 3     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 4     1 Nizzolo, … Italy     Team Dim… South A… Brussels Brussels
 5     1 Colbrelli… Italy     Bahrain … Bahrain  Brussels Brussels
 6     1 Matthews,… Australia Team Sun… Netherl… Brussels Brussels
 7     1 Trentin, … Italy     Mitchelt… Austral… Brussels Brussels
 8     1 Naesen, O… Belgium   Ag2r La … France   Brussels Brussels
 9     1 Viviani, … Italy     Deceunin… Belgium  Brussels Brussels
10     1 Stuyven, … Belgium   Trek–Seg… USA      Brussels Brussels
# … with 3,686 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <dbl>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
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
```

omo <- function(n) {
  cat(str_c("stage == ", n, " & time_rank == 1 ~ time,\n stage == ", n, " & time_rank != 1 ~ winning_times[[", n, ", 2]] + time"))
}
omo(1)

tdf_clean %>%
  mutate(time = case_when(
    omo(1),
    omo(2), 
    omo(3),
    TRUE ~ time
  ))


```r
minutes_and_seconds <- function(time) {
  min <- time %/% 60
  sec <- time %% 60
  return (str_c(min, ":", sec))
  as.POSIXlt()
}

tdf_clean %>%
  mutate(time = minutes_and_seconds(time))
```

```
# A tibble: 3,696 x 18
   stage rider_name rider_nat team_name team_nat dep_city arr_city
   <int> <chr>      <chr>     <chr>     <chr>    <chr>    <chr>   
 1     1 Teunissen… Netherla… Team Jum… Netherl… Brussels Brussels
 2     1 Sagan, Pe… Slovakia  Bora - H… Germany  Brussels Brussels
 3     1 Ewan, Cal… Australia Lotto So… Belgium  Brussels Brussels
 4     1 Nizzolo, … Italy     Team Dim… South A… Brussels Brussels
 5     1 Colbrelli… Italy     Bahrain … Bahrain  Brussels Brussels
 6     1 Matthews,… Australia Team Sun… Netherl… Brussels Brussels
 7     1 Trentin, … Italy     Mitchelt… Austral… Brussels Brussels
 8     1 Naesen, O… Belgium   Ag2r La … France   Brussels Brussels
 9     1 Viviani, … Italy     Deceunin… Belgium  Brussels Brussels
10     1 Stuyven, … Belgium   Trek–Seg… USA      Brussels Brussels
# … with 3,686 more rows, and 11 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>
```


### References 

Converting to decimal hours:
https://www.r-bloggers.com/using-dates-and-times-in-r/
