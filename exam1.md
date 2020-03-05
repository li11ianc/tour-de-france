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

Use object tdf to create a tidy data frame called tdf_clean that contains the following variables. Each variable should be of the specified type given in parentheses.

stage - stage of the Tour (integer)
rider_name - full name of the cyclist, no need to change the format (character)
rider_nat - cyclist's nationality (character)
team_name - cyclist's team name (character)
team_nat - cyclist's team nationality (character)
dep_city - departure city for given stage (character)
arr_city - arrival city for given stage (character)
classification - stage's classification (character)
distance - stage's distance that cyclists will ride (double)
start_date - stage's start date, not the time (date)
time - cyclist's time or relative time on a given stage (character)
time_rank - rank of cyclist as given in the stage (integer)
sprint_pts - sprint points earned by cyclist on given stage (double)
sprint_rank - rank of cyclist based on sprint points within stage (integer)
climb_pts - climb points earned by cyclist on given stage (double)
climb_rank - rank of cyclist based on climb points within stage (integer)
young_rider_time - young rider time on a given stage (character)
young_rider_rank - rank of cyclist based on young rider time within stage (integer)
If a variable's value is missing, code it as NA. For example, some cyclists may have values dns, dnf, or dq if they did not start, did not finish, or were disqualified, respectively. Similarly, most riders will not have climb points and a climb rank since only a few points are up for grabs in a given stage; riders missing these values should also have NA for the respective variable's value.


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
  select(-team_time, -team_rank)
```

-dns, -dnf, -dsq,


```r
tdf_clean
```

```
# A tibble: 3,696 x 21
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
# … with 3,686 more rows, and 14 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>, dns <lgl>, dnf <lgl>,
#   dsq <lgl>
```


```r
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
# A tibble: 21 x 21
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
# … with 11 more rows, and 14 more variables: classification <chr>,
#   distance <dbl>, start_date <date>, time <chr>, time_rank <int>,
#   sprint_pts <dbl>, sprint_rank <int>, climb_pts <dbl>, climb_rank <int>,
#   young_rider_time <chr>, young_rider_rank <int>, dns <lgl>, dnf <lgl>,
#   dsq <lgl>
```


```r
saveRDS(tdf_clean, "results/tdf_clean.rds")
```

