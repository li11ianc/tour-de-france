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
stage1 <- tdf[[1]]
```


lapply(tdf, unlist) %>%
  lapply(., unlist)

name <- trimws(map_chr(nasa, 1))
id <- as.integer(map_chr(nasa, 2))
name_type <- map_chr(nasa, 3)
rec_class <- map_chr(nasa, 4)
mass <- as.double(map_chr(nasa, 5))
fall <- map_chr(nasa, 6)
year <- map_chr(nasa, 7)
rec_lat <- map(nasa, 8)
rec_long <- map(nasa, 9)
geo_coord <- map(nasa, 10)
geo_coord <- map(geo_coord,2)
data <- cbind(name, id, name_type, rec_class, mass, fall, year, rec_lat, rec_long, geo_coord)
data

map_df(nasa, `[`, c("name", "id", "nametype", "recclass", "fall"))

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

Create a folder in your repo called results. Save tdf_clean as an object in folder results with the below code.

saveRDS(tdf_clean, "results/tdf_clean.rds")



# beginning with stage 1
for x in (1:21){
  
}
stage <- map_chr(tdf, stage1$stage$description)
  to get stage : tdf[[n]]$stage$description for n 1-3
  to get ridername : tdf[[i]]$stage$competitors[[j]]$name for i 1-3 and all j, length(tdf[[i]]$stage$competitors
  to get ridernationality : tdf[[i]]$stage$competitors[[j]]$nationality for i 1-3 and all j, length(tdf[[i]]$stage$competitors
  to get team_name : tdf[[i]]$stage$competitors[[j]]$team$name
  team_nationality : tdf[[1]]$stage$competitors[[1]]$team$nationality
  dept city :  tdf[[1]]$stage$departure_city
  arrival city : tdf[[1]]$stage$arrival_city
  classification ??
# 


```r
data.frame(tdf[[2]]$stage) %>%
  select(-contains("parents"))
```

```
               id description                 scheduled
1 sr:stage:415978     Stage 2 2019-07-07T12:30:00+00:00
              scheduled_end  type departure_city arrival_city status
1 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
   classification distance distance_unit single_event      competitors.id
1 Team Time Trial     27,6            km        FALSE sr:competitor:26658
     competitors.name competitors.gender competitors.nationality
1 Valverde, Alejandro               male                   Spain
  competitors.country_code competitors.team.id competitors.team.name
1                      ESP sr:competitor:26600         Movistar Team
  competitors.team.gender competitors.team.nationality
1                    male                        Spain
  competitors.team.country_code     competitors.id.1 competitors.name.1
1                           ESP sr:competitor:135930         Haig, Jack
  competitors.gender.1 competitors.nationality.1 competitors.country_code.1
1                 male                 Australia                        AUS
  competitors.team.id.1 competitors.team.name.1 competitors.team.gender.1
1   sr:competitor:62812        Mitchelton-Scott                      male
  competitors.team.nationality.1 competitors.team.country_code.1
1                      Australia                             AUS
      competitors.id.2 competitors.name.2 competitors.gender.2
1 sr:competitor:123892        Yates, Adam                 male
  competitors.nationality.2 competitors.country_code.2 competitors.team.id.2
1             Great Britain                        GBR   sr:competitor:62812
  competitors.team.name.2 competitors.team.gender.2
1        Mitchelton-Scott                      male
  competitors.team.nationality.2 competitors.team.country_code.2
1                      Australia                             AUS
      competitors.id.3 competitors.name.3 competitors.gender.3
1 sr:competitor:310616     Scully, Thomas                 male
  competitors.nationality.3 competitors.country_code.3 competitors.team.id.3
1               New Zealand                        NZL   sr:competitor:27747
  competitors.team.name.3 competitors.team.gender.3
1      EF Education First                      male
  competitors.team.nationality.3 competitors.team.country_code.3
1                            USA                             USA
      competitors.id.4 competitors.name.4 competitors.gender.4
1 sr:competitor:123378     Zakarin, Ilnur                 male
  competitors.nationality.4 competitors.country_code.4 competitors.team.id.4
1                    Russia                        RUS   sr:competitor:33029
  competitors.team.name.4 competitors.team.gender.4
1  Team Katusha - Alpecin                      male
  competitors.team.nationality.4 competitors.team.country_code.4
1                    Switzerland                             CHE
      competitors.id.5 competitors.name.5 competitors.gender.5
1 sr:competitor:135922        Ewan, Caleb                 male
  competitors.nationality.5 competitors.country_code.5 competitors.team.id.5
1                 Australia                        AUS   sr:competitor:27616
  competitors.team.name.5 competitors.team.gender.5
1            Lotto Soudal                      male
  competitors.team.nationality.5 competitors.team.country_code.5
1                        Belgium                             BEL
      competitors.id.6 competitors.name.6 competitors.gender.6
1 sr:competitor:135938     Mohoric, Matej                 male
  competitors.nationality.6 competitors.country_code.6 competitors.team.id.6
1                  Slovenia                        SVN   sr:competitor:26395
  competitors.team.name.6 competitors.team.gender.6
1        Bahrain - Merida                      male
  competitors.team.nationality.6 competitors.team.country_code.6
1                        Bahrain                             BHR
      competitors.id.7  competitors.name.7 competitors.gender.7
1 sr:competitor:135924 Alaphilippe, Julian                 male
  competitors.nationality.7 competitors.country_code.7 competitors.team.id.7
1                    France                        FRA   sr:competitor:26520
    competitors.team.name.7 competitors.team.gender.7
1 Deceuninck - Quick - Step                      male
  competitors.team.nationality.7 competitors.team.country_code.7
1                        Belgium                             BEL
      competitors.id.8 competitors.name.8 competitors.gender.8
1 sr:competitor:135926        Zabel, Rick                 male
  competitors.nationality.8 competitors.country_code.8 competitors.team.id.8
1                   Germany                        DEU   sr:competitor:33029
  competitors.team.name.8 competitors.team.gender.8
1  Team Katusha - Alpecin                      male
  competitors.team.nationality.8 competitors.team.country_code.8
1                    Switzerland                             CHE
      competitors.id.9 competitors.name.9 competitors.gender.9
1 sr:competitor:146106    Stuyven, Jasper                 male
  competitors.nationality.9 competitors.country_code.9 competitors.team.id.9
1                   Belgium                        BEL   sr:competitor:62896
  competitors.team.name.9 competitors.team.gender.9
1          Trek–Segafredo                      male
  competitors.team.nationality.9 competitors.team.country_code.9
1                            USA                             USA
     competitors.id.10 competitors.name.10 competitors.gender.10
1 sr:competitor:135946    Bettiol, Alberto                  male
  competitors.nationality.10 competitors.country_code.10 competitors.team.id.10
1                      Italy                         ITA    sr:competitor:27747
  competitors.team.name.10 competitors.team.gender.10
1       EF Education First                       male
  competitors.team.nationality.10 competitors.team.country_code.10
1                             USA                              USA
     competitors.id.11    competitors.name.11 competitors.gender.11
1 sr:competitor:123886 Kragh Andersen, Soeren                  male
  competitors.nationality.11 competitors.country_code.11 competitors.team.id.11
1                    Denmark                         DNK   sr:competitor:310638
  competitors.team.name.11 competitors.team.gender.11
1              Team Sunweb                       male
  competitors.team.nationality.11 competitors.team.country_code.11
1                     Netherlands                              NLD
     competitors.id.12 competitors.name.12 competitors.gender.12
1 sr:competitor:146110   van Baarle, Dylan                  male
  competitors.nationality.12 competitors.country_code.12 competitors.team.id.12
1                Netherlands                         NLD    sr:competitor:39815
  competitors.team.name.12 competitors.team.gender.12
1               Team Ineos                       male
  competitors.team.nationality.12 competitors.team.country_code.12
1                   Great Britain                              GBR
     competitors.id.13 competitors.name.13 competitors.gender.13
1 sr:competitor:147128  Bonifazio, Niccolo                  male
  competitors.nationality.13 competitors.country_code.13 competitors.team.id.13
1                      Italy                         ITA   sr:competitor:246991
  competitors.team.name.13 competitors.team.gender.13
1           Direct Energie                       male
  competitors.team.nationality.13 competitors.team.country_code.13
1                          France                              FRA
     competitors.id.14 competitors.name.14 competitors.gender.14
1 sr:competitor:198734  Rossetto, Stephane                  male
  competitors.nationality.14 competitors.country_code.14 competitors.team.id.14
1                     France                         FRA    sr:competitor:26495
  competitors.team.name.14 competitors.team.gender.14
1                  Cofidis                       male
  competitors.team.nationality.14 competitors.team.country_code.14
1                          France                              FRA
     competitors.id.15 competitors.name.15 competitors.gender.15
1 sr:competitor:208169 Laporte, Christophe                  male
  competitors.nationality.15 competitors.country_code.15 competitors.team.id.15
1                     France                         FRA    sr:competitor:26495
  competitors.team.name.15 competitors.team.gender.15
1                  Cofidis                       male
  competitors.team.nationality.15 competitors.team.country_code.15
1                          France                              FRA
     competitors.id.16 competitors.name.16 competitors.gender.16
1 sr:competitor:197808       Benoot, Tiesj                  male
  competitors.nationality.16 competitors.country_code.16 competitors.team.id.16
1                    Belgium                         BEL    sr:competitor:27616
  competitors.team.name.16 competitors.team.gender.16
1             Lotto Soudal                       male
  competitors.team.nationality.16 competitors.team.country_code.16
1                         Belgium                              BEL
     competitors.id.17 competitors.name.17 competitors.gender.17
1 sr:competitor:171236    de Buyst, Jasper                  male
  competitors.nationality.17 competitors.country_code.17 competitors.team.id.17
1                    Belgium                         BEL    sr:competitor:27616
  competitors.team.name.17 competitors.team.gender.17
1             Lotto Soudal                       male
  competitors.team.nationality.17 competitors.team.country_code.17
1                         Belgium                              BEL
     competitors.id.18 competitors.name.18 competitors.gender.18
1 sr:competitor:196712        Teuns, Dylan                  male
  competitors.nationality.18 competitors.country_code.18 competitors.team.id.18
1                    Belgium                         BEL    sr:competitor:26395
  competitors.team.name.18 competitors.team.gender.18
1         Bahrain - Merida                       male
  competitors.team.nationality.18 competitors.team.country_code.18
1                         Bahrain                              BHR
     competitors.id.19 competitors.name.19 competitors.gender.19
1 sr:competitor:174908      Woods, Michael                  male
  competitors.nationality.19 competitors.country_code.19 competitors.team.id.19
1                     Canada                         CAN    sr:competitor:27747
  competitors.team.name.19 competitors.team.gender.19
1       EF Education First                       male
  competitors.team.nationality.19 competitors.team.country_code.19
1                             USA                              USA
     competitors.id.20 competitors.name.20 competitors.gender.20
1 sr:competitor:123888        Yates, Simon                  male
  competitors.nationality.20 competitors.country_code.20 competitors.team.id.20
1              Great Britain                         GBR    sr:competitor:62812
  competitors.team.name.20 competitors.team.gender.20
1         Mitchelton-Scott                       male
  competitors.team.nationality.20 competitors.team.country_code.20
1                       Australia                              AUS
     competitors.id.21       competitors.name.21 competitors.gender.21
1 sr:competitor:123880 Valgren Andersen, Michael                  male
  competitors.nationality.21 competitors.country_code.21 competitors.team.id.21
1                    Denmark                         DNK    sr:competitor:80955
  competitors.team.name.21 competitors.team.gender.21
1      Team Dimension Data                       male
  competitors.team.nationality.21 competitors.team.country_code.21
1                    South Africa                              ZAF
     competitors.id.22 competitors.name.22 competitors.gender.22
1 sr:competitor:199422        Kung, Stefan                  male
  competitors.nationality.22 competitors.country_code.22 competitors.team.id.22
1                Switzerland                         CHE    sr:competitor:26516
  competitors.team.name.22 competitors.team.gender.22
1           Groupama – FDJ                       male
  competitors.team.nationality.22 competitors.team.country_code.22
1                          France                              FRA
    competitors.id.23        competitors.name.23 competitors.gender.23
1 sr:competitor:92871 Verona Quintanilla, Carlos                  male
  competitors.nationality.23 competitors.country_code.23 competitors.team.id.23
1                      Spain                         ESP    sr:competitor:26600
  competitors.team.name.23 competitors.team.gender.23
1            Movistar Team                       male
  competitors.team.nationality.23 competitors.team.country_code.23
1                           Spain                              ESP
    competitors.id.24 competitors.name.24 competitors.gender.24
1 sr:competitor:78671        Molard, Rudy                  male
  competitors.nationality.24 competitors.country_code.24 competitors.team.id.24
1                     France                         FRA    sr:competitor:26516
  competitors.team.name.24 competitors.team.gender.24
1           Groupama – FDJ                       male
  competitors.team.nationality.24 competitors.team.country_code.24
1                          France                              FRA
    competitors.id.25 competitors.name.25 competitors.gender.25
1 sr:competitor:80287        Wellens, Tim                  male
  competitors.nationality.25 competitors.country_code.25 competitors.team.id.25
1                    Belgium                         BEL    sr:competitor:27616
  competitors.team.name.25 competitors.team.gender.25
1             Lotto Soudal                       male
  competitors.team.nationality.25 competitors.team.country_code.25
1                         Belgium                              BEL
    competitors.id.26 competitors.name.26 competitors.gender.26
1 sr:competitor:80289         Houle, Hugo                  male
  competitors.nationality.26 competitors.country_code.26 competitors.team.id.26
1                     Canada                         CAN    sr:competitor:26598
  competitors.team.name.26 competitors.team.gender.26
1          Astana Pro Team                       male
  competitors.team.nationality.26 competitors.team.country_code.26
1                      Kazakhstan                              KAZ
    competitors.id.27           competitors.name.27 competitors.gender.27
1 sr:competitor:81383 Janse van Rensburg, Reinhardt                  male
  competitors.nationality.27 competitors.country_code.27 competitors.team.id.27
1               South Africa                         ZAF    sr:competitor:80955
  competitors.team.name.27 competitors.team.gender.27
1      Team Dimension Data                       male
  competitors.team.nationality.27 competitors.team.country_code.27
1                    South Africa                              ZAF
    competitors.id.28 competitors.name.28 competitors.gender.28
1 sr:competitor:88952    Gougeard, Alexis                  male
  competitors.nationality.28 competitors.country_code.28 competitors.team.id.28
1                     France                         FRA    sr:competitor:26519
  competitors.team.name.28 competitors.team.gender.28
1         Ag2r La Mondiale                       male
  competitors.team.nationality.28 competitors.team.country_code.28
1                          France                              FRA
    competitors.id.29 competitors.name.29 competitors.gender.29
1 sr:competitor:82007          Aru, Fabio                  male
  competitors.nationality.29 competitors.country_code.29 competitors.team.id.29
1                      Italy                         ITA   sr:competitor:310636
  competitors.team.name.29 competitors.team.gender.29
1        UAE Team Emirates                       male
  competitors.team.nationality.29 competitors.team.country_code.29
1            United Arab Emirates                              ARE
    competitors.id.30 competitors.name.30 competitors.gender.30
1 sr:competitor:91766     Barguil, Warren                  male
  competitors.nationality.30 competitors.country_code.30 competitors.team.id.30
1                     France                         FRA   sr:competitor:246989
  competitors.team.name.30 competitors.team.gender.30
1          Fortuneo-Samsic                       male
  competitors.team.nationality.30 competitors.team.country_code.30
1                          France                              FRA
    competitors.id.31 competitors.name.31 competitors.gender.31
1 sr:competitor:91768  Vuillermoz, Alexis                  male
  competitors.nationality.31 competitors.country_code.31 competitors.team.id.31
1                     France                         FRA    sr:competitor:26519
  competitors.team.name.31 competitors.team.gender.31
1         Ag2r La Mondiale                       male
  competitors.team.nationality.31 competitors.team.country_code.31
1                          France                              FRA
    competitors.id.32 competitors.name.32 competitors.gender.32
1 sr:competitor:93161      Lampaert, Yves                  male
  competitors.nationality.32 competitors.country_code.32 competitors.team.id.32
1                    Belgium                         BEL    sr:competitor:26520
   competitors.team.name.32 competitors.team.gender.32
1 Deceuninck - Quick - Step                       male
  competitors.team.nationality.32 competitors.team.country_code.32
1                         Belgium                              BEL
     competitors.id.33  competitors.name.33 competitors.gender.33
1 sr:competitor:123874 Nielsen, Magnus Cort                  male
  competitors.nationality.33 competitors.country_code.33 competitors.team.id.33
1                    Denmark                         DNK    sr:competitor:26598
  competitors.team.name.33 competitors.team.gender.33
1          Astana Pro Team                       male
  competitors.team.nationality.33 competitors.team.country_code.33
1                      Kazakhstan                              KAZ
    competitors.id.34 competitors.name.34 competitors.gender.34
1 sr:competitor:93179       Arndt, Nikias                  male
  competitors.nationality.34 competitors.country_code.34 competitors.team.id.34
1                    Germany                         DEU   sr:competitor:310638
  competitors.team.name.34 competitors.team.gender.34
1              Team Sunweb                       male
  competitors.team.nationality.34 competitors.team.country_code.34
1                     Netherlands                              NLD
    competitors.id.35 competitors.name.35 competitors.gender.35
1 sr:competitor:93813    Lutsenko, Alexey                  male
  competitors.nationality.35 competitors.country_code.35 competitors.team.id.35
1                 Kazakhstan                         KAZ    sr:competitor:26598
  competitors.team.name.35 competitors.team.gender.35
1          Astana Pro Team                       male
  competitors.team.nationality.35 competitors.team.country_code.35
1                      Kazakhstan                              KAZ
    competitors.id.36    competitors.name.36 competitors.gender.36
1 sr:competitor:93811 Fraile Matarranz, Omar                  male
  competitors.nationality.36 competitors.country_code.36 competitors.team.id.36
1                      Spain                         ESP    sr:competitor:26598
  competitors.team.name.36 competitors.team.gender.36
1          Astana Pro Team                       male
  competitors.team.nationality.36 competitors.team.country_code.36
1                      Kazakhstan                              KAZ
    competitors.id.37  competitors.name.37 competitors.gender.37
1 sr:competitor:94613 Perichon, Pierre-Luc                  male
  competitors.nationality.37 competitors.country_code.37 competitors.team.id.37
1                     France                         FRA    sr:competitor:26495
  competitors.team.name.37 competitors.team.gender.37
1                  Cofidis                       male
  competitors.team.nationality.37 competitors.team.country_code.37
1                          France                              FRA
    competitors.id.38    competitors.name.38 competitors.gender.38
1 sr:competitor:95635 Reichenbach, Sebastien                  male
  competitors.nationality.38 competitors.country_code.38 competitors.team.id.38
1                Switzerland                         CHE    sr:competitor:26516
  competitors.team.name.38 competitors.team.gender.38
1           Groupama – FDJ                       male
  competitors.team.nationality.38 competitors.team.country_code.38
1                          France                              FRA
     competitors.id.39 competitors.name.39 competitors.gender.39
1 sr:competitor:146340          Haga, Chad                  male
  competitors.nationality.39 competitors.country_code.39 competitors.team.id.39
1                        USA                         USA   sr:competitor:310638
  competitors.team.name.39 competitors.team.gender.39
1              Team Sunweb                       male
  competitors.team.nationality.39 competitors.team.country_code.39
1                     Netherlands                              NLD
     competitors.id.40 competitors.name.40 competitors.gender.40
1 sr:competitor:101459    Berhane, Natnael                  male
  competitors.nationality.40 competitors.country_code.40 competitors.team.id.40
1                    Eritrea                         ERI    sr:competitor:26495
  competitors.team.name.40 competitors.team.gender.40
1                  Cofidis                       male
  competitors.team.nationality.40 competitors.team.country_code.40
1                          France                              FRA
     competitors.id.41 competitors.name.41 competitors.gender.41
1 sr:competitor:123856 Bystroem, Sven Erik                  male
  competitors.nationality.41 competitors.country_code.41 competitors.team.id.41
1                     Norway                         NOR   sr:competitor:310636
  competitors.team.name.41 competitors.team.gender.41
1        UAE Team Emirates                       male
  competitors.team.nationality.41 competitors.team.country_code.41
1            United Arab Emirates                              ARE
     competitors.id.42    competitors.name.42 competitors.gender.42
1 sr:competitor:318361 Schachmann, Maximilian                  male
  competitors.nationality.42 competitors.country_code.42 competitors.team.id.42
1                    Germany                         DEU    sr:competitor:50271
  competitors.team.name.42 competitors.team.gender.42
1         Bora - Hansgrohe                       male
  competitors.team.nationality.42 competitors.team.country_code.42
1                         Germany                              DEU
     competitors.id.43 competitors.name.43 competitors.gender.43
1 sr:competitor:226716       Skujins, Toms                  male
  competitors.nationality.43 competitors.country_code.43 competitors.team.id.43
1                     Latvia                         LVA    sr:competitor:62896
  competitors.team.name.43 competitors.team.gender.43
1           Trek–Segafredo                       male
  competitors.team.nationality.43 competitors.team.country_code.43
1                             USA                              USA
    competitors.id.44 competitors.name.44 competitors.gender.44
1 sr:competitor:67014      Bardet, Romain                  male
  competitors.nationality.44 competitors.country_code.44 competitors.team.id.44
1                     France                         FRA    sr:competitor:26519
  competitors.team.name.44 competitors.team.gender.44
1         Ag2r La Mondiale                       male
  competitors.team.nationality.44 competitors.team.country_code.44
1                          France                              FRA
     competitors.id.45 competitors.name.45 competitors.gender.45
1 sr:competitor:310574  Mas Nicolau, Enric                  male
  competitors.nationality.45 competitors.country_code.45 competitors.team.id.45
1                      Spain                         ESP    sr:competitor:26520
   competitors.team.name.45 competitors.team.gender.45
1 Deceuninck - Quick - Step                       male
  competitors.team.nationality.45 competitors.team.country_code.45
1                         Belgium                              BEL
     competitors.id.46 competitors.name.46 competitors.gender.46
1 sr:competitor:249457        Politt, Nils                  male
  competitors.nationality.46 competitors.country_code.46 competitors.team.id.46
1                    Germany                         DEU    sr:competitor:33029
  competitors.team.name.46 competitors.team.gender.46
1   Team Katusha - Alpecin                       male
  competitors.team.nationality.46 competitors.team.country_code.46
1                     Switzerland                              CHE
     competitors.id.47 competitors.name.47 competitors.gender.47
1 sr:competitor:246981   Calmejane, Lilian                  male
  competitors.nationality.47 competitors.country_code.47 competitors.team.id.47
1                     France                         FRA   sr:competitor:246991
  competitors.team.name.47 competitors.team.gender.47
1           Direct Energie                       male
  competitors.team.nationality.47 competitors.team.country_code.47
1                          France                              FRA
     competitors.id.48 competitors.name.48 competitors.gender.48
1 sr:competitor:248863     Bernard, Julien                  male
  competitors.nationality.48 competitors.country_code.48 competitors.team.id.48
1                     France                         FRA    sr:competitor:62896
  competitors.team.name.48 competitors.team.gender.48
1           Trek–Segafredo                       male
  competitors.team.nationality.48 competitors.team.country_code.48
1                             USA                              USA
     competitors.id.49 competitors.name.49 competitors.gender.49
1 sr:competitor:254335   Martin, Guillaume                  male
  competitors.nationality.49 competitors.country_code.49 competitors.team.id.49
1                     France                         FRA    sr:competitor:49122
  competitors.team.name.49 competitors.team.gender.49
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.49 competitors.team.country_code.49
1                         Belgium                              BEL
     competitors.id.50 competitors.name.50 competitors.gender.50
1 sr:competitor:313921        Bernal, Egan                  male
  competitors.nationality.50 competitors.country_code.50 competitors.team.id.50
1                   Colombia                         COL    sr:competitor:39815
  competitors.team.name.50 competitors.team.gender.50
1               Team Ineos                       male
  competitors.team.nationality.50 competitors.team.country_code.50
1                   Great Britain                              GBR
     competitors.id.51 competitors.name.51 competitors.gender.51
1 sr:competitor:282491    Grellier, Fabien                  male
  competitors.nationality.51 competitors.country_code.51 competitors.team.id.51
1                     France                         FRA   sr:competitor:246991
  competitors.team.name.51 competitors.team.gender.51
1           Direct Energie                       male
  competitors.team.nationality.51 competitors.team.country_code.51
1                          France                              FRA
     competitors.id.52 competitors.name.52 competitors.gender.52
1 sr:competitor:286739      de Gendt, Aime                  male
  competitors.nationality.52 competitors.country_code.52 competitors.team.id.52
1                    Belgium                         BEL    sr:competitor:49122
  competitors.team.name.52 competitors.team.gender.52
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.52 competitors.team.country_code.52
1                         Belgium                              BEL
     competitors.id.53  competitors.name.53 competitors.gender.53
1 sr:competitor:313919 Garcia Cortina, Ivan                  male
  competitors.nationality.53 competitors.country_code.53 competitors.team.id.53
1                      Spain                         ESP    sr:competitor:26395
  competitors.team.name.53 competitors.team.gender.53
1         Bahrain - Merida                       male
  competitors.team.nationality.53 competitors.team.country_code.53
1                         Bahrain                              BHR
     competitors.id.54     competitors.name.54 competitors.gender.54
1 sr:competitor:319169 Jansen Groendahl, Amund                  male
  competitors.nationality.54 competitors.country_code.54 competitors.team.id.54
1                     Norway                         NOR   sr:competitor:189354
  competitors.team.name.54 competitors.team.gender.54
1       Team Jumbo - Visma                       male
  competitors.team.nationality.54 competitors.team.country_code.54
1                     Netherlands                              NLD
     competitors.id.55                    competitors.name.55
1 sr:competitor:226972 Richeze Araquistain, Ariel Maximiliano
  competitors.gender.55 competitors.nationality.55 competitors.country_code.55
1                  male                  Argentina                         ARG
  competitors.team.id.55  competitors.team.name.55 competitors.team.gender.55
1    sr:competitor:26520 Deceuninck - Quick - Step                       male
  competitors.team.nationality.55 competitors.team.country_code.55
1                         Belgium                              BEL
     competitors.id.56 competitors.name.56 competitors.gender.56
1 sr:competitor:317941      Kamna, Lennard                  male
  competitors.nationality.56 competitors.country_code.56 competitors.team.id.56
1                    Germany                         DEU   sr:competitor:310638
  competitors.team.name.56 competitors.team.gender.56
1              Team Sunweb                       male
  competitors.team.nationality.56 competitors.team.country_code.56
1                     Netherlands                              NLD
     competitors.id.57 competitors.name.57 competitors.gender.57
1 sr:competitor:323145        Gaudu, David                  male
  competitors.nationality.57 competitors.country_code.57 competitors.team.id.57
1                     France                         FRA    sr:competitor:26516
  competitors.team.name.57 competitors.team.gender.57
1           Groupama – FDJ                       male
  competitors.team.nationality.57 competitors.team.country_code.57
1                          France                              FRA
     competitors.id.58 competitors.name.58 competitors.gender.58
1 sr:competitor:325989      Perez, Anthony                  male
  competitors.nationality.58 competitors.country_code.58 competitors.team.id.58
1                     France                         FRA    sr:competitor:26495
  competitors.team.name.58 competitors.team.gender.58
1                  Cofidis                       male
  competitors.team.nationality.58 competitors.team.country_code.58
1                          France                              FRA
     competitors.id.59 competitors.name.59 competitors.gender.59
1 sr:competitor:329997       Gesbert, Elie                  male
  competitors.nationality.59 competitors.country_code.59 competitors.team.id.59
1                     France                         FRA   sr:competitor:246989
  competitors.team.name.59 competitors.team.gender.59
1          Fortuneo-Samsic                       male
  competitors.team.nationality.59 competitors.team.country_code.59
1                          France                              FRA
     competitors.id.60 competitors.name.60 competitors.gender.60
1 sr:competitor:330003      Ourselin, Paul                  male
  competitors.nationality.60 competitors.country_code.60 competitors.team.id.60
1                     France                         FRA   sr:competitor:246991
  competitors.team.name.60 competitors.team.gender.60
1           Direct Energie                       male
  competitors.team.nationality.60 competitors.team.country_code.60
1                          France                              FRA
     competitors.id.61 competitors.name.61 competitors.gender.61
1 sr:competitor:353504      Van Aert, Wout                  male
  competitors.nationality.61 competitors.country_code.61 competitors.team.id.61
1                    Belgium                         BEL   sr:competitor:189354
  competitors.team.name.61 competitors.team.gender.61
1       Team Jumbo - Visma                       male
  competitors.team.nationality.61 competitors.team.country_code.61
1                     Netherlands                              NLD
     competitors.id.62 competitors.name.62 competitors.gender.62
1 sr:competitor:379864   Cosnefroy, Benoit                  male
  competitors.nationality.62 competitors.country_code.62 competitors.team.id.62
1                     France                         FRA    sr:competitor:26519
  competitors.team.name.62 competitors.team.gender.62
1         Ag2r La Mondiale                       male
  competitors.team.nationality.62 competitors.team.country_code.62
1                          France                              FRA
     competitors.id.63 competitors.name.63 competitors.gender.63
1 sr:competitor:379848   Philipsen, Jasper                  male
  competitors.nationality.63 competitors.country_code.63 competitors.team.id.63
1                    Belgium                         BEL   sr:competitor:310636
  competitors.team.name.63 competitors.team.gender.63
1        UAE Team Emirates                       male
  competitors.team.nationality.63 competitors.team.country_code.63
1            United Arab Emirates                              ARE
     competitors.id.64 competitors.name.64 competitors.gender.64
1 sr:competitor:241178      Bevin, Patrick                  male
  competitors.nationality.64 competitors.country_code.64 competitors.team.id.64
1                New Zealand                         NZL    sr:competitor:27981
  competitors.team.name.64 competitors.team.gender.64
1                 CCC Team                       male
  competitors.team.nationality.64 competitors.team.country_code.64
1                          Poland                              POL
     competitors.id.65 competitors.name.65 competitors.gender.65
1 sr:competitor:248853    de Plus, Laurens                  male
  competitors.nationality.65 competitors.country_code.65 competitors.team.id.65
1                    Belgium                         BEL   sr:competitor:189354
  competitors.team.name.65 competitors.team.gender.65
1       Team Jumbo - Visma                       male
  competitors.team.nationality.65 competitors.team.country_code.65
1                     Netherlands                              NLD
     competitors.id.66 competitors.name.66 competitors.gender.66
1 sr:competitor:198722     Teunissen, Mike                  male
  competitors.nationality.66 competitors.country_code.66 competitors.team.id.66
1                Netherlands                         NLD   sr:competitor:189354
  competitors.team.name.66 competitors.team.gender.66
1       Team Jumbo - Visma                       male
  competitors.team.nationality.66 competitors.team.country_code.66
1                     Netherlands                              NLD
     competitors.id.67 competitors.name.67 competitors.gender.67
1 sr:competitor:198994     Turgis, Anthony                  male
  competitors.nationality.67 competitors.country_code.67 competitors.team.id.67
1                     France                         FRA   sr:competitor:246991
  competitors.team.name.67 competitors.team.gender.67
1           Direct Energie                       male
  competitors.team.nationality.67 competitors.team.country_code.67
1                          France                              FRA
     competitors.id.68 competitors.name.68 competitors.gender.68
1 sr:competitor:196754     Ledanois, Kevin                  male
  competitors.nationality.68 competitors.country_code.68 competitors.team.id.68
1                     France                         FRA   sr:competitor:246989
  competitors.team.name.68 competitors.team.gender.68
1          Fortuneo-Samsic                       male
  competitors.team.nationality.68 competitors.team.country_code.68
1                          France                              FRA
     competitors.id.69 competitors.name.69 competitors.gender.69
1 sr:competitor:254977  Wisniowski, Lukasz                  male
  competitors.nationality.69 competitors.country_code.69 competitors.team.id.69
1                     Poland                         POL    sr:competitor:27981
  competitors.team.name.69 competitors.team.gender.69
1                 CCC Team                       male
  competitors.team.nationality.69 competitors.team.country_code.69
1                          Poland                              POL
     competitors.id.70 competitors.name.70 competitors.gender.70
1 sr:competitor:194902     Konrad, Patrick                  male
  competitors.nationality.70 competitors.country_code.70 competitors.team.id.70
1                    Austria                         AUT    sr:competitor:50271
  competitors.team.name.70 competitors.team.gender.70
1         Bora - Hansgrohe                       male
  competitors.team.nationality.70 competitors.team.country_code.70
1                         Germany                              DEU
     competitors.id.71 competitors.name.71 competitors.gender.71
1 sr:competitor:219922  Groenewegen, Dylan                  male
  competitors.nationality.71 competitors.country_code.71 competitors.team.id.71
1                Netherlands                         NLD   sr:competitor:189354
  competitors.team.name.71 competitors.team.gender.71
1       Team Jumbo - Visma                       male
  competitors.team.nationality.71 competitors.team.country_code.71
1                     Netherlands                              NLD
     competitors.id.72 competitors.name.72 competitors.gender.72
1 sr:competitor:197934     Naesen, Olivier                  male
  competitors.nationality.72 competitors.country_code.72 competitors.team.id.72
1                    Belgium                         BEL    sr:competitor:26519
  competitors.team.name.72 competitors.team.gender.72
1         Ag2r La Mondiale                       male
  competitors.team.nationality.72 competitors.team.country_code.72
1                          France                              FRA
     competitors.id.73 competitors.name.73 competitors.gender.73
1 sr:competitor:196762 Soler Gimenez, Marc                  male
  competitors.nationality.73 competitors.country_code.73 competitors.team.id.73
1                      Spain                         ESP    sr:competitor:26600
  competitors.team.name.73 competitors.team.gender.73
1            Movistar Team                       male
  competitors.team.nationality.73 competitors.team.country_code.73
1                           Spain                              ESP
     competitors.id.74 competitors.name.74 competitors.gender.74
1 sr:competitor:196774   Backaert, Fredrik                  male
  competitors.nationality.74 competitors.country_code.74 competitors.team.id.74
1                    Belgium                         BEL    sr:competitor:49122
  competitors.team.name.74 competitors.team.gender.74
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.74 competitors.team.country_code.74
1                         Belgium                              BEL
     competitors.id.75 competitors.name.75 competitors.gender.75
1 sr:competitor:198720      Rosskopf, Joey                  male
  competitors.nationality.75 competitors.country_code.75 competitors.team.id.75
1                        USA                         USA    sr:competitor:27981
  competitors.team.name.75 competitors.team.gender.75
1                 CCC Team                       male
  competitors.team.nationality.75 competitors.team.country_code.75
1                          Poland                              POL
     competitors.id.76 competitors.name.76 competitors.gender.76
1 sr:competitor:250457      Moscon, Gianni                  male
  competitors.nationality.76 competitors.country_code.76 competitors.team.id.76
1                      Italy                         ITA    sr:competitor:39815
  competitors.team.name.76 competitors.team.gender.76
1               Team Ineos                       male
  competitors.team.nationality.76 competitors.team.country_code.76
1                   Great Britain                              GBR
     competitors.id.77 competitors.name.77 competitors.gender.77
1 sr:competitor:323211    Meurisse, Xandro                  male
  competitors.nationality.77 competitors.country_code.77 competitors.team.id.77
1                    Belgium                         BEL    sr:competitor:49122
  competitors.team.name.77 competitors.team.gender.77
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.77 competitors.team.country_code.77
1                         Belgium                              BEL
     competitors.id.78 competitors.name.78 competitors.gender.78
1 sr:competitor:201073   Buchmann, Emanuel                  male
  competitors.nationality.78 competitors.country_code.78 competitors.team.id.78
1                    Germany                         DEU    sr:competitor:50271
  competitors.team.name.78 competitors.team.gender.78
1         Bora - Hansgrohe                       male
  competitors.team.nationality.78 competitors.team.country_code.78
1                         Germany                              DEU
     competitors.id.79 competitors.name.79 competitors.gender.79
1 sr:competitor:226826  Postlberger, Lukas                  male
  competitors.nationality.79 competitors.country_code.79 competitors.team.id.79
1                    Austria                         AUT    sr:competitor:50271
  competitors.team.name.79 competitors.team.gender.79
1         Bora - Hansgrohe                       male
  competitors.team.nationality.79 competitors.team.country_code.79
1                         Germany                              DEU
     competitors.id.80 competitors.name.80 competitors.gender.80
1 sr:competitor:252831     Ciccone, Giulio                  male
  competitors.nationality.80 competitors.country_code.80 competitors.team.id.80
1                      Italy                         ITA    sr:competitor:62896
  competitors.team.name.80 competitors.team.gender.80
1           Trek–Segafredo                       male
  competitors.team.nationality.80 competitors.team.country_code.80
1                             USA                              USA
     competitors.id.81   competitors.name.81 competitors.gender.81
1 sr:competitor:246979 Eiking, Odd Christian                  male
  competitors.nationality.81 competitors.country_code.81 competitors.team.id.81
1                     Norway                         NOR    sr:competitor:49122
  competitors.team.name.81 competitors.team.gender.81
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.81 competitors.team.country_code.81
1                         Belgium                              BEL
     competitors.id.82 competitors.name.82 competitors.gender.82
1 sr:competitor:247361  Muhlberger, Gregor                  male
  competitors.nationality.82 competitors.country_code.82 competitors.team.id.82
1                    Austria                         AUT    sr:competitor:50271
  competitors.team.name.82 competitors.team.gender.82
1         Bora - Hansgrohe                       male
  competitors.team.nationality.82 competitors.team.country_code.82
1                         Germany                              DEU
     competitors.id.83 competitors.name.83 competitors.gender.83
1 sr:competitor:318333 Wurtz Schmidt, Mads                  male
  competitors.nationality.83 competitors.country_code.83 competitors.team.id.83
1                    Denmark                         DNK    sr:competitor:33029
  competitors.team.name.83 competitors.team.gender.83
1   Team Katusha - Alpecin                       male
  competitors.team.nationality.83 competitors.team.country_code.83
1                     Switzerland                              CHE
     competitors.id.84 competitors.name.84 competitors.gender.84
1 sr:competitor:318335     Asgreen, Kasper                  male
  competitors.nationality.84 competitors.country_code.84 competitors.team.id.84
1                    Denmark                         DNK    sr:competitor:26520
   competitors.team.name.84 competitors.team.gender.84
1 Deceuninck - Quick - Step                       male
  competitors.team.nationality.84 competitors.team.country_code.84
1                         Belgium                              BEL
     competitors.id.85 competitors.name.85 competitors.gender.85
1 sr:competitor:221492     Goncalves, Jose                  male
  competitors.nationality.85 competitors.country_code.85 competitors.team.id.85
1                   Portugal                         PRT    sr:competitor:33029
  competitors.team.name.85 competitors.team.gender.85
1   Team Katusha - Alpecin                       male
  competitors.team.nationality.85 competitors.team.country_code.85
1                     Switzerland                              CHE
    competitors.id.86 competitors.name.86 competitors.gender.86
1 sr:competitor:69216     Bennett, George                  male
  competitors.nationality.86 competitors.country_code.86 competitors.team.id.86
1                New Zealand                         NZL   sr:competitor:189354
  competitors.team.name.86 competitors.team.gender.86
1       Team Jumbo - Visma                       male
  competitors.team.nationality.86 competitors.team.country_code.86
1                     Netherlands                              NLD
    competitors.id.87   competitors.name.87 competitors.gender.87
1 sr:competitor:66830 Laengen, Vegard Stake                  male
  competitors.nationality.87 competitors.country_code.87 competitors.team.id.87
1                     Norway                         NOR   sr:competitor:310636
  competitors.team.name.87 competitors.team.gender.87
1        UAE Team Emirates                       male
  competitors.team.nationality.87 competitors.team.country_code.87
1            United Arab Emirates                              ARE
    competitors.id.88    competitors.name.88 competitors.gender.88
1 sr:competitor:26697 Sanchez Gil, Luis Leon                  male
  competitors.nationality.88 competitors.country_code.88 competitors.team.id.88
1                      Spain                         ESP    sr:competitor:26598
  competitors.team.name.88 competitors.team.gender.88
1          Astana Pro Team                       male
  competitors.team.nationality.88 competitors.team.country_code.88
1                      Kazakhstan                              KAZ
    competitors.id.89 competitors.name.89 competitors.gender.89
1 sr:competitor:27911       Roux, Anthony                  male
  competitors.nationality.89 competitors.country_code.89 competitors.team.id.89
1                     France                         FRA    sr:competitor:26516
  competitors.team.name.89 competitors.team.gender.89
1           Groupama – FDJ                       male
  competitors.team.nationality.89 competitors.team.country_code.89
1                          France                              FRA
    competitors.id.90 competitors.name.90 competitors.gender.90
1 sr:competitor:27768     Thomas, Geraint                  male
  competitors.nationality.90 competitors.country_code.90 competitors.team.id.90
1              Great Britain                         GBR    sr:competitor:39815
  competitors.team.name.90 competitors.team.gender.90
1               Team Ineos                       male
  competitors.team.nationality.90 competitors.team.country_code.90
1                   Great Britain                              GBR
    competitors.id.91 competitors.name.91 competitors.gender.91
1 sr:competitor:27770     Fuglsang, Jakob                  male
  competitors.nationality.91 competitors.country_code.91 competitors.team.id.91
1                    Denmark                         DNK    sr:competitor:26598
  competitors.team.name.91 competitors.team.gender.91
1          Astana Pro Team                       male
  competitors.team.nationality.91 competitors.team.country_code.91
1                      Kazakhstan                              KAZ
    competitors.id.92 competitors.name.92 competitors.gender.92
1 sr:competitor:27851        Impey, Daryl                  male
  competitors.nationality.92 competitors.country_code.92 competitors.team.id.92
1               South Africa                         ZAF    sr:competitor:62812
  competitors.team.name.92 competitors.team.gender.92
1         Mitchelton-Scott                       male
  competitors.team.nationality.92 competitors.team.country_code.92
1                       Australia                              AUS
    competitors.id.93 competitors.name.93 competitors.gender.93
1 sr:competitor:27883      Kangert, Tanel                  male
  competitors.nationality.93 competitors.country_code.93 competitors.team.id.93
1                    Estonia                         EST    sr:competitor:27747
  competitors.team.name.93 competitors.team.gender.93
1       EF Education First                       male
  competitors.team.nationality.93 competitors.team.country_code.93
1                             USA                              USA
    competitors.id.94   competitors.name.94 competitors.gender.94
1 sr:competitor:27884 Hagen, Edvald Boasson                  male
  competitors.nationality.94 competitors.country_code.94 competitors.team.id.94
1                     Norway                         NOR    sr:competitor:80955
  competitors.team.name.94 competitors.team.gender.94
1      Team Dimension Data                       male
  competitors.team.nationality.94 competitors.team.country_code.94
1                    South Africa                              ZAF
    competitors.id.95 competitors.name.95 competitors.gender.95
1 sr:competitor:27886        Martin, Tony                  male
  competitors.nationality.95 competitors.country_code.95 competitors.team.id.95
1                    Germany                         DEU   sr:competitor:189354
  competitors.team.name.95 competitors.team.gender.95
1       Team Jumbo - Visma                       male
  competitors.team.nationality.95 competitors.team.country_code.95
1                     Netherlands                              NLD
    competitors.id.96 competitors.name.96 competitors.gender.96
1 sr:competitor:27895      Mollema, Bauke                  male
  competitors.nationality.96 competitors.country_code.96 competitors.team.id.96
1                Netherlands                         NLD    sr:competitor:62896
  competitors.team.name.96 competitors.team.gender.96
1           Trek–Segafredo                       male
  competitors.team.nationality.96 competitors.team.country_code.96
1                             USA                              USA
    competitors.id.97 competitors.name.97 competitors.gender.97
1 sr:competitor:27907      Frank, Mathias                  male
  competitors.nationality.97 competitors.country_code.97 competitors.team.id.97
1                Switzerland                         CHE    sr:competitor:26519
  competitors.team.name.97 competitors.team.gender.97
1         Ag2r La Mondiale                       male
  competitors.team.nationality.97 competitors.team.country_code.97
1                          France                              FRA
    competitors.id.98 competitors.name.98 competitors.gender.98
1 sr:competitor:27913      Offredo, Yoann                  male
  competitors.nationality.98 competitors.country_code.98 competitors.team.id.98
1                     France                         FRA    sr:competitor:49122
  competitors.team.name.98 competitors.team.gender.98
1      Wanty Groupe Gobert                       male
  competitors.team.nationality.98 competitors.team.country_code.98
1                         Belgium                              BEL
    competitors.id.99 competitors.name.99 competitors.gender.99
1 sr:competitor:27667       Clarke, Simon                  male
  competitors.nationality.99 competitors.country_code.99 competitors.team.id.99
1                  Australia                         AUS    sr:competitor:27747
  competitors.team.name.99 competitors.team.gender.99
1       EF Education First                       male
  competitors.team.nationality.99 competitors.team.country_code.99
1                             USA                              USA
   competitors.id.100 competitors.name.100 competitors.gender.100
1 sr:competitor:27916       Taaramae, Rein                   male
  competitors.nationality.100 competitors.country_code.100
1                     Estonia                          EST
  competitors.team.id.100 competitors.team.name.100 competitors.team.gender.100
1    sr:competitor:246991            Direct Energie                        male
  competitors.team.nationality.100 competitors.team.country_code.100
1                           France                               FRA
   competitors.id.101 competitors.name.101 competitors.gender.101
1 sr:competitor:27922        Simon, Julien                   male
  competitors.nationality.101 competitors.country_code.101
1                      France                          FRA
  competitors.team.id.101 competitors.team.name.101 competitors.team.gender.101
1     sr:competitor:26495                   Cofidis                        male
  competitors.team.nationality.101 competitors.team.country_code.101
1                           France                               FRA
   competitors.id.102 competitors.name.102 competitors.gender.102
1 sr:competitor:27926        Porte, Richie                   male
  competitors.nationality.102 competitors.country_code.102
1                   Australia                          AUS
  competitors.team.id.102 competitors.team.name.102 competitors.team.gender.102
1     sr:competitor:62896            Trek–Segafredo                        male
  competitors.team.nationality.102 competitors.team.country_code.102
1                              USA                               USA
   competitors.id.103 competitors.name.103 competitors.gender.103
1 sr:competitor:27968        Bouet, Maxime                   male
  competitors.nationality.103 competitors.country_code.103
1                      France                          FRA
  competitors.team.id.103 competitors.team.name.103 competitors.team.gender.103
1    sr:competitor:246989           Fortuneo-Samsic                        male
  competitors.team.nationality.103 competitors.team.country_code.103
1                           France                               FRA
   competitors.id.104 competitors.name.104 competitors.gender.104
1 sr:competitor:27970       Martin, Daniel                   male
  competitors.nationality.104 competitors.country_code.104
1                     Ireland                          IRL
  competitors.team.id.104 competitors.team.name.104 competitors.team.gender.104
1    sr:competitor:310636         UAE Team Emirates                        male
  competitors.team.nationality.104 competitors.team.country_code.104
1             United Arab Emirates                               ARE
   competitors.id.105 competitors.name.105 competitors.gender.105
1 sr:competitor:41621         Kluge, Roger                   male
  competitors.nationality.105 competitors.country_code.105
1                     Germany                          DEU
  competitors.team.id.105 competitors.team.name.105 competitors.team.gender.105
1     sr:competitor:27616              Lotto Soudal                        male
  competitors.team.nationality.105 competitors.team.country_code.105
1                          Belgium                               BEL
   competitors.id.106        competitors.name.106 competitors.gender.106
1 sr:competitor:34530 Faria Da Costa, Rui Alberto                   male
  competitors.nationality.106 competitors.country_code.106
1                    Portugal                          PRT
  competitors.team.id.106 competitors.team.name.106 competitors.team.gender.106
1    sr:competitor:310636         UAE Team Emirates                        male
  competitors.team.nationality.106 competitors.team.country_code.106
1             United Arab Emirates                               ARE
   competitors.id.107 competitors.name.107 competitors.gender.107
1 sr:competitor:44301       Gallopin, Tony                   male
  competitors.nationality.107 competitors.country_code.107
1                      France                          FRA
  competitors.team.id.107 competitors.team.name.107 competitors.team.gender.107
1     sr:competitor:26519          Ag2r La Mondiale                        male
  competitors.team.nationality.107 competitors.team.country_code.107
1                           France                               FRA
   competitors.id.108 competitors.name.108 competitors.gender.108
1 sr:competitor:27762       Cherel, Mikael                   male
  competitors.nationality.108 competitors.country_code.108
1                      France                          FRA
  competitors.team.id.108 competitors.team.name.108 competitors.team.gender.108
1     sr:competitor:26519          Ag2r La Mondiale                        male
  competitors.team.nationality.108 competitors.team.country_code.108
1                           France                               FRA
   competitors.id.109 competitors.name.109 competitors.gender.109
1 sr:competitor:27654       Terpstra, Niki                   male
  competitors.nationality.109 competitors.country_code.109
1                 Netherlands                          NLD
  competitors.team.id.109 competitors.team.name.109 competitors.team.gender.109
1    sr:competitor:246991            Direct Energie                        male
  competitors.team.nationality.109 competitors.team.country_code.109
1                           France                               FRA
   competitors.id.110 competitors.name.110 competitors.gender.110
1 sr:competitor:34405       Amador, Andrey                   male
  competitors.nationality.110 competitors.country_code.110
1                  Costa Rica                          CRI
  competitors.team.id.110 competitors.team.name.110 competitors.team.gender.110
1     sr:competitor:26600             Movistar Team                        male
  competitors.team.nationality.110 competitors.team.country_code.110
1                            Spain                               ESP
   competitors.id.111 competitors.name.111 competitors.gender.111
1 sr:competitor:27072    Burghardt, Marcus                   male
  competitors.nationality.111 competitors.country_code.111
1                     Germany                          DEU
  competitors.team.id.111 competitors.team.name.111 competitors.team.gender.111
1     sr:competitor:50271          Bora - Hansgrohe                        male
  competitors.team.nationality.111 competitors.team.country_code.111
1                          Germany                               DEU
   competitors.id.112 competitors.name.112 competitors.gender.112
1 sr:competitor:26766     Bak, Lars Ytting                   male
  competitors.nationality.112 competitors.country_code.112
1                     Denmark                          DNK
  competitors.team.id.112 competitors.team.name.112 competitors.team.gender.112
1     sr:competitor:80955       Team Dimension Data                        male
  competitors.team.nationality.112 competitors.team.country_code.112
1                     South Africa                               ZAF
   competitors.id.113 competitors.name.113 competitors.gender.113
1 sr:competitor:26792     Nibali, Vincenzo                   male
  competitors.nationality.113 competitors.country_code.113
1                       Italy                          ITA
  competitors.team.id.113 competitors.team.name.113 competitors.team.gender.113
1     sr:competitor:26395          Bahrain - Merida                        male
  competitors.team.nationality.113 competitors.team.country_code.113
1                          Bahrain                               BHR
   competitors.id.114 competitors.name.114 competitors.gender.114
1 sr:competitor:26822        De Kort, Koen                   male
  competitors.nationality.114 competitors.country_code.114
1                 Netherlands                          NLD
  competitors.team.id.114 competitors.team.name.114 competitors.team.gender.114
1     sr:competitor:62896            Trek–Segafredo                        male
  competitors.team.nationality.114 competitors.team.country_code.114
1                              USA                               USA
   competitors.id.115 competitors.name.115 competitors.gender.115
1 sr:competitor:26862      Monfort, Maxime                   male
  competitors.nationality.115 competitors.country_code.115
1                      France                          FRA
  competitors.team.id.115 competitors.team.name.115 competitors.team.gender.115
1     sr:competitor:27616              Lotto Soudal                        male
  competitors.team.nationality.115 competitors.team.country_code.115
1                          Belgium                               BEL
   competitors.id.116 competitors.name.116 competitors.gender.116
1 sr:competitor:26921       Roche, Nicolas                   male
  competitors.nationality.116 competitors.country_code.116
1                     Ireland                          IRL
  competitors.team.id.116 competitors.team.name.116 competitors.team.gender.116
1    sr:competitor:310638               Team Sunweb                        male
  competitors.team.nationality.116 competitors.team.country_code.116
1                      Netherlands                               NLD
   competitors.id.117 competitors.name.117 competitors.gender.117
1 sr:competitor:26931       Erviti, Imanol                   male
  competitors.nationality.117 competitors.country_code.117
1                       Spain                          ESP
  competitors.team.id.117 competitors.team.name.117 competitors.team.gender.117
1     sr:competitor:26600             Movistar Team                        male
  competitors.team.nationality.117 competitors.team.country_code.117
1                            Spain                               ESP
   competitors.id.118 competitors.name.118 competitors.gender.118
1 sr:competitor:26973       Greipel, Andre                   male
  competitors.nationality.118 competitors.country_code.118
1                     Germany                          DEU
  competitors.team.id.118 competitors.team.name.118 competitors.team.gender.118
1    sr:competitor:246989           Fortuneo-Samsic                        male
  competitors.team.nationality.118 competitors.team.country_code.118
1                           France                               FRA
   competitors.id.119 competitors.name.119 competitors.gender.119
1 sr:competitor:27050       Moinard, Amael                   male
  competitors.nationality.119 competitors.country_code.119
1                      France                          FRA
  competitors.team.id.119 competitors.team.name.119 competitors.team.gender.119
1    sr:competitor:246989           Fortuneo-Samsic                        male
  competitors.team.nationality.119 competitors.team.country_code.119
1                           France                               FRA
   competitors.id.120 competitors.name.120 competitors.gender.120
1 sr:competitor:27183     Cummings, Steven                   male
  competitors.nationality.120 competitors.country_code.120
1               Great Britain                          GBR
  competitors.team.id.120 competitors.team.name.120 competitors.team.gender.120
1     sr:competitor:80955       Team Dimension Data                        male
  competitors.team.nationality.120 competitors.team.country_code.120
1                     South Africa                               ZAF
   competitors.id.121 competitors.name.121 competitors.gender.121
1 sr:competitor:27623   Van Avermaet, Greg                   male
  competitors.nationality.121 competitors.country_code.121
1                     Belgium                          BEL
  competitors.team.id.121 competitors.team.name.121 competitors.team.gender.121
1     sr:competitor:27981                  CCC Team                        male
  competitors.team.nationality.121 competitors.team.country_code.121
1                           Poland                               POL
   competitors.id.122 competitors.name.122 competitors.gender.122
1 sr:competitor:27345      Uran, Rigoberto                   male
  competitors.nationality.122 competitors.country_code.122
1                    Colombia                          COL
  competitors.team.id.122 competitors.team.name.122 competitors.team.gender.122
1     sr:competitor:27747        EF Education First                        male
  competitors.team.nationality.122 competitors.team.country_code.122
1                              USA                               USA
   competitors.id.123 competitors.name.123 competitors.gender.123
1 sr:competitor:27397      Bonnet, William                   male
  competitors.nationality.123 competitors.country_code.123
1                      France                          FRA
  competitors.team.id.123 competitors.team.name.123 competitors.team.gender.123
1     sr:competitor:26516            Groupama – FDJ                        male
  competitors.team.nationality.123 competitors.team.country_code.123
1                           France                               FRA
   competitors.id.124 competitors.name.124 competitors.gender.124
1 sr:competitor:27407 Langeveld, Sebastian                   male
  competitors.nationality.124 competitors.country_code.124
1                 Netherlands                          NLD
  competitors.team.id.124 competitors.team.name.124 competitors.team.gender.124
1     sr:competitor:27747        EF Education First                        male
  competitors.team.nationality.124 competitors.team.country_code.124
1                              USA                               USA
   competitors.id.125 competitors.name.125 competitors.gender.125
1 sr:competitor:27412       Pauwels, Serge                   male
  competitors.nationality.125 competitors.country_code.125
1                     Belgium                          BEL
  competitors.team.id.125 competitors.team.name.125 competitors.team.gender.125
1     sr:competitor:27981                  CCC Team                        male
  competitors.team.nationality.125 competitors.team.country_code.125
1                           Poland                               POL
   competitors.id.126 competitors.name.126 competitors.gender.126
1 sr:competitor:27446     Kreuziger, Roman                   male
  competitors.nationality.126 competitors.country_code.126
1              Czech Republic                          CZE
  competitors.team.id.126 competitors.team.name.126 competitors.team.gender.126
1     sr:competitor:80955       Team Dimension Data                        male
  competitors.team.nationality.126 competitors.team.country_code.126
1                     South Africa                               ZAF
   competitors.id.127 competitors.name.127 competitors.gender.127
1 sr:competitor:27499      Schaer, Michael                   male
  competitors.nationality.127 competitors.country_code.127
1                 Switzerland                          CHE
  competitors.team.id.127 competitors.team.name.127 competitors.team.gender.127
1     sr:competitor:27981                  CCC Team                        male
  competitors.team.nationality.127 competitors.team.country_code.127
1                           Poland                               POL
   competitors.id.128 competitors.name.128 competitors.gender.128
1 sr:competitor:27603  Ladagnous, Matthieu                   male
  competitors.nationality.128 competitors.country_code.128
1                      France                          FRA
  competitors.team.id.128 competitors.team.name.128 competitors.team.gender.128
1     sr:competitor:26516            Groupama – FDJ                        male
  competitors.team.nationality.128 competitors.team.country_code.128
1                           France                               FRA
   competitors.id.129 competitors.name.129 competitors.gender.129
1 sr:competitor:27620      Devenyns, Dries                   male
  competitors.nationality.129 competitors.country_code.129
1                     Belgium                          BEL
  competitors.team.id.129 competitors.team.name.129 competitors.team.gender.129
1     sr:competitor:26520 Deceuninck - Quick - Step                        male
  competitors.team.nationality.129 competitors.team.country_code.129
1                          Belgium                               BEL
   competitors.id.130 competitors.name.130 competitors.gender.130
1 sr:competitor:35498  Van Garderen, Tejay                   male
  competitors.nationality.130 competitors.country_code.130
1                         USA                          USA
  competitors.team.id.130 competitors.team.name.130 competitors.team.gender.130
1     sr:competitor:27747        EF Education First                        male
  competitors.team.nationality.130 competitors.team.country_code.130
1                              USA                               USA
   competitors.id.131 competitors.name.131 competitors.gender.131
1 sr:competitor:34406          Oss, Daniel                   male
  competitors.nationality.131 competitors.country_code.131
1                       Italy                          ITA
  competitors.team.id.131 competitors.team.name.131 competitors.team.gender.131
1     sr:competitor:50271          Bora - Hansgrohe                        male
  competitors.team.nationality.131 competitors.team.country_code.131
1                          Germany                               DEU
   competitors.id.132 competitors.name.132 competitors.gender.132
1 sr:competitor:68002        Haller, Marco                   male
  competitors.nationality.132 competitors.country_code.132
1                     Austria                          AUT
  competitors.team.id.132 competitors.team.name.132 competitors.team.gender.132
1     sr:competitor:33029    Team Katusha - Alpecin                        male
  competitors.team.nationality.132 competitors.team.country_code.132
1                      Switzerland                               CHE
   competitors.id.133 competitors.name.133 competitors.gender.133
1 sr:competitor:50026     Nizzolo, Giacomo                   male
  competitors.nationality.133 competitors.country_code.133
1                       Italy                          ITA
  competitors.team.id.133 competitors.team.name.133 competitors.team.gender.133
1     sr:competitor:80955       Team Dimension Data                        male
  competitors.team.nationality.133 competitors.team.country_code.133
1                     South Africa                               ZAF
   competitors.id.134       competitors.name.134 competitors.gender.134
1 sr:competitor:67711 Henao Montoya, Sergio Luis                   male
  competitors.nationality.134 competitors.country_code.134
1                    Colombia                          COL
  competitors.team.id.134 competitors.team.name.134 competitors.team.gender.134
1    sr:competitor:310636         UAE Team Emirates                        male
  competitors.team.nationality.134 competitors.team.country_code.134
1             United Arab Emirates                               ARE
   competitors.id.135 competitors.name.135 competitors.gender.135
1 sr:competitor:47984      Durbridge, Luke                   male
  competitors.nationality.135 competitors.country_code.135
1                   Australia                          AUS
  competitors.team.id.135 competitors.team.name.135 competitors.team.gender.135
1     sr:competitor:62812          Mitchelton-Scott                        male
  competitors.team.nationality.135 competitors.team.country_code.135
1                        Australia                               AUS
   competitors.id.136 competitors.name.136 competitors.gender.136
1 sr:competitor:47989     Hepburn, Michael                   male
  competitors.nationality.136 competitors.country_code.136
1                   Australia                          AUS
  competitors.team.id.136 competitors.team.name.136 competitors.team.gender.136
1     sr:competitor:62812          Mitchelton-Scott                        male
  competitors.team.nationality.136 competitors.team.country_code.136
1                        Australia                               AUS
   competitors.id.137 competitors.name.137 competitors.gender.137
1 sr:competitor:49209       King, Benjamin                   male
  competitors.nationality.137 competitors.country_code.137
1                         USA                          USA
  competitors.team.id.137 competitors.team.name.137 competitors.team.gender.137
1     sr:competitor:80955       Team Dimension Data                        male
  competitors.team.nationality.137 competitors.team.country_code.137
1                     South Africa                               ZAF
   competitors.id.138 competitors.name.138 competitors.gender.138
1 sr:competitor:49569      Vachon, Florian                   male
  competitors.nationality.138 competitors.country_code.138
1                      France                          FRA
  competitors.team.id.138 competitors.team.name.138 competitors.team.gender.138
1    sr:competitor:246989           Fortuneo-Samsic                        male
  competitors.team.nationality.138 competitors.team.country_code.138
1                           France                               FRA
   competitors.id.139  competitors.name.139 competitors.gender.139
1 sr:competitor:49953 de Marchi, Alessandro                   male
  competitors.nationality.139 competitors.country_code.139
1                       Italy                          ITA
  competitors.team.id.139 competitors.team.name.139 competitors.team.gender.139
1     sr:competitor:27981                  CCC Team                        male
  competitors.team.nationality.139 competitors.team.country_code.139
1                           Poland                               POL
   competitors.id.140 competitors.name.140 competitors.gender.140
1 sr:competitor:49955    Pasqualon, Andrea                   male
  competitors.nationality.140 competitors.country_code.140
1                       Italy                          ITA
  competitors.team.id.140 competitors.team.name.140 competitors.team.gender.140
1     sr:competitor:49122       Wanty Groupe Gobert                        male
  competitors.team.nationality.140 competitors.team.country_code.140
1                          Belgium                               BEL
   competitors.id.141 competitors.name.141 competitors.gender.141
1 sr:competitor:50044      Quintana, Nairo                   male
  competitors.nationality.141 competitors.country_code.141
1                    Colombia                          COL
  competitors.team.id.141 competitors.team.name.141 competitors.team.gender.141
1     sr:competitor:26600             Movistar Team                        male
  competitors.team.nationality.141 competitors.team.country_code.141
1                            Spain                               ESP
   competitors.id.142 competitors.name.142 competitors.gender.142
1 sr:competitor:50032        Edet, Nicolas                   male
  competitors.nationality.142 competitors.country_code.142
1                      France                          FRA
  competitors.team.id.142 competitors.team.name.142 competitors.team.gender.142
1     sr:competitor:26495                   Cofidis                        male
  competitors.team.nationality.142 competitors.team.country_code.142
1                           France                               FRA
   competitors.id.143 competitors.name.143 competitors.gender.143
1 sr:competitor:50287   Landa Meana, Mikel                   male
  competitors.nationality.143 competitors.country_code.143
1                       Spain                          ESP
  competitors.team.id.143 competitors.team.name.143 competitors.team.gender.143
1     sr:competitor:26600             Movistar Team                        male
  competitors.team.nationality.143 competitors.team.country_code.143
1                            Spain                               ESP
   competitors.id.144 competitors.name.144 competitors.gender.144
1 sr:competitor:50048         Tratnik, Jan                   male
  competitors.nationality.144 competitors.country_code.144
1                    Slovenia                          SVN
  competitors.team.id.144 competitors.team.name.144 competitors.team.gender.144
1     sr:competitor:26395          Bahrain - Merida                        male
  competitors.team.nationality.144 competitors.team.country_code.144
1                          Bahrain                               BHR
   competitors.id.145 competitors.name.145 competitors.gender.145
1 sr:competitor:50313    van Melsen, Kevin                   male
  competitors.nationality.145 competitors.country_code.145
1                     Belgium                          BEL
  competitors.team.id.145 competitors.team.name.145 competitors.team.gender.145
1     sr:competitor:49122       Wanty Groupe Gobert                        male
  competitors.team.nationality.145 competitors.team.country_code.145
1                          Belgium                               BEL
   competitors.id.146 competitors.name.146 competitors.gender.146
1 sr:competitor:50588    Debusschere, Jens                   male
  competitors.nationality.146 competitors.country_code.146
1                     Belgium                          BEL
  competitors.team.id.146 competitors.team.name.146 competitors.team.gender.146
1     sr:competitor:33029    Team Katusha - Alpecin                        male
  competitors.team.nationality.146 competitors.team.country_code.146
1                      Switzerland                               CHE
   competitors.id.147 competitors.name.147 competitors.gender.147
1 sr:competitor:50710 Herrada Lopez, Jesus                   male
  competitors.nationality.147 competitors.country_code.147
1                       Spain                          ESP
  competitors.team.id.147 competitors.team.name.147 competitors.team.gender.147
1     sr:competitor:26495                   Cofidis                        male
  competitors.team.nationality.147 competitors.team.country_code.147
1                           France                               FRA
   competitors.id.148 competitors.name.148 competitors.gender.148
1 sr:competitor:51780        Bilbao, Pello                   male
  competitors.nationality.148 competitors.country_code.148
1                       Spain                          ESP
  competitors.team.id.148 competitors.team.name.148 competitors.team.gender.148
1     sr:competitor:26598           Astana Pro Team                        male
  competitors.team.nationality.148 competitors.team.country_code.148
1                       Kazakhstan                               KAZ
   competitors.id.149     competitors.name.149 competitors.gender.149
1 sr:competitor:55679 Juul-Jensen, Christopher                   male
  competitors.nationality.149 competitors.country_code.149
1                     Denmark                          DNK
  competitors.team.id.149 competitors.team.name.149 competitors.team.gender.149
1     sr:competitor:62812          Mitchelton-Scott                        male
  competitors.team.nationality.149 competitors.team.country_code.149
1                        Australia                               AUS
   competitors.id.150 competitors.name.150 competitors.gender.150
1 sr:competitor:54471      Trentin, Matteo                   male
  competitors.nationality.150 competitors.country_code.150
1                       Italy                          ITA
  competitors.team.id.150 competitors.team.name.150 competitors.team.gender.150
1     sr:competitor:62812          Mitchelton-Scott                        male
  competitors.team.nationality.150 competitors.team.country_code.150
1                        Australia                               AUS
   competitors.id.151 competitors.name.151 competitors.gender.151
1 sr:competitor:62830     Kelderman, Wilco                   male
  competitors.nationality.151 competitors.country_code.151
1                 Netherlands                          NLD
  competitors.team.id.151 competitors.team.name.151 competitors.team.gender.151
1    sr:competitor:310638               Team Sunweb                        male
  competitors.team.nationality.151 competitors.team.country_code.151
1                      Netherlands                               NLD
   competitors.id.152 competitors.name.152 competitors.gender.152
1 sr:competitor:50288  Kwiatkowski, Michal                   male
  competitors.nationality.152 competitors.country_code.152
1                      Poland                          POL
  competitors.team.id.152 competitors.team.name.152 competitors.team.gender.152
1     sr:competitor:39815                Team Ineos                        male
  competitors.team.nationality.152 competitors.team.country_code.152
1                    Great Britain                               GBR
   competitors.id.153 competitors.name.153 competitors.gender.153
1 sr:competitor:50285           Rowe, Luke                   male
  competitors.nationality.153 competitors.country_code.153
1               Great Britain                          GBR
  competitors.team.id.153 competitors.team.name.153 competitors.team.gender.153
1     sr:competitor:39815                Team Ineos                        male
  competitors.team.nationality.153 competitors.team.country_code.153
1                    Great Britain                               GBR
   competitors.id.154 competitors.name.154 competitors.gender.154
1 sr:competitor:49690      Caruso, Damiano                   male
  competitors.nationality.154 competitors.country_code.154
1                       Italy                          ITA
  competitors.team.id.154 competitors.team.name.154 competitors.team.gender.154
1     sr:competitor:26395          Bahrain - Merida                        male
  competitors.team.nationality.154 competitors.team.country_code.154
1                          Bahrain                               BHR
   competitors.id.155 competitors.name.155 competitors.gender.155
1 sr:competitor:39813       Sicard, Romain                   male
  competitors.nationality.155 competitors.country_code.155
1                      France                          FRA
  competitors.team.id.155 competitors.team.name.155 competitors.team.gender.155
1    sr:competitor:246991            Direct Energie                        male
  competitors.team.nationality.155 competitors.team.country_code.155
1                           France                               FRA
   competitors.id.156 competitors.name.156 competitors.gender.156
1 sr:competitor:41433  Kristoff, Alexander                   male
  competitors.nationality.156 competitors.country_code.156
1                      Norway                          NOR
  competitors.team.id.156 competitors.team.name.156 competitors.team.gender.156
1    sr:competitor:310636         UAE Team Emirates                        male
  competitors.team.nationality.156 competitors.team.country_code.156
1             United Arab Emirates                               ARE
   competitors.id.157 competitors.name.157 competitors.gender.157
1 sr:competitor:35401     De Gendt, Thomas                   male
  competitors.nationality.157 competitors.country_code.157
1                     Belgium                          BEL
  competitors.team.id.157 competitors.team.name.157 competitors.team.gender.157
1     sr:competitor:27616              Lotto Soudal                        male
  competitors.team.nationality.157 competitors.team.country_code.157
1                          Belgium                               BEL
   competitors.id.158 competitors.name.158 competitors.gender.158
1 sr:competitor:44092        Viviani, Elia                   male
  competitors.nationality.158 competitors.country_code.158
1                       Italy                          ITA
  competitors.team.id.158 competitors.team.name.158 competitors.team.gender.158
1     sr:competitor:26520 Deceuninck - Quick - Step                        male
  competitors.team.nationality.158 competitors.team.country_code.158
1                          Belgium                               BEL
   competitors.id.159     competitors.name.159 competitors.gender.159
1 sr:competitor:35470 Izagirre Insausti, Gorka                   male
  competitors.nationality.159 competitors.country_code.159
1                       Spain                          ESP
  competitors.team.id.159 competitors.team.name.159 competitors.team.gender.159
1     sr:competitor:26598           Astana Pro Team                        male
  competitors.team.nationality.159 competitors.team.country_code.159
1                       Kazakhstan                               KAZ
   competitors.id.160 competitors.name.160 competitors.gender.160
1 sr:competitor:35557       Geschke, Simon                   male
  competitors.nationality.160 competitors.country_code.160
1                     Germany                          DEU
  competitors.team.id.160 competitors.team.name.160 competitors.team.gender.160
1     sr:competitor:27981                  CCC Team                        male
  competitors.team.nationality.160 competitors.team.country_code.160
1                           Poland                               POL
   competitors.id.161 competitors.name.161 competitors.gender.161
1 sr:competitor:35558        Poels, Wouter                   male
  competitors.nationality.161 competitors.country_code.161
1                 Netherlands                          NLD
  competitors.team.id.161 competitors.team.name.161 competitors.team.gender.161
1     sr:competitor:39815                Team Ineos                        male
  competitors.team.nationality.161 competitors.team.country_code.161
1                    Great Britain                               GBR
   competitors.id.162 competitors.name.162 competitors.gender.162
1 sr:competitor:36863    Moerkoev, Michael                   male
  competitors.nationality.162 competitors.country_code.162
1                     Denmark                          DNK
  competitors.team.id.162 competitors.team.name.162 competitors.team.gender.162
1     sr:competitor:26520 Deceuninck - Quick - Step                        male
  competitors.team.nationality.162 competitors.team.country_code.162
1                          Belgium                               BEL
   competitors.id.163                  competitors.name.163
1 sr:competitor:50262 Santos Simoes Oliveira, Nelson Filipe
  competitors.gender.163 competitors.nationality.163
1                   male                    Portugal
  competitors.country_code.163 competitors.team.id.163
1                          PRT     sr:competitor:26600
  competitors.team.name.163 competitors.team.gender.163
1             Movistar Team                        male
  competitors.team.nationality.163 competitors.team.country_code.163
1                            Spain                               ESP
   competitors.id.164 competitors.name.164 competitors.gender.164
1 sr:competitor:39816       Pinot, Thibaut                   male
  competitors.nationality.164 competitors.country_code.164
1                      France                          FRA
  competitors.team.id.164 competitors.team.name.164 competitors.team.gender.164
1     sr:competitor:26516            Groupama – FDJ                        male
  competitors.team.nationality.164 competitors.team.country_code.164
1                           France                               FRA
   competitors.id.165 competitors.name.165 competitors.gender.165
1 sr:competitor:50283     Colbrelli, Sonny                   male
  competitors.nationality.165 competitors.country_code.165
1                       Italy                          ITA
  competitors.team.id.165 competitors.team.name.165 competitors.team.gender.165
1     sr:competitor:26395          Bahrain - Merida                        male
  competitors.team.nationality.165 competitors.team.country_code.165
1                          Bahrain                               BHR
   competitors.id.166          competitors.name.166 competitors.gender.166
1 sr:competitor:39819 Castroviejo, Nicolas Jonathan                   male
  competitors.nationality.166 competitors.country_code.166
1                       Spain                          ESP
  competitors.team.id.166 competitors.team.name.166 competitors.team.gender.166
1     sr:competitor:39815                Team Ineos                        male
  competitors.team.nationality.166 competitors.team.country_code.166
1                    Great Britain                               GBR
   competitors.id.167 competitors.name.167 competitors.gender.167
1 sr:competitor:39823         Sagan, Peter                   male
  competitors.nationality.167 competitors.country_code.167
1                    Slovakia                          SVK
  competitors.team.id.167 competitors.team.name.167 competitors.team.gender.167
1     sr:competitor:50271          Bora - Hansgrohe                        male
  competitors.team.nationality.167 competitors.team.country_code.167
1                          Germany                               DEU
   competitors.id.168 competitors.name.168 competitors.gender.168
1 sr:competitor:39828    Matthews, Michael                   male
  competitors.nationality.168 competitors.country_code.168
1                   Australia                          AUS
  competitors.team.id.168 competitors.team.name.168 competitors.team.gender.168
1    sr:competitor:310638               Team Sunweb                        male
  competitors.team.nationality.168 competitors.team.country_code.168
1                      Netherlands                               NLD
   competitors.id.169 competitors.name.169 competitors.gender.169
1 sr:competitor:39829        Dennis, Rohan                   male
  competitors.nationality.169 competitors.country_code.169
1                   Australia                          AUS
  competitors.team.id.169 competitors.team.name.169 competitors.team.gender.169
1     sr:competitor:26395          Bahrain - Merida                        male
  competitors.team.nationality.169 competitors.team.country_code.169
1                          Bahrain                               BHR
   competitors.id.170 competitors.name.170 competitors.gender.170
1 sr:competitor:41623     Keukeleire, Jens                   male
  competitors.nationality.170 competitors.country_code.170
1                     Belgium                          BEL
  competitors.team.id.170 competitors.team.name.170 competitors.team.gender.170
1     sr:competitor:27616              Lotto Soudal                        male
  competitors.team.nationality.170 competitors.team.country_code.170
1                          Belgium                               BEL
   competitors.id.171 competitors.name.171 competitors.gender.171
1 sr:competitor:41444       Felline, Fabio                   male
  competitors.nationality.171 competitors.country_code.171
1                       Italy                          ITA
  competitors.team.id.171 competitors.team.name.171 competitors.team.gender.171
1     sr:competitor:62896            Trek–Segafredo                        male
  competitors.team.nationality.171 competitors.team.country_code.171
1                              USA                               USA
   competitors.id.172 competitors.name.172 competitors.gender.172
1 sr:competitor:41446   Kruijswijk, Steven                   male
  competitors.nationality.172 competitors.country_code.172
1                 Netherlands                          NLD
  competitors.team.id.172 competitors.team.name.172 competitors.team.gender.172
1    sr:competitor:189354        Team Jumbo - Visma                        male
  competitors.team.nationality.172 competitors.team.country_code.172
1                      Netherlands                               NLD
   competitors.id.173 competitors.name.173 competitors.gender.173
1 sr:competitor:42654   Delaplace, Anthony                   male
  competitors.nationality.173 competitors.country_code.173
1                      France                          FRA
  competitors.team.id.173 competitors.team.name.173 competitors.team.gender.173
1    sr:competitor:246989           Fortuneo-Samsic                        male
  competitors.team.nationality.173 competitors.team.country_code.173
1                           France                               FRA
   competitors.id.174 competitors.name.174 competitors.gender.174
1 sr:competitor:50281        Dowsett, Alex                   male
  competitors.nationality.174 competitors.country_code.174
1               Great Britain                          GBR
  competitors.team.id.174 competitors.team.name.174 competitors.team.gender.174
1     sr:competitor:33029    Team Katusha - Alpecin                        male
  competitors.team.nationality.174 competitors.team.country_code.174
1                      Switzerland                               CHE
    competitors.id.175 competitors.name.175 competitors.gender.175
1 sr:competitor:532557            Bol, Cees                   male
  competitors.nationality.175 competitors.country_code.175
1                 Netherlands                          NLD
  competitors.team.id.175 competitors.team.name.175 competitors.team.gender.175
1    sr:competitor:310638               Team Sunweb                        male
  competitors.team.nationality.175 competitors.team.country_code.175
1                      Netherlands                               NLD
              teams.id         teams.name teams.gender teams.nationality
1 sr:competitor:189354 Team Jumbo - Visma         male       Netherlands
  teams.country_code teams.result.team_time teams.result.team_time_ranking
1                NLD               00:28.57                              1
           teams.id.1 teams.name.1 teams.gender.1 teams.nationality.1
1 sr:competitor:39815   Team Ineos           male       Great Britain
  teams.country_code.1 teams.result.team_time.1
1                  GBR                +00:00.20
  teams.result.team_time_ranking.1          teams.id.2
1                                2 sr:competitor:26520
               teams.name.2 teams.gender.2 teams.nationality.2
1 Deceuninck - Quick - Step           male             Belgium
  teams.country_code.2 teams.result.team_time.2
1                  BEL                +00:00.21
  teams.result.team_time_ranking.2           teams.id.3 teams.name.3
1                                3 sr:competitor:310638  Team Sunweb
  teams.gender.3 teams.nationality.3 teams.country_code.3
1           male         Netherlands                  NLD
  teams.result.team_time.3 teams.result.team_time_ranking.3          teams.id.4
1                +00:00.26                                4 sr:competitor:33029
            teams.name.4 teams.gender.4 teams.nationality.4
1 Team Katusha - Alpecin           male         Switzerland
  teams.country_code.4 teams.result.team_time.4
1                  CHE                +00:00.26
  teams.result.team_time_ranking.4          teams.id.5       teams.name.5
1                                5 sr:competitor:27747 EF Education First
  teams.gender.5 teams.nationality.5 teams.country_code.5
1           male                 USA                  USA
  teams.result.team_time.5 teams.result.team_time_ranking.5          teams.id.6
1                +00:00.28                                6 sr:competitor:27981
  teams.name.6 teams.gender.6 teams.nationality.6 teams.country_code.6
1     CCC Team           male              Poland                  POL
  teams.result.team_time.6 teams.result.team_time_ranking.6          teams.id.7
1                +00:00.31                                7 sr:competitor:26516
    teams.name.7 teams.gender.7 teams.nationality.7 teams.country_code.7
1 Groupama – FDJ           male              France                  FRA
  teams.result.team_time.7 teams.result.team_time_ranking.7          teams.id.8
1                +00:00.32                                8 sr:competitor:26395
      teams.name.8 teams.gender.8 teams.nationality.8 teams.country_code.8
1 Bahrain - Merida           male             Bahrain                  BHR
  teams.result.team_time.8 teams.result.team_time_ranking.8          teams.id.9
1                +00:00.36                                9 sr:competitor:26598
     teams.name.9 teams.gender.9 teams.nationality.9 teams.country_code.9
1 Astana Pro Team           male          Kazakhstan                  KAZ
  teams.result.team_time.9 teams.result.team_time_ranking.9         teams.id.10
1                +00:00.41                               10 sr:competitor:62812
     teams.name.10 teams.gender.10 teams.nationality.10 teams.country_code.10
1 Mitchelton-Scott            male            Australia                   AUS
  teams.result.team_time.10 teams.result.team_time_ranking.10
1                 +00:00.41                                11
          teams.id.11    teams.name.11 teams.gender.11 teams.nationality.11
1 sr:competitor:50271 Bora - Hansgrohe            male              Germany
  teams.country_code.11 teams.result.team_time.11
1                   DEU                 +00:00.46
  teams.result.team_time_ranking.11         teams.id.12 teams.name.12
1                                12 sr:competitor:26495       Cofidis
  teams.gender.12 teams.nationality.12 teams.country_code.12
1            male               France                   FRA
  teams.result.team_time.12 teams.result.team_time_ranking.12
1                 +00:00.53                                13
          teams.id.13       teams.name.13 teams.gender.13 teams.nationality.13
1 sr:competitor:80955 Team Dimension Data            male         South Africa
  teams.country_code.13 teams.result.team_time.13
1                   ZAF                 +00:00.54
  teams.result.team_time_ranking.13         teams.id.14 teams.name.14
1                                14 sr:competitor:27616  Lotto Soudal
  teams.gender.14 teams.nationality.14 teams.country_code.14
1            male              Belgium                   BEL
  teams.result.team_time.14 teams.result.team_time_ranking.14
1                 +00:00.59                                15
           teams.id.15     teams.name.15 teams.gender.15 teams.nationality.15
1 sr:competitor:310636 UAE Team Emirates            male United Arab Emirates
  teams.country_code.15 teams.result.team_time.15
1                   ARE                 +00:01.03
  teams.result.team_time_ranking.15         teams.id.16 teams.name.16
1                                16 sr:competitor:26600 Movistar Team
  teams.gender.16 teams.nationality.16 teams.country_code.16
1            male                Spain                   ESP
  teams.result.team_time.16 teams.result.team_time_ranking.16
1                 +00:01.05                                17
          teams.id.17  teams.name.17 teams.gender.17 teams.nationality.17
1 sr:competitor:62896 Trek–Segafredo            male                  USA
  teams.country_code.17 teams.result.team_time.17
1                   USA                 +00:01.18
  teams.result.team_time_ranking.17         teams.id.18    teams.name.18
1                                18 sr:competitor:26519 Ag2r La Mondiale
  teams.gender.18 teams.nationality.18 teams.country_code.18
1            male               France                   FRA
  teams.result.team_time.18 teams.result.team_time_ranking.18
1                 +00:01.19                                19
           teams.id.19  teams.name.19 teams.gender.19 teams.nationality.19
1 sr:competitor:246991 Direct Energie            male               France
  teams.country_code.19 teams.result.team_time.19
1                   FRA                 +00:01.42
  teams.result.team_time_ranking.19          teams.id.20   teams.name.20
1                                20 sr:competitor:246989 Fortuneo-Samsic
  teams.gender.20 teams.nationality.20 teams.country_code.20
1            male               France                   FRA
  teams.result.team_time.20 teams.result.team_time_ranking.20
1                 +00:01.51                                21
          teams.id.21       teams.name.21 teams.gender.21 teams.nationality.21
1 sr:competitor:49122 Wanty Groupe Gobert            male              Belgium
  teams.country_code.21 teams.result.team_time.21
1                   BEL                 +00:01.58
  teams.result.team_time_ranking.21
1                                22
```

```r
stage_info <- data.frame(tdf[[2]]$stage) %>%
  select(description:single_event)
```


```r
people <- lapply(tdf[[2]]$stage$competitors, data.frame) %>%
  bind_rows() %>%
  mutate(description = "Stage 2")
```


```r
team_info <- lapply(tdf[[2]]$stage$teams, data.frame) %>%
  bind_rows() %>%
  rename(team.id = id)
```


```r
people_teams <- full_join(people, team_info, by = "team.id")
data <- full_join(people_teams, stage_info, by = "description") 
data
```

```
                      id                                 name.x gender.x
1    sr:competitor:26658                    Valverde, Alejandro     male
2   sr:competitor:135930                             Haig, Jack     male
3   sr:competitor:123892                            Yates, Adam     male
4   sr:competitor:310616                         Scully, Thomas     male
5   sr:competitor:123378                         Zakarin, Ilnur     male
6   sr:competitor:135922                            Ewan, Caleb     male
7   sr:competitor:135938                         Mohoric, Matej     male
8   sr:competitor:135924                    Alaphilippe, Julian     male
9   sr:competitor:135926                            Zabel, Rick     male
10  sr:competitor:146106                        Stuyven, Jasper     male
11  sr:competitor:135946                       Bettiol, Alberto     male
12  sr:competitor:123886                 Kragh Andersen, Soeren     male
13  sr:competitor:146110                      van Baarle, Dylan     male
14  sr:competitor:147128                     Bonifazio, Niccolo     male
15  sr:competitor:198734                     Rossetto, Stephane     male
16  sr:competitor:208169                    Laporte, Christophe     male
17  sr:competitor:197808                          Benoot, Tiesj     male
18  sr:competitor:171236                       de Buyst, Jasper     male
19  sr:competitor:196712                           Teuns, Dylan     male
20  sr:competitor:174908                         Woods, Michael     male
21  sr:competitor:123888                           Yates, Simon     male
22  sr:competitor:123880              Valgren Andersen, Michael     male
23  sr:competitor:199422                           Kung, Stefan     male
24   sr:competitor:92871             Verona Quintanilla, Carlos     male
25   sr:competitor:78671                           Molard, Rudy     male
26   sr:competitor:80287                           Wellens, Tim     male
27   sr:competitor:80289                            Houle, Hugo     male
28   sr:competitor:81383          Janse van Rensburg, Reinhardt     male
29   sr:competitor:88952                       Gougeard, Alexis     male
30   sr:competitor:82007                             Aru, Fabio     male
31   sr:competitor:91766                        Barguil, Warren     male
32   sr:competitor:91768                     Vuillermoz, Alexis     male
33   sr:competitor:93161                         Lampaert, Yves     male
34  sr:competitor:123874                   Nielsen, Magnus Cort     male
35   sr:competitor:93179                          Arndt, Nikias     male
36   sr:competitor:93813                       Lutsenko, Alexey     male
37   sr:competitor:93811                 Fraile Matarranz, Omar     male
38   sr:competitor:94613                   Perichon, Pierre-Luc     male
39   sr:competitor:95635                 Reichenbach, Sebastien     male
40  sr:competitor:146340                             Haga, Chad     male
41  sr:competitor:101459                       Berhane, Natnael     male
42  sr:competitor:123856                    Bystroem, Sven Erik     male
43  sr:competitor:318361                 Schachmann, Maximilian     male
44  sr:competitor:226716                          Skujins, Toms     male
45   sr:competitor:67014                         Bardet, Romain     male
46  sr:competitor:310574                     Mas Nicolau, Enric     male
47  sr:competitor:249457                           Politt, Nils     male
48  sr:competitor:246981                      Calmejane, Lilian     male
49  sr:competitor:248863                        Bernard, Julien     male
50  sr:competitor:254335                      Martin, Guillaume     male
51  sr:competitor:313921                           Bernal, Egan     male
52  sr:competitor:282491                       Grellier, Fabien     male
53  sr:competitor:286739                         de Gendt, Aime     male
54  sr:competitor:313919                   Garcia Cortina, Ivan     male
55  sr:competitor:319169                Jansen Groendahl, Amund     male
56  sr:competitor:226972 Richeze Araquistain, Ariel Maximiliano     male
57  sr:competitor:317941                         Kamna, Lennard     male
58  sr:competitor:323145                           Gaudu, David     male
59  sr:competitor:325989                         Perez, Anthony     male
60  sr:competitor:329997                          Gesbert, Elie     male
61  sr:competitor:330003                         Ourselin, Paul     male
62  sr:competitor:353504                         Van Aert, Wout     male
63  sr:competitor:379864                      Cosnefroy, Benoit     male
64  sr:competitor:379848                      Philipsen, Jasper     male
65  sr:competitor:241178                         Bevin, Patrick     male
66  sr:competitor:248853                       de Plus, Laurens     male
67  sr:competitor:198722                        Teunissen, Mike     male
68  sr:competitor:198994                        Turgis, Anthony     male
69  sr:competitor:196754                        Ledanois, Kevin     male
70  sr:competitor:254977                     Wisniowski, Lukasz     male
71  sr:competitor:194902                        Konrad, Patrick     male
72  sr:competitor:219922                     Groenewegen, Dylan     male
73  sr:competitor:197934                        Naesen, Olivier     male
74  sr:competitor:196762                    Soler Gimenez, Marc     male
75  sr:competitor:196774                      Backaert, Fredrik     male
76  sr:competitor:198720                         Rosskopf, Joey     male
77  sr:competitor:250457                         Moscon, Gianni     male
78  sr:competitor:323211                       Meurisse, Xandro     male
79  sr:competitor:201073                      Buchmann, Emanuel     male
80  sr:competitor:226826                     Postlberger, Lukas     male
81  sr:competitor:252831                        Ciccone, Giulio     male
82  sr:competitor:246979                  Eiking, Odd Christian     male
83  sr:competitor:247361                     Muhlberger, Gregor     male
84  sr:competitor:318333                    Wurtz Schmidt, Mads     male
85  sr:competitor:318335                        Asgreen, Kasper     male
86  sr:competitor:221492                        Goncalves, Jose     male
87   sr:competitor:69216                        Bennett, George     male
88   sr:competitor:66830                  Laengen, Vegard Stake     male
89   sr:competitor:26697                 Sanchez Gil, Luis Leon     male
90   sr:competitor:27911                          Roux, Anthony     male
91   sr:competitor:27768                        Thomas, Geraint     male
92   sr:competitor:27770                        Fuglsang, Jakob     male
93   sr:competitor:27851                           Impey, Daryl     male
94   sr:competitor:27883                         Kangert, Tanel     male
95   sr:competitor:27884                  Hagen, Edvald Boasson     male
96   sr:competitor:27886                           Martin, Tony     male
97   sr:competitor:27895                         Mollema, Bauke     male
98   sr:competitor:27907                         Frank, Mathias     male
99   sr:competitor:27913                         Offredo, Yoann     male
100  sr:competitor:27667                          Clarke, Simon     male
101  sr:competitor:27916                         Taaramae, Rein     male
102  sr:competitor:27922                          Simon, Julien     male
103  sr:competitor:27926                          Porte, Richie     male
104  sr:competitor:27968                          Bouet, Maxime     male
105  sr:competitor:27970                         Martin, Daniel     male
106  sr:competitor:41621                           Kluge, Roger     male
107  sr:competitor:34530            Faria Da Costa, Rui Alberto     male
108  sr:competitor:44301                         Gallopin, Tony     male
109  sr:competitor:27762                         Cherel, Mikael     male
110  sr:competitor:27654                         Terpstra, Niki     male
111  sr:competitor:34405                         Amador, Andrey     male
112  sr:competitor:27072                      Burghardt, Marcus     male
113  sr:competitor:26766                       Bak, Lars Ytting     male
114  sr:competitor:26792                       Nibali, Vincenzo     male
115  sr:competitor:26822                          De Kort, Koen     male
116  sr:competitor:26862                        Monfort, Maxime     male
117  sr:competitor:26921                         Roche, Nicolas     male
118  sr:competitor:26931                         Erviti, Imanol     male
119  sr:competitor:26973                         Greipel, Andre     male
120  sr:competitor:27050                         Moinard, Amael     male
121  sr:competitor:27183                       Cummings, Steven     male
122  sr:competitor:27623                     Van Avermaet, Greg     male
123  sr:competitor:27345                        Uran, Rigoberto     male
124  sr:competitor:27397                        Bonnet, William     male
125  sr:competitor:27407                   Langeveld, Sebastian     male
126  sr:competitor:27412                         Pauwels, Serge     male
127  sr:competitor:27446                       Kreuziger, Roman     male
128  sr:competitor:27499                        Schaer, Michael     male
129  sr:competitor:27603                    Ladagnous, Matthieu     male
130  sr:competitor:27620                        Devenyns, Dries     male
131  sr:competitor:35498                    Van Garderen, Tejay     male
132  sr:competitor:34406                            Oss, Daniel     male
133  sr:competitor:68002                          Haller, Marco     male
134  sr:competitor:50026                       Nizzolo, Giacomo     male
135  sr:competitor:67711             Henao Montoya, Sergio Luis     male
136  sr:competitor:47984                        Durbridge, Luke     male
137  sr:competitor:47989                       Hepburn, Michael     male
138  sr:competitor:49209                         King, Benjamin     male
139  sr:competitor:49569                        Vachon, Florian     male
140  sr:competitor:49953                  de Marchi, Alessandro     male
141  sr:competitor:49955                      Pasqualon, Andrea     male
142  sr:competitor:50044                        Quintana, Nairo     male
143  sr:competitor:50032                          Edet, Nicolas     male
144  sr:competitor:50287                     Landa Meana, Mikel     male
145  sr:competitor:50048                           Tratnik, Jan     male
146  sr:competitor:50313                      van Melsen, Kevin     male
147  sr:competitor:50588                      Debusschere, Jens     male
148  sr:competitor:50710                   Herrada Lopez, Jesus     male
149  sr:competitor:51780                          Bilbao, Pello     male
150  sr:competitor:55679               Juul-Jensen, Christopher     male
151  sr:competitor:54471                        Trentin, Matteo     male
152  sr:competitor:62830                       Kelderman, Wilco     male
153  sr:competitor:50288                    Kwiatkowski, Michal     male
154  sr:competitor:50285                             Rowe, Luke     male
155  sr:competitor:49690                        Caruso, Damiano     male
156  sr:competitor:39813                         Sicard, Romain     male
157  sr:competitor:41433                    Kristoff, Alexander     male
158  sr:competitor:35401                       De Gendt, Thomas     male
159  sr:competitor:44092                          Viviani, Elia     male
160  sr:competitor:35470               Izagirre Insausti, Gorka     male
161  sr:competitor:35557                         Geschke, Simon     male
162  sr:competitor:35558                          Poels, Wouter     male
163  sr:competitor:36863                      Moerkoev, Michael     male
164  sr:competitor:50262  Santos Simoes Oliveira, Nelson Filipe     male
165  sr:competitor:39816                         Pinot, Thibaut     male
166  sr:competitor:50283                       Colbrelli, Sonny     male
167  sr:competitor:39819          Castroviejo, Nicolas Jonathan     male
168  sr:competitor:39823                           Sagan, Peter     male
169  sr:competitor:39828                      Matthews, Michael     male
170  sr:competitor:39829                          Dennis, Rohan     male
171  sr:competitor:41623                       Keukeleire, Jens     male
172  sr:competitor:41444                         Felline, Fabio     male
173  sr:competitor:41446                     Kruijswijk, Steven     male
174  sr:competitor:42654                     Delaplace, Anthony     male
175  sr:competitor:50281                          Dowsett, Alex     male
176 sr:competitor:532557                              Bol, Cees     male
     nationality.x country_code.x              team.id
1            Spain            ESP  sr:competitor:26600
2        Australia            AUS  sr:competitor:62812
3    Great Britain            GBR  sr:competitor:62812
4      New Zealand            NZL  sr:competitor:27747
5           Russia            RUS  sr:competitor:33029
6        Australia            AUS  sr:competitor:27616
7         Slovenia            SVN  sr:competitor:26395
8           France            FRA  sr:competitor:26520
9          Germany            DEU  sr:competitor:33029
10         Belgium            BEL  sr:competitor:62896
11           Italy            ITA  sr:competitor:27747
12         Denmark            DNK sr:competitor:310638
13     Netherlands            NLD  sr:competitor:39815
14           Italy            ITA sr:competitor:246991
15          France            FRA  sr:competitor:26495
16          France            FRA  sr:competitor:26495
17         Belgium            BEL  sr:competitor:27616
18         Belgium            BEL  sr:competitor:27616
19         Belgium            BEL  sr:competitor:26395
20          Canada            CAN  sr:competitor:27747
21   Great Britain            GBR  sr:competitor:62812
22         Denmark            DNK  sr:competitor:80955
23     Switzerland            CHE  sr:competitor:26516
24           Spain            ESP  sr:competitor:26600
25          France            FRA  sr:competitor:26516
26         Belgium            BEL  sr:competitor:27616
27          Canada            CAN  sr:competitor:26598
28    South Africa            ZAF  sr:competitor:80955
29          France            FRA  sr:competitor:26519
30           Italy            ITA sr:competitor:310636
31          France            FRA sr:competitor:246989
32          France            FRA  sr:competitor:26519
33         Belgium            BEL  sr:competitor:26520
34         Denmark            DNK  sr:competitor:26598
35         Germany            DEU sr:competitor:310638
36      Kazakhstan            KAZ  sr:competitor:26598
37           Spain            ESP  sr:competitor:26598
38          France            FRA  sr:competitor:26495
39     Switzerland            CHE  sr:competitor:26516
40             USA            USA sr:competitor:310638
41         Eritrea            ERI  sr:competitor:26495
42          Norway            NOR sr:competitor:310636
43         Germany            DEU  sr:competitor:50271
44          Latvia            LVA  sr:competitor:62896
45          France            FRA  sr:competitor:26519
46           Spain            ESP  sr:competitor:26520
47         Germany            DEU  sr:competitor:33029
48          France            FRA sr:competitor:246991
49          France            FRA  sr:competitor:62896
50          France            FRA  sr:competitor:49122
51        Colombia            COL  sr:competitor:39815
52          France            FRA sr:competitor:246991
53         Belgium            BEL  sr:competitor:49122
54           Spain            ESP  sr:competitor:26395
55          Norway            NOR sr:competitor:189354
56       Argentina            ARG  sr:competitor:26520
57         Germany            DEU sr:competitor:310638
58          France            FRA  sr:competitor:26516
59          France            FRA  sr:competitor:26495
60          France            FRA sr:competitor:246989
61          France            FRA sr:competitor:246991
62         Belgium            BEL sr:competitor:189354
63          France            FRA  sr:competitor:26519
64         Belgium            BEL sr:competitor:310636
65     New Zealand            NZL  sr:competitor:27981
66         Belgium            BEL sr:competitor:189354
67     Netherlands            NLD sr:competitor:189354
68          France            FRA sr:competitor:246991
69          France            FRA sr:competitor:246989
70          Poland            POL  sr:competitor:27981
71         Austria            AUT  sr:competitor:50271
72     Netherlands            NLD sr:competitor:189354
73         Belgium            BEL  sr:competitor:26519
74           Spain            ESP  sr:competitor:26600
75         Belgium            BEL  sr:competitor:49122
76             USA            USA  sr:competitor:27981
77           Italy            ITA  sr:competitor:39815
78         Belgium            BEL  sr:competitor:49122
79         Germany            DEU  sr:competitor:50271
80         Austria            AUT  sr:competitor:50271
81           Italy            ITA  sr:competitor:62896
82          Norway            NOR  sr:competitor:49122
83         Austria            AUT  sr:competitor:50271
84         Denmark            DNK  sr:competitor:33029
85         Denmark            DNK  sr:competitor:26520
86        Portugal            PRT  sr:competitor:33029
87     New Zealand            NZL sr:competitor:189354
88          Norway            NOR sr:competitor:310636
89           Spain            ESP  sr:competitor:26598
90          France            FRA  sr:competitor:26516
91   Great Britain            GBR  sr:competitor:39815
92         Denmark            DNK  sr:competitor:26598
93    South Africa            ZAF  sr:competitor:62812
94         Estonia            EST  sr:competitor:27747
95          Norway            NOR  sr:competitor:80955
96         Germany            DEU sr:competitor:189354
97     Netherlands            NLD  sr:competitor:62896
98     Switzerland            CHE  sr:competitor:26519
99          France            FRA  sr:competitor:49122
100      Australia            AUS  sr:competitor:27747
101        Estonia            EST sr:competitor:246991
102         France            FRA  sr:competitor:26495
103      Australia            AUS  sr:competitor:62896
104         France            FRA sr:competitor:246989
105        Ireland            IRL sr:competitor:310636
106        Germany            DEU  sr:competitor:27616
107       Portugal            PRT sr:competitor:310636
108         France            FRA  sr:competitor:26519
109         France            FRA  sr:competitor:26519
110    Netherlands            NLD sr:competitor:246991
111     Costa Rica            CRI  sr:competitor:26600
112        Germany            DEU  sr:competitor:50271
113        Denmark            DNK  sr:competitor:80955
114          Italy            ITA  sr:competitor:26395
115    Netherlands            NLD  sr:competitor:62896
116         France            FRA  sr:competitor:27616
117        Ireland            IRL sr:competitor:310638
118          Spain            ESP  sr:competitor:26600
119        Germany            DEU sr:competitor:246989
120         France            FRA sr:competitor:246989
121  Great Britain            GBR  sr:competitor:80955
122        Belgium            BEL  sr:competitor:27981
123       Colombia            COL  sr:competitor:27747
124         France            FRA  sr:competitor:26516
125    Netherlands            NLD  sr:competitor:27747
126        Belgium            BEL  sr:competitor:27981
127 Czech Republic            CZE  sr:competitor:80955
128    Switzerland            CHE  sr:competitor:27981
129         France            FRA  sr:competitor:26516
130        Belgium            BEL  sr:competitor:26520
131            USA            USA  sr:competitor:27747
132          Italy            ITA  sr:competitor:50271
133        Austria            AUT  sr:competitor:33029
134          Italy            ITA  sr:competitor:80955
135       Colombia            COL sr:competitor:310636
136      Australia            AUS  sr:competitor:62812
137      Australia            AUS  sr:competitor:62812
138            USA            USA  sr:competitor:80955
139         France            FRA sr:competitor:246989
140          Italy            ITA  sr:competitor:27981
141          Italy            ITA  sr:competitor:49122
142       Colombia            COL  sr:competitor:26600
143         France            FRA  sr:competitor:26495
144          Spain            ESP  sr:competitor:26600
145       Slovenia            SVN  sr:competitor:26395
146        Belgium            BEL  sr:competitor:49122
147        Belgium            BEL  sr:competitor:33029
148          Spain            ESP  sr:competitor:26495
149          Spain            ESP  sr:competitor:26598
150        Denmark            DNK  sr:competitor:62812
151          Italy            ITA  sr:competitor:62812
152    Netherlands            NLD sr:competitor:310638
153         Poland            POL  sr:competitor:39815
154  Great Britain            GBR  sr:competitor:39815
155          Italy            ITA  sr:competitor:26395
156         France            FRA sr:competitor:246991
157         Norway            NOR sr:competitor:310636
158        Belgium            BEL  sr:competitor:27616
159          Italy            ITA  sr:competitor:26520
160          Spain            ESP  sr:competitor:26598
161        Germany            DEU  sr:competitor:27981
162    Netherlands            NLD  sr:competitor:39815
163        Denmark            DNK  sr:competitor:26520
164       Portugal            PRT  sr:competitor:26600
165         France            FRA  sr:competitor:26516
166          Italy            ITA  sr:competitor:26395
167          Spain            ESP  sr:competitor:39815
168       Slovakia            SVK  sr:competitor:50271
169      Australia            AUS sr:competitor:310638
170      Australia            AUS  sr:competitor:26395
171        Belgium            BEL  sr:competitor:27616
172          Italy            ITA  sr:competitor:62896
173    Netherlands            NLD sr:competitor:189354
174         France            FRA sr:competitor:246989
175  Great Britain            GBR  sr:competitor:33029
176    Netherlands            NLD sr:competitor:310638
                    team.name team.gender     team.nationality
1               Movistar Team        male                Spain
2            Mitchelton-Scott        male            Australia
3            Mitchelton-Scott        male            Australia
4          EF Education First        male                  USA
5      Team Katusha - Alpecin        male          Switzerland
6                Lotto Soudal        male              Belgium
7            Bahrain - Merida        male              Bahrain
8   Deceuninck - Quick - Step        male              Belgium
9      Team Katusha - Alpecin        male          Switzerland
10             Trek–Segafredo        male                  USA
11         EF Education First        male                  USA
12                Team Sunweb        male          Netherlands
13                 Team Ineos        male        Great Britain
14             Direct Energie        male               France
15                    Cofidis        male               France
16                    Cofidis        male               France
17               Lotto Soudal        male              Belgium
18               Lotto Soudal        male              Belgium
19           Bahrain - Merida        male              Bahrain
20         EF Education First        male                  USA
21           Mitchelton-Scott        male            Australia
22        Team Dimension Data        male         South Africa
23             Groupama – FDJ        male               France
24              Movistar Team        male                Spain
25             Groupama – FDJ        male               France
26               Lotto Soudal        male              Belgium
27            Astana Pro Team        male           Kazakhstan
28        Team Dimension Data        male         South Africa
29           Ag2r La Mondiale        male               France
30          UAE Team Emirates        male United Arab Emirates
31            Fortuneo-Samsic        male               France
32           Ag2r La Mondiale        male               France
33  Deceuninck - Quick - Step        male              Belgium
34            Astana Pro Team        male           Kazakhstan
35                Team Sunweb        male          Netherlands
36            Astana Pro Team        male           Kazakhstan
37            Astana Pro Team        male           Kazakhstan
38                    Cofidis        male               France
39             Groupama – FDJ        male               France
40                Team Sunweb        male          Netherlands
41                    Cofidis        male               France
42          UAE Team Emirates        male United Arab Emirates
43           Bora - Hansgrohe        male              Germany
44             Trek–Segafredo        male                  USA
45           Ag2r La Mondiale        male               France
46  Deceuninck - Quick - Step        male              Belgium
47     Team Katusha - Alpecin        male          Switzerland
48             Direct Energie        male               France
49             Trek–Segafredo        male                  USA
50        Wanty Groupe Gobert        male              Belgium
51                 Team Ineos        male        Great Britain
52             Direct Energie        male               France
53        Wanty Groupe Gobert        male              Belgium
54           Bahrain - Merida        male              Bahrain
55         Team Jumbo - Visma        male          Netherlands
56  Deceuninck - Quick - Step        male              Belgium
57                Team Sunweb        male          Netherlands
58             Groupama – FDJ        male               France
59                    Cofidis        male               France
60            Fortuneo-Samsic        male               France
61             Direct Energie        male               France
62         Team Jumbo - Visma        male          Netherlands
63           Ag2r La Mondiale        male               France
64          UAE Team Emirates        male United Arab Emirates
65                   CCC Team        male               Poland
66         Team Jumbo - Visma        male          Netherlands
67         Team Jumbo - Visma        male          Netherlands
68             Direct Energie        male               France
69            Fortuneo-Samsic        male               France
70                   CCC Team        male               Poland
71           Bora - Hansgrohe        male              Germany
72         Team Jumbo - Visma        male          Netherlands
73           Ag2r La Mondiale        male               France
74              Movistar Team        male                Spain
75        Wanty Groupe Gobert        male              Belgium
76                   CCC Team        male               Poland
77                 Team Ineos        male        Great Britain
78        Wanty Groupe Gobert        male              Belgium
79           Bora - Hansgrohe        male              Germany
80           Bora - Hansgrohe        male              Germany
81             Trek–Segafredo        male                  USA
82        Wanty Groupe Gobert        male              Belgium
83           Bora - Hansgrohe        male              Germany
84     Team Katusha - Alpecin        male          Switzerland
85  Deceuninck - Quick - Step        male              Belgium
86     Team Katusha - Alpecin        male          Switzerland
87         Team Jumbo - Visma        male          Netherlands
88          UAE Team Emirates        male United Arab Emirates
89            Astana Pro Team        male           Kazakhstan
90             Groupama – FDJ        male               France
91                 Team Ineos        male        Great Britain
92            Astana Pro Team        male           Kazakhstan
93           Mitchelton-Scott        male            Australia
94         EF Education First        male                  USA
95        Team Dimension Data        male         South Africa
96         Team Jumbo - Visma        male          Netherlands
97             Trek–Segafredo        male                  USA
98           Ag2r La Mondiale        male               France
99        Wanty Groupe Gobert        male              Belgium
100        EF Education First        male                  USA
101            Direct Energie        male               France
102                   Cofidis        male               France
103            Trek–Segafredo        male                  USA
104           Fortuneo-Samsic        male               France
105         UAE Team Emirates        male United Arab Emirates
106              Lotto Soudal        male              Belgium
107         UAE Team Emirates        male United Arab Emirates
108          Ag2r La Mondiale        male               France
109          Ag2r La Mondiale        male               France
110            Direct Energie        male               France
111             Movistar Team        male                Spain
112          Bora - Hansgrohe        male              Germany
113       Team Dimension Data        male         South Africa
114          Bahrain - Merida        male              Bahrain
115            Trek–Segafredo        male                  USA
116              Lotto Soudal        male              Belgium
117               Team Sunweb        male          Netherlands
118             Movistar Team        male                Spain
119           Fortuneo-Samsic        male               France
120           Fortuneo-Samsic        male               France
121       Team Dimension Data        male         South Africa
122                  CCC Team        male               Poland
123        EF Education First        male                  USA
124            Groupama – FDJ        male               France
125        EF Education First        male                  USA
126                  CCC Team        male               Poland
127       Team Dimension Data        male         South Africa
128                  CCC Team        male               Poland
129            Groupama – FDJ        male               France
130 Deceuninck - Quick - Step        male              Belgium
131        EF Education First        male                  USA
132          Bora - Hansgrohe        male              Germany
133    Team Katusha - Alpecin        male          Switzerland
134       Team Dimension Data        male         South Africa
135         UAE Team Emirates        male United Arab Emirates
136          Mitchelton-Scott        male            Australia
137          Mitchelton-Scott        male            Australia
138       Team Dimension Data        male         South Africa
139           Fortuneo-Samsic        male               France
140                  CCC Team        male               Poland
141       Wanty Groupe Gobert        male              Belgium
142             Movistar Team        male                Spain
143                   Cofidis        male               France
144             Movistar Team        male                Spain
145          Bahrain - Merida        male              Bahrain
146       Wanty Groupe Gobert        male              Belgium
147    Team Katusha - Alpecin        male          Switzerland
148                   Cofidis        male               France
149           Astana Pro Team        male           Kazakhstan
150          Mitchelton-Scott        male            Australia
151          Mitchelton-Scott        male            Australia
152               Team Sunweb        male          Netherlands
153                Team Ineos        male        Great Britain
154                Team Ineos        male        Great Britain
155          Bahrain - Merida        male              Bahrain
156            Direct Energie        male               France
157         UAE Team Emirates        male United Arab Emirates
158              Lotto Soudal        male              Belgium
159 Deceuninck - Quick - Step        male              Belgium
160           Astana Pro Team        male           Kazakhstan
161                  CCC Team        male               Poland
162                Team Ineos        male        Great Britain
163 Deceuninck - Quick - Step        male              Belgium
164             Movistar Team        male                Spain
165            Groupama – FDJ        male               France
166          Bahrain - Merida        male              Bahrain
167                Team Ineos        male        Great Britain
168          Bora - Hansgrohe        male              Germany
169               Team Sunweb        male          Netherlands
170          Bahrain - Merida        male              Bahrain
171              Lotto Soudal        male              Belgium
172            Trek–Segafredo        male                  USA
173        Team Jumbo - Visma        male          Netherlands
174           Fortuneo-Samsic        male               France
175    Team Katusha - Alpecin        male          Switzerland
176               Team Sunweb        male          Netherlands
    team.country_code description                    name.y gender.y
1                 ESP     Stage 2             Movistar Team     male
2                 AUS     Stage 2          Mitchelton-Scott     male
3                 AUS     Stage 2          Mitchelton-Scott     male
4                 USA     Stage 2        EF Education First     male
5                 CHE     Stage 2    Team Katusha - Alpecin     male
6                 BEL     Stage 2              Lotto Soudal     male
7                 BHR     Stage 2          Bahrain - Merida     male
8                 BEL     Stage 2 Deceuninck - Quick - Step     male
9                 CHE     Stage 2    Team Katusha - Alpecin     male
10                USA     Stage 2            Trek–Segafredo     male
11                USA     Stage 2        EF Education First     male
12                NLD     Stage 2               Team Sunweb     male
13                GBR     Stage 2                Team Ineos     male
14                FRA     Stage 2            Direct Energie     male
15                FRA     Stage 2                   Cofidis     male
16                FRA     Stage 2                   Cofidis     male
17                BEL     Stage 2              Lotto Soudal     male
18                BEL     Stage 2              Lotto Soudal     male
19                BHR     Stage 2          Bahrain - Merida     male
20                USA     Stage 2        EF Education First     male
21                AUS     Stage 2          Mitchelton-Scott     male
22                ZAF     Stage 2       Team Dimension Data     male
23                FRA     Stage 2            Groupama – FDJ     male
24                ESP     Stage 2             Movistar Team     male
25                FRA     Stage 2            Groupama – FDJ     male
26                BEL     Stage 2              Lotto Soudal     male
27                KAZ     Stage 2           Astana Pro Team     male
28                ZAF     Stage 2       Team Dimension Data     male
29                FRA     Stage 2          Ag2r La Mondiale     male
30                ARE     Stage 2         UAE Team Emirates     male
31                FRA     Stage 2           Fortuneo-Samsic     male
32                FRA     Stage 2          Ag2r La Mondiale     male
33                BEL     Stage 2 Deceuninck - Quick - Step     male
34                KAZ     Stage 2           Astana Pro Team     male
35                NLD     Stage 2               Team Sunweb     male
36                KAZ     Stage 2           Astana Pro Team     male
37                KAZ     Stage 2           Astana Pro Team     male
38                FRA     Stage 2                   Cofidis     male
39                FRA     Stage 2            Groupama – FDJ     male
40                NLD     Stage 2               Team Sunweb     male
41                FRA     Stage 2                   Cofidis     male
42                ARE     Stage 2         UAE Team Emirates     male
43                DEU     Stage 2          Bora - Hansgrohe     male
44                USA     Stage 2            Trek–Segafredo     male
45                FRA     Stage 2          Ag2r La Mondiale     male
46                BEL     Stage 2 Deceuninck - Quick - Step     male
47                CHE     Stage 2    Team Katusha - Alpecin     male
48                FRA     Stage 2            Direct Energie     male
49                USA     Stage 2            Trek–Segafredo     male
50                BEL     Stage 2       Wanty Groupe Gobert     male
51                GBR     Stage 2                Team Ineos     male
52                FRA     Stage 2            Direct Energie     male
53                BEL     Stage 2       Wanty Groupe Gobert     male
54                BHR     Stage 2          Bahrain - Merida     male
55                NLD     Stage 2        Team Jumbo - Visma     male
56                BEL     Stage 2 Deceuninck - Quick - Step     male
57                NLD     Stage 2               Team Sunweb     male
58                FRA     Stage 2            Groupama – FDJ     male
59                FRA     Stage 2                   Cofidis     male
60                FRA     Stage 2           Fortuneo-Samsic     male
61                FRA     Stage 2            Direct Energie     male
62                NLD     Stage 2        Team Jumbo - Visma     male
63                FRA     Stage 2          Ag2r La Mondiale     male
64                ARE     Stage 2         UAE Team Emirates     male
65                POL     Stage 2                  CCC Team     male
66                NLD     Stage 2        Team Jumbo - Visma     male
67                NLD     Stage 2        Team Jumbo - Visma     male
68                FRA     Stage 2            Direct Energie     male
69                FRA     Stage 2           Fortuneo-Samsic     male
70                POL     Stage 2                  CCC Team     male
71                DEU     Stage 2          Bora - Hansgrohe     male
72                NLD     Stage 2        Team Jumbo - Visma     male
73                FRA     Stage 2          Ag2r La Mondiale     male
74                ESP     Stage 2             Movistar Team     male
75                BEL     Stage 2       Wanty Groupe Gobert     male
76                POL     Stage 2                  CCC Team     male
77                GBR     Stage 2                Team Ineos     male
78                BEL     Stage 2       Wanty Groupe Gobert     male
79                DEU     Stage 2          Bora - Hansgrohe     male
80                DEU     Stage 2          Bora - Hansgrohe     male
81                USA     Stage 2            Trek–Segafredo     male
82                BEL     Stage 2       Wanty Groupe Gobert     male
83                DEU     Stage 2          Bora - Hansgrohe     male
84                CHE     Stage 2    Team Katusha - Alpecin     male
85                BEL     Stage 2 Deceuninck - Quick - Step     male
86                CHE     Stage 2    Team Katusha - Alpecin     male
87                NLD     Stage 2        Team Jumbo - Visma     male
88                ARE     Stage 2         UAE Team Emirates     male
89                KAZ     Stage 2           Astana Pro Team     male
90                FRA     Stage 2            Groupama – FDJ     male
91                GBR     Stage 2                Team Ineos     male
92                KAZ     Stage 2           Astana Pro Team     male
93                AUS     Stage 2          Mitchelton-Scott     male
94                USA     Stage 2        EF Education First     male
95                ZAF     Stage 2       Team Dimension Data     male
96                NLD     Stage 2        Team Jumbo - Visma     male
97                USA     Stage 2            Trek–Segafredo     male
98                FRA     Stage 2          Ag2r La Mondiale     male
99                BEL     Stage 2       Wanty Groupe Gobert     male
100               USA     Stage 2        EF Education First     male
101               FRA     Stage 2            Direct Energie     male
102               FRA     Stage 2                   Cofidis     male
103               USA     Stage 2            Trek–Segafredo     male
104               FRA     Stage 2           Fortuneo-Samsic     male
105               ARE     Stage 2         UAE Team Emirates     male
106               BEL     Stage 2              Lotto Soudal     male
107               ARE     Stage 2         UAE Team Emirates     male
108               FRA     Stage 2          Ag2r La Mondiale     male
109               FRA     Stage 2          Ag2r La Mondiale     male
110               FRA     Stage 2            Direct Energie     male
111               ESP     Stage 2             Movistar Team     male
112               DEU     Stage 2          Bora - Hansgrohe     male
113               ZAF     Stage 2       Team Dimension Data     male
114               BHR     Stage 2          Bahrain - Merida     male
115               USA     Stage 2            Trek–Segafredo     male
116               BEL     Stage 2              Lotto Soudal     male
117               NLD     Stage 2               Team Sunweb     male
118               ESP     Stage 2             Movistar Team     male
119               FRA     Stage 2           Fortuneo-Samsic     male
120               FRA     Stage 2           Fortuneo-Samsic     male
121               ZAF     Stage 2       Team Dimension Data     male
122               POL     Stage 2                  CCC Team     male
123               USA     Stage 2        EF Education First     male
124               FRA     Stage 2            Groupama – FDJ     male
125               USA     Stage 2        EF Education First     male
126               POL     Stage 2                  CCC Team     male
127               ZAF     Stage 2       Team Dimension Data     male
128               POL     Stage 2                  CCC Team     male
129               FRA     Stage 2            Groupama – FDJ     male
130               BEL     Stage 2 Deceuninck - Quick - Step     male
131               USA     Stage 2        EF Education First     male
132               DEU     Stage 2          Bora - Hansgrohe     male
133               CHE     Stage 2    Team Katusha - Alpecin     male
134               ZAF     Stage 2       Team Dimension Data     male
135               ARE     Stage 2         UAE Team Emirates     male
136               AUS     Stage 2          Mitchelton-Scott     male
137               AUS     Stage 2          Mitchelton-Scott     male
138               ZAF     Stage 2       Team Dimension Data     male
139               FRA     Stage 2           Fortuneo-Samsic     male
140               POL     Stage 2                  CCC Team     male
141               BEL     Stage 2       Wanty Groupe Gobert     male
142               ESP     Stage 2             Movistar Team     male
143               FRA     Stage 2                   Cofidis     male
144               ESP     Stage 2             Movistar Team     male
145               BHR     Stage 2          Bahrain - Merida     male
146               BEL     Stage 2       Wanty Groupe Gobert     male
147               CHE     Stage 2    Team Katusha - Alpecin     male
148               FRA     Stage 2                   Cofidis     male
149               KAZ     Stage 2           Astana Pro Team     male
150               AUS     Stage 2          Mitchelton-Scott     male
151               AUS     Stage 2          Mitchelton-Scott     male
152               NLD     Stage 2               Team Sunweb     male
153               GBR     Stage 2                Team Ineos     male
154               GBR     Stage 2                Team Ineos     male
155               BHR     Stage 2          Bahrain - Merida     male
156               FRA     Stage 2            Direct Energie     male
157               ARE     Stage 2         UAE Team Emirates     male
158               BEL     Stage 2              Lotto Soudal     male
159               BEL     Stage 2 Deceuninck - Quick - Step     male
160               KAZ     Stage 2           Astana Pro Team     male
161               POL     Stage 2                  CCC Team     male
162               GBR     Stage 2                Team Ineos     male
163               BEL     Stage 2 Deceuninck - Quick - Step     male
164               ESP     Stage 2             Movistar Team     male
165               FRA     Stage 2            Groupama – FDJ     male
166               BHR     Stage 2          Bahrain - Merida     male
167               GBR     Stage 2                Team Ineos     male
168               DEU     Stage 2          Bora - Hansgrohe     male
169               NLD     Stage 2               Team Sunweb     male
170               BHR     Stage 2          Bahrain - Merida     male
171               BEL     Stage 2              Lotto Soudal     male
172               USA     Stage 2            Trek–Segafredo     male
173               NLD     Stage 2        Team Jumbo - Visma     male
174               FRA     Stage 2           Fortuneo-Samsic     male
175               CHE     Stage 2    Team Katusha - Alpecin     male
176               NLD     Stage 2               Team Sunweb     male
           nationality.y country_code.y result.team_time
1                  Spain            ESP        +00:01.05
2              Australia            AUS        +00:00.41
3              Australia            AUS        +00:00.41
4                    USA            USA        +00:00.28
5            Switzerland            CHE        +00:00.26
6                Belgium            BEL        +00:00.59
7                Bahrain            BHR        +00:00.36
8                Belgium            BEL        +00:00.21
9            Switzerland            CHE        +00:00.26
10                   USA            USA        +00:01.18
11                   USA            USA        +00:00.28
12           Netherlands            NLD        +00:00.26
13         Great Britain            GBR        +00:00.20
14                France            FRA        +00:01.42
15                France            FRA        +00:00.53
16                France            FRA        +00:00.53
17               Belgium            BEL        +00:00.59
18               Belgium            BEL        +00:00.59
19               Bahrain            BHR        +00:00.36
20                   USA            USA        +00:00.28
21             Australia            AUS        +00:00.41
22          South Africa            ZAF        +00:00.54
23                France            FRA        +00:00.32
24                 Spain            ESP        +00:01.05
25                France            FRA        +00:00.32
26               Belgium            BEL        +00:00.59
27            Kazakhstan            KAZ        +00:00.41
28          South Africa            ZAF        +00:00.54
29                France            FRA        +00:01.19
30  United Arab Emirates            ARE        +00:01.03
31                France            FRA        +00:01.51
32                France            FRA        +00:01.19
33               Belgium            BEL        +00:00.21
34            Kazakhstan            KAZ        +00:00.41
35           Netherlands            NLD        +00:00.26
36            Kazakhstan            KAZ        +00:00.41
37            Kazakhstan            KAZ        +00:00.41
38                France            FRA        +00:00.53
39                France            FRA        +00:00.32
40           Netherlands            NLD        +00:00.26
41                France            FRA        +00:00.53
42  United Arab Emirates            ARE        +00:01.03
43               Germany            DEU        +00:00.46
44                   USA            USA        +00:01.18
45                France            FRA        +00:01.19
46               Belgium            BEL        +00:00.21
47           Switzerland            CHE        +00:00.26
48                France            FRA        +00:01.42
49                   USA            USA        +00:01.18
50               Belgium            BEL        +00:01.58
51         Great Britain            GBR        +00:00.20
52                France            FRA        +00:01.42
53               Belgium            BEL        +00:01.58
54               Bahrain            BHR        +00:00.36
55           Netherlands            NLD         00:28.57
56               Belgium            BEL        +00:00.21
57           Netherlands            NLD        +00:00.26
58                France            FRA        +00:00.32
59                France            FRA        +00:00.53
60                France            FRA        +00:01.51
61                France            FRA        +00:01.42
62           Netherlands            NLD         00:28.57
63                France            FRA        +00:01.19
64  United Arab Emirates            ARE        +00:01.03
65                Poland            POL        +00:00.31
66           Netherlands            NLD         00:28.57
67           Netherlands            NLD         00:28.57
68                France            FRA        +00:01.42
69                France            FRA        +00:01.51
70                Poland            POL        +00:00.31
71               Germany            DEU        +00:00.46
72           Netherlands            NLD         00:28.57
73                France            FRA        +00:01.19
74                 Spain            ESP        +00:01.05
75               Belgium            BEL        +00:01.58
76                Poland            POL        +00:00.31
77         Great Britain            GBR        +00:00.20
78               Belgium            BEL        +00:01.58
79               Germany            DEU        +00:00.46
80               Germany            DEU        +00:00.46
81                   USA            USA        +00:01.18
82               Belgium            BEL        +00:01.58
83               Germany            DEU        +00:00.46
84           Switzerland            CHE        +00:00.26
85               Belgium            BEL        +00:00.21
86           Switzerland            CHE        +00:00.26
87           Netherlands            NLD         00:28.57
88  United Arab Emirates            ARE        +00:01.03
89            Kazakhstan            KAZ        +00:00.41
90                France            FRA        +00:00.32
91         Great Britain            GBR        +00:00.20
92            Kazakhstan            KAZ        +00:00.41
93             Australia            AUS        +00:00.41
94                   USA            USA        +00:00.28
95          South Africa            ZAF        +00:00.54
96           Netherlands            NLD         00:28.57
97                   USA            USA        +00:01.18
98                France            FRA        +00:01.19
99               Belgium            BEL        +00:01.58
100                  USA            USA        +00:00.28
101               France            FRA        +00:01.42
102               France            FRA        +00:00.53
103                  USA            USA        +00:01.18
104               France            FRA        +00:01.51
105 United Arab Emirates            ARE        +00:01.03
106              Belgium            BEL        +00:00.59
107 United Arab Emirates            ARE        +00:01.03
108               France            FRA        +00:01.19
109               France            FRA        +00:01.19
110               France            FRA        +00:01.42
111                Spain            ESP        +00:01.05
112              Germany            DEU        +00:00.46
113         South Africa            ZAF        +00:00.54
114              Bahrain            BHR        +00:00.36
115                  USA            USA        +00:01.18
116              Belgium            BEL        +00:00.59
117          Netherlands            NLD        +00:00.26
118                Spain            ESP        +00:01.05
119               France            FRA        +00:01.51
120               France            FRA        +00:01.51
121         South Africa            ZAF        +00:00.54
122               Poland            POL        +00:00.31
123                  USA            USA        +00:00.28
124               France            FRA        +00:00.32
125                  USA            USA        +00:00.28
126               Poland            POL        +00:00.31
127         South Africa            ZAF        +00:00.54
128               Poland            POL        +00:00.31
129               France            FRA        +00:00.32
130              Belgium            BEL        +00:00.21
131                  USA            USA        +00:00.28
132              Germany            DEU        +00:00.46
133          Switzerland            CHE        +00:00.26
134         South Africa            ZAF        +00:00.54
135 United Arab Emirates            ARE        +00:01.03
136            Australia            AUS        +00:00.41
137            Australia            AUS        +00:00.41
138         South Africa            ZAF        +00:00.54
139               France            FRA        +00:01.51
140               Poland            POL        +00:00.31
141              Belgium            BEL        +00:01.58
142                Spain            ESP        +00:01.05
143               France            FRA        +00:00.53
144                Spain            ESP        +00:01.05
145              Bahrain            BHR        +00:00.36
146              Belgium            BEL        +00:01.58
147          Switzerland            CHE        +00:00.26
148               France            FRA        +00:00.53
149           Kazakhstan            KAZ        +00:00.41
150            Australia            AUS        +00:00.41
151            Australia            AUS        +00:00.41
152          Netherlands            NLD        +00:00.26
153        Great Britain            GBR        +00:00.20
154        Great Britain            GBR        +00:00.20
155              Bahrain            BHR        +00:00.36
156               France            FRA        +00:01.42
157 United Arab Emirates            ARE        +00:01.03
158              Belgium            BEL        +00:00.59
159              Belgium            BEL        +00:00.21
160           Kazakhstan            KAZ        +00:00.41
161               Poland            POL        +00:00.31
162        Great Britain            GBR        +00:00.20
163              Belgium            BEL        +00:00.21
164                Spain            ESP        +00:01.05
165               France            FRA        +00:00.32
166              Bahrain            BHR        +00:00.36
167        Great Britain            GBR        +00:00.20
168              Germany            DEU        +00:00.46
169          Netherlands            NLD        +00:00.26
170              Bahrain            BHR        +00:00.36
171              Belgium            BEL        +00:00.59
172                  USA            USA        +00:01.18
173          Netherlands            NLD         00:28.57
174               France            FRA        +00:01.51
175          Switzerland            CHE        +00:00.26
176          Netherlands            NLD        +00:00.26
    result.team_time_ranking                 scheduled
1                         17 2019-07-07T12:30:00+00:00
2                         11 2019-07-07T12:30:00+00:00
3                         11 2019-07-07T12:30:00+00:00
4                          6 2019-07-07T12:30:00+00:00
5                          5 2019-07-07T12:30:00+00:00
6                         15 2019-07-07T12:30:00+00:00
7                          9 2019-07-07T12:30:00+00:00
8                          3 2019-07-07T12:30:00+00:00
9                          5 2019-07-07T12:30:00+00:00
10                        18 2019-07-07T12:30:00+00:00
11                         6 2019-07-07T12:30:00+00:00
12                         4 2019-07-07T12:30:00+00:00
13                         2 2019-07-07T12:30:00+00:00
14                        20 2019-07-07T12:30:00+00:00
15                        13 2019-07-07T12:30:00+00:00
16                        13 2019-07-07T12:30:00+00:00
17                        15 2019-07-07T12:30:00+00:00
18                        15 2019-07-07T12:30:00+00:00
19                         9 2019-07-07T12:30:00+00:00
20                         6 2019-07-07T12:30:00+00:00
21                        11 2019-07-07T12:30:00+00:00
22                        14 2019-07-07T12:30:00+00:00
23                         8 2019-07-07T12:30:00+00:00
24                        17 2019-07-07T12:30:00+00:00
25                         8 2019-07-07T12:30:00+00:00
26                        15 2019-07-07T12:30:00+00:00
27                        10 2019-07-07T12:30:00+00:00
28                        14 2019-07-07T12:30:00+00:00
29                        19 2019-07-07T12:30:00+00:00
30                        16 2019-07-07T12:30:00+00:00
31                        21 2019-07-07T12:30:00+00:00
32                        19 2019-07-07T12:30:00+00:00
33                         3 2019-07-07T12:30:00+00:00
34                        10 2019-07-07T12:30:00+00:00
35                         4 2019-07-07T12:30:00+00:00
36                        10 2019-07-07T12:30:00+00:00
37                        10 2019-07-07T12:30:00+00:00
38                        13 2019-07-07T12:30:00+00:00
39                         8 2019-07-07T12:30:00+00:00
40                         4 2019-07-07T12:30:00+00:00
41                        13 2019-07-07T12:30:00+00:00
42                        16 2019-07-07T12:30:00+00:00
43                        12 2019-07-07T12:30:00+00:00
44                        18 2019-07-07T12:30:00+00:00
45                        19 2019-07-07T12:30:00+00:00
46                         3 2019-07-07T12:30:00+00:00
47                         5 2019-07-07T12:30:00+00:00
48                        20 2019-07-07T12:30:00+00:00
49                        18 2019-07-07T12:30:00+00:00
50                        22 2019-07-07T12:30:00+00:00
51                         2 2019-07-07T12:30:00+00:00
52                        20 2019-07-07T12:30:00+00:00
53                        22 2019-07-07T12:30:00+00:00
54                         9 2019-07-07T12:30:00+00:00
55                         1 2019-07-07T12:30:00+00:00
56                         3 2019-07-07T12:30:00+00:00
57                         4 2019-07-07T12:30:00+00:00
58                         8 2019-07-07T12:30:00+00:00
59                        13 2019-07-07T12:30:00+00:00
60                        21 2019-07-07T12:30:00+00:00
61                        20 2019-07-07T12:30:00+00:00
62                         1 2019-07-07T12:30:00+00:00
63                        19 2019-07-07T12:30:00+00:00
64                        16 2019-07-07T12:30:00+00:00
65                         7 2019-07-07T12:30:00+00:00
66                         1 2019-07-07T12:30:00+00:00
67                         1 2019-07-07T12:30:00+00:00
68                        20 2019-07-07T12:30:00+00:00
69                        21 2019-07-07T12:30:00+00:00
70                         7 2019-07-07T12:30:00+00:00
71                        12 2019-07-07T12:30:00+00:00
72                         1 2019-07-07T12:30:00+00:00
73                        19 2019-07-07T12:30:00+00:00
74                        17 2019-07-07T12:30:00+00:00
75                        22 2019-07-07T12:30:00+00:00
76                         7 2019-07-07T12:30:00+00:00
77                         2 2019-07-07T12:30:00+00:00
78                        22 2019-07-07T12:30:00+00:00
79                        12 2019-07-07T12:30:00+00:00
80                        12 2019-07-07T12:30:00+00:00
81                        18 2019-07-07T12:30:00+00:00
82                        22 2019-07-07T12:30:00+00:00
83                        12 2019-07-07T12:30:00+00:00
84                         5 2019-07-07T12:30:00+00:00
85                         3 2019-07-07T12:30:00+00:00
86                         5 2019-07-07T12:30:00+00:00
87                         1 2019-07-07T12:30:00+00:00
88                        16 2019-07-07T12:30:00+00:00
89                        10 2019-07-07T12:30:00+00:00
90                         8 2019-07-07T12:30:00+00:00
91                         2 2019-07-07T12:30:00+00:00
92                        10 2019-07-07T12:30:00+00:00
93                        11 2019-07-07T12:30:00+00:00
94                         6 2019-07-07T12:30:00+00:00
95                        14 2019-07-07T12:30:00+00:00
96                         1 2019-07-07T12:30:00+00:00
97                        18 2019-07-07T12:30:00+00:00
98                        19 2019-07-07T12:30:00+00:00
99                        22 2019-07-07T12:30:00+00:00
100                        6 2019-07-07T12:30:00+00:00
101                       20 2019-07-07T12:30:00+00:00
102                       13 2019-07-07T12:30:00+00:00
103                       18 2019-07-07T12:30:00+00:00
104                       21 2019-07-07T12:30:00+00:00
105                       16 2019-07-07T12:30:00+00:00
106                       15 2019-07-07T12:30:00+00:00
107                       16 2019-07-07T12:30:00+00:00
108                       19 2019-07-07T12:30:00+00:00
109                       19 2019-07-07T12:30:00+00:00
110                       20 2019-07-07T12:30:00+00:00
111                       17 2019-07-07T12:30:00+00:00
112                       12 2019-07-07T12:30:00+00:00
113                       14 2019-07-07T12:30:00+00:00
114                        9 2019-07-07T12:30:00+00:00
115                       18 2019-07-07T12:30:00+00:00
116                       15 2019-07-07T12:30:00+00:00
117                        4 2019-07-07T12:30:00+00:00
118                       17 2019-07-07T12:30:00+00:00
119                       21 2019-07-07T12:30:00+00:00
120                       21 2019-07-07T12:30:00+00:00
121                       14 2019-07-07T12:30:00+00:00
122                        7 2019-07-07T12:30:00+00:00
123                        6 2019-07-07T12:30:00+00:00
124                        8 2019-07-07T12:30:00+00:00
125                        6 2019-07-07T12:30:00+00:00
126                        7 2019-07-07T12:30:00+00:00
127                       14 2019-07-07T12:30:00+00:00
128                        7 2019-07-07T12:30:00+00:00
129                        8 2019-07-07T12:30:00+00:00
130                        3 2019-07-07T12:30:00+00:00
131                        6 2019-07-07T12:30:00+00:00
132                       12 2019-07-07T12:30:00+00:00
133                        5 2019-07-07T12:30:00+00:00
134                       14 2019-07-07T12:30:00+00:00
135                       16 2019-07-07T12:30:00+00:00
136                       11 2019-07-07T12:30:00+00:00
137                       11 2019-07-07T12:30:00+00:00
138                       14 2019-07-07T12:30:00+00:00
139                       21 2019-07-07T12:30:00+00:00
140                        7 2019-07-07T12:30:00+00:00
141                       22 2019-07-07T12:30:00+00:00
142                       17 2019-07-07T12:30:00+00:00
143                       13 2019-07-07T12:30:00+00:00
144                       17 2019-07-07T12:30:00+00:00
145                        9 2019-07-07T12:30:00+00:00
146                       22 2019-07-07T12:30:00+00:00
147                        5 2019-07-07T12:30:00+00:00
148                       13 2019-07-07T12:30:00+00:00
149                       10 2019-07-07T12:30:00+00:00
150                       11 2019-07-07T12:30:00+00:00
151                       11 2019-07-07T12:30:00+00:00
152                        4 2019-07-07T12:30:00+00:00
153                        2 2019-07-07T12:30:00+00:00
154                        2 2019-07-07T12:30:00+00:00
155                        9 2019-07-07T12:30:00+00:00
156                       20 2019-07-07T12:30:00+00:00
157                       16 2019-07-07T12:30:00+00:00
158                       15 2019-07-07T12:30:00+00:00
159                        3 2019-07-07T12:30:00+00:00
160                       10 2019-07-07T12:30:00+00:00
161                        7 2019-07-07T12:30:00+00:00
162                        2 2019-07-07T12:30:00+00:00
163                        3 2019-07-07T12:30:00+00:00
164                       17 2019-07-07T12:30:00+00:00
165                        8 2019-07-07T12:30:00+00:00
166                        9 2019-07-07T12:30:00+00:00
167                        2 2019-07-07T12:30:00+00:00
168                       12 2019-07-07T12:30:00+00:00
169                        4 2019-07-07T12:30:00+00:00
170                        9 2019-07-07T12:30:00+00:00
171                       15 2019-07-07T12:30:00+00:00
172                       18 2019-07-07T12:30:00+00:00
173                        1 2019-07-07T12:30:00+00:00
174                       21 2019-07-07T12:30:00+00:00
175                        5 2019-07-07T12:30:00+00:00
176                        4 2019-07-07T12:30:00+00:00
                scheduled_end  type departure_city arrival_city status
1   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
2   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
3   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
4   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
5   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
6   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
7   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
8   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
9   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
10  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
11  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
12  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
13  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
14  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
15  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
16  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
17  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
18  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
19  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
20  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
21  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
22  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
23  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
24  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
25  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
26  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
27  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
28  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
29  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
30  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
31  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
32  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
33  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
34  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
35  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
36  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
37  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
38  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
39  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
40  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
41  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
42  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
43  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
44  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
45  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
46  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
47  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
48  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
49  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
50  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
51  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
52  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
53  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
54  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
55  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
56  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
57  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
58  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
59  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
60  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
61  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
62  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
63  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
64  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
65  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
66  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
67  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
68  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
69  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
70  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
71  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
72  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
73  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
74  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
75  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
76  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
77  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
78  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
79  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
80  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
81  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
82  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
83  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
84  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
85  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
86  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
87  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
88  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
89  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
90  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
91  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
92  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
93  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
94  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
95  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
96  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
97  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
98  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
99  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
100 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
101 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
102 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
103 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
104 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
105 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
106 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
107 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
108 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
109 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
110 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
111 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
112 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
113 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
114 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
115 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
116 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
117 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
118 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
119 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
120 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
121 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
122 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
123 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
124 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
125 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
126 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
127 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
128 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
129 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
130 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
131 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
132 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
133 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
134 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
135 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
136 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
137 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
138 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
139 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
140 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
141 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
142 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
143 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
144 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
145 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
146 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
147 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
148 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
149 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
150 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
151 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
152 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
153 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
154 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
155 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
156 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
157 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
158 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
159 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
160 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
161 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
162 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
163 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
164 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
165 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
166 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
167 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
168 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
169 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
170 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
171 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
172 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
173 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
174 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
175 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
176 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
     classification distance distance_unit single_event
1   Team Time Trial     27,6            km        FALSE
2   Team Time Trial     27,6            km        FALSE
3   Team Time Trial     27,6            km        FALSE
4   Team Time Trial     27,6            km        FALSE
5   Team Time Trial     27,6            km        FALSE
6   Team Time Trial     27,6            km        FALSE
7   Team Time Trial     27,6            km        FALSE
8   Team Time Trial     27,6            km        FALSE
9   Team Time Trial     27,6            km        FALSE
10  Team Time Trial     27,6            km        FALSE
11  Team Time Trial     27,6            km        FALSE
12  Team Time Trial     27,6            km        FALSE
13  Team Time Trial     27,6            km        FALSE
14  Team Time Trial     27,6            km        FALSE
15  Team Time Trial     27,6            km        FALSE
16  Team Time Trial     27,6            km        FALSE
17  Team Time Trial     27,6            km        FALSE
18  Team Time Trial     27,6            km        FALSE
19  Team Time Trial     27,6            km        FALSE
20  Team Time Trial     27,6            km        FALSE
21  Team Time Trial     27,6            km        FALSE
22  Team Time Trial     27,6            km        FALSE
23  Team Time Trial     27,6            km        FALSE
24  Team Time Trial     27,6            km        FALSE
25  Team Time Trial     27,6            km        FALSE
26  Team Time Trial     27,6            km        FALSE
27  Team Time Trial     27,6            km        FALSE
28  Team Time Trial     27,6            km        FALSE
29  Team Time Trial     27,6            km        FALSE
30  Team Time Trial     27,6            km        FALSE
31  Team Time Trial     27,6            km        FALSE
32  Team Time Trial     27,6            km        FALSE
33  Team Time Trial     27,6            km        FALSE
34  Team Time Trial     27,6            km        FALSE
35  Team Time Trial     27,6            km        FALSE
36  Team Time Trial     27,6            km        FALSE
37  Team Time Trial     27,6            km        FALSE
38  Team Time Trial     27,6            km        FALSE
39  Team Time Trial     27,6            km        FALSE
40  Team Time Trial     27,6            km        FALSE
41  Team Time Trial     27,6            km        FALSE
42  Team Time Trial     27,6            km        FALSE
43  Team Time Trial     27,6            km        FALSE
44  Team Time Trial     27,6            km        FALSE
45  Team Time Trial     27,6            km        FALSE
46  Team Time Trial     27,6            km        FALSE
47  Team Time Trial     27,6            km        FALSE
48  Team Time Trial     27,6            km        FALSE
49  Team Time Trial     27,6            km        FALSE
50  Team Time Trial     27,6            km        FALSE
51  Team Time Trial     27,6            km        FALSE
52  Team Time Trial     27,6            km        FALSE
53  Team Time Trial     27,6            km        FALSE
54  Team Time Trial     27,6            km        FALSE
55  Team Time Trial     27,6            km        FALSE
56  Team Time Trial     27,6            km        FALSE
57  Team Time Trial     27,6            km        FALSE
58  Team Time Trial     27,6            km        FALSE
59  Team Time Trial     27,6            km        FALSE
60  Team Time Trial     27,6            km        FALSE
61  Team Time Trial     27,6            km        FALSE
62  Team Time Trial     27,6            km        FALSE
63  Team Time Trial     27,6            km        FALSE
64  Team Time Trial     27,6            km        FALSE
65  Team Time Trial     27,6            km        FALSE
66  Team Time Trial     27,6            km        FALSE
67  Team Time Trial     27,6            km        FALSE
68  Team Time Trial     27,6            km        FALSE
69  Team Time Trial     27,6            km        FALSE
70  Team Time Trial     27,6            km        FALSE
71  Team Time Trial     27,6            km        FALSE
72  Team Time Trial     27,6            km        FALSE
73  Team Time Trial     27,6            km        FALSE
74  Team Time Trial     27,6            km        FALSE
75  Team Time Trial     27,6            km        FALSE
76  Team Time Trial     27,6            km        FALSE
77  Team Time Trial     27,6            km        FALSE
78  Team Time Trial     27,6            km        FALSE
79  Team Time Trial     27,6            km        FALSE
80  Team Time Trial     27,6            km        FALSE
81  Team Time Trial     27,6            km        FALSE
82  Team Time Trial     27,6            km        FALSE
83  Team Time Trial     27,6            km        FALSE
84  Team Time Trial     27,6            km        FALSE
85  Team Time Trial     27,6            km        FALSE
86  Team Time Trial     27,6            km        FALSE
87  Team Time Trial     27,6            km        FALSE
88  Team Time Trial     27,6            km        FALSE
89  Team Time Trial     27,6            km        FALSE
90  Team Time Trial     27,6            km        FALSE
91  Team Time Trial     27,6            km        FALSE
92  Team Time Trial     27,6            km        FALSE
93  Team Time Trial     27,6            km        FALSE
94  Team Time Trial     27,6            km        FALSE
95  Team Time Trial     27,6            km        FALSE
96  Team Time Trial     27,6            km        FALSE
97  Team Time Trial     27,6            km        FALSE
98  Team Time Trial     27,6            km        FALSE
99  Team Time Trial     27,6            km        FALSE
100 Team Time Trial     27,6            km        FALSE
101 Team Time Trial     27,6            km        FALSE
102 Team Time Trial     27,6            km        FALSE
103 Team Time Trial     27,6            km        FALSE
104 Team Time Trial     27,6            km        FALSE
105 Team Time Trial     27,6            km        FALSE
106 Team Time Trial     27,6            km        FALSE
107 Team Time Trial     27,6            km        FALSE
108 Team Time Trial     27,6            km        FALSE
109 Team Time Trial     27,6            km        FALSE
110 Team Time Trial     27,6            km        FALSE
111 Team Time Trial     27,6            km        FALSE
112 Team Time Trial     27,6            km        FALSE
113 Team Time Trial     27,6            km        FALSE
114 Team Time Trial     27,6            km        FALSE
115 Team Time Trial     27,6            km        FALSE
116 Team Time Trial     27,6            km        FALSE
117 Team Time Trial     27,6            km        FALSE
118 Team Time Trial     27,6            km        FALSE
119 Team Time Trial     27,6            km        FALSE
120 Team Time Trial     27,6            km        FALSE
121 Team Time Trial     27,6            km        FALSE
122 Team Time Trial     27,6            km        FALSE
123 Team Time Trial     27,6            km        FALSE
124 Team Time Trial     27,6            km        FALSE
125 Team Time Trial     27,6            km        FALSE
126 Team Time Trial     27,6            km        FALSE
127 Team Time Trial     27,6            km        FALSE
128 Team Time Trial     27,6            km        FALSE
129 Team Time Trial     27,6            km        FALSE
130 Team Time Trial     27,6            km        FALSE
131 Team Time Trial     27,6            km        FALSE
132 Team Time Trial     27,6            km        FALSE
133 Team Time Trial     27,6            km        FALSE
134 Team Time Trial     27,6            km        FALSE
135 Team Time Trial     27,6            km        FALSE
136 Team Time Trial     27,6            km        FALSE
137 Team Time Trial     27,6            km        FALSE
138 Team Time Trial     27,6            km        FALSE
139 Team Time Trial     27,6            km        FALSE
140 Team Time Trial     27,6            km        FALSE
141 Team Time Trial     27,6            km        FALSE
142 Team Time Trial     27,6            km        FALSE
143 Team Time Trial     27,6            km        FALSE
144 Team Time Trial     27,6            km        FALSE
145 Team Time Trial     27,6            km        FALSE
146 Team Time Trial     27,6            km        FALSE
147 Team Time Trial     27,6            km        FALSE
148 Team Time Trial     27,6            km        FALSE
149 Team Time Trial     27,6            km        FALSE
150 Team Time Trial     27,6            km        FALSE
151 Team Time Trial     27,6            km        FALSE
152 Team Time Trial     27,6            km        FALSE
153 Team Time Trial     27,6            km        FALSE
154 Team Time Trial     27,6            km        FALSE
155 Team Time Trial     27,6            km        FALSE
156 Team Time Trial     27,6            km        FALSE
157 Team Time Trial     27,6            km        FALSE
158 Team Time Trial     27,6            km        FALSE
159 Team Time Trial     27,6            km        FALSE
160 Team Time Trial     27,6            km        FALSE
161 Team Time Trial     27,6            km        FALSE
162 Team Time Trial     27,6            km        FALSE
163 Team Time Trial     27,6            km        FALSE
164 Team Time Trial     27,6            km        FALSE
165 Team Time Trial     27,6            km        FALSE
166 Team Time Trial     27,6            km        FALSE
167 Team Time Trial     27,6            km        FALSE
168 Team Time Trial     27,6            km        FALSE
169 Team Time Trial     27,6            km        FALSE
170 Team Time Trial     27,6            km        FALSE
171 Team Time Trial     27,6            km        FALSE
172 Team Time Trial     27,6            km        FALSE
173 Team Time Trial     27,6            km        FALSE
174 Team Time Trial     27,6            km        FALSE
175 Team Time Trial     27,6            km        FALSE
176 Team Time Trial     27,6            km        FALSE
```

```r
new_data <- data %>%
  select(stage = description, rider_name = name.x, rider_nat = nationality.x, team_name = team.name, team_nat = team.nationality, team_time = result.team_time, team_ranking = result.team_time_ranking, dep_city = departure_city, arr_city = arrival_city, classification, distance, start_date = scheduled)
new_data
```

```
      stage                             rider_name      rider_nat
1   Stage 2                    Valverde, Alejandro          Spain
2   Stage 2                             Haig, Jack      Australia
3   Stage 2                            Yates, Adam  Great Britain
4   Stage 2                         Scully, Thomas    New Zealand
5   Stage 2                         Zakarin, Ilnur         Russia
6   Stage 2                            Ewan, Caleb      Australia
7   Stage 2                         Mohoric, Matej       Slovenia
8   Stage 2                    Alaphilippe, Julian         France
9   Stage 2                            Zabel, Rick        Germany
10  Stage 2                        Stuyven, Jasper        Belgium
11  Stage 2                       Bettiol, Alberto          Italy
12  Stage 2                 Kragh Andersen, Soeren        Denmark
13  Stage 2                      van Baarle, Dylan    Netherlands
14  Stage 2                     Bonifazio, Niccolo          Italy
15  Stage 2                     Rossetto, Stephane         France
16  Stage 2                    Laporte, Christophe         France
17  Stage 2                          Benoot, Tiesj        Belgium
18  Stage 2                       de Buyst, Jasper        Belgium
19  Stage 2                           Teuns, Dylan        Belgium
20  Stage 2                         Woods, Michael         Canada
21  Stage 2                           Yates, Simon  Great Britain
22  Stage 2              Valgren Andersen, Michael        Denmark
23  Stage 2                           Kung, Stefan    Switzerland
24  Stage 2             Verona Quintanilla, Carlos          Spain
25  Stage 2                           Molard, Rudy         France
26  Stage 2                           Wellens, Tim        Belgium
27  Stage 2                            Houle, Hugo         Canada
28  Stage 2          Janse van Rensburg, Reinhardt   South Africa
29  Stage 2                       Gougeard, Alexis         France
30  Stage 2                             Aru, Fabio          Italy
31  Stage 2                        Barguil, Warren         France
32  Stage 2                     Vuillermoz, Alexis         France
33  Stage 2                         Lampaert, Yves        Belgium
34  Stage 2                   Nielsen, Magnus Cort        Denmark
35  Stage 2                          Arndt, Nikias        Germany
36  Stage 2                       Lutsenko, Alexey     Kazakhstan
37  Stage 2                 Fraile Matarranz, Omar          Spain
38  Stage 2                   Perichon, Pierre-Luc         France
39  Stage 2                 Reichenbach, Sebastien    Switzerland
40  Stage 2                             Haga, Chad            USA
41  Stage 2                       Berhane, Natnael        Eritrea
42  Stage 2                    Bystroem, Sven Erik         Norway
43  Stage 2                 Schachmann, Maximilian        Germany
44  Stage 2                          Skujins, Toms         Latvia
45  Stage 2                         Bardet, Romain         France
46  Stage 2                     Mas Nicolau, Enric          Spain
47  Stage 2                           Politt, Nils        Germany
48  Stage 2                      Calmejane, Lilian         France
49  Stage 2                        Bernard, Julien         France
50  Stage 2                      Martin, Guillaume         France
51  Stage 2                           Bernal, Egan       Colombia
52  Stage 2                       Grellier, Fabien         France
53  Stage 2                         de Gendt, Aime        Belgium
54  Stage 2                   Garcia Cortina, Ivan          Spain
55  Stage 2                Jansen Groendahl, Amund         Norway
56  Stage 2 Richeze Araquistain, Ariel Maximiliano      Argentina
57  Stage 2                         Kamna, Lennard        Germany
58  Stage 2                           Gaudu, David         France
59  Stage 2                         Perez, Anthony         France
60  Stage 2                          Gesbert, Elie         France
61  Stage 2                         Ourselin, Paul         France
62  Stage 2                         Van Aert, Wout        Belgium
63  Stage 2                      Cosnefroy, Benoit         France
64  Stage 2                      Philipsen, Jasper        Belgium
65  Stage 2                         Bevin, Patrick    New Zealand
66  Stage 2                       de Plus, Laurens        Belgium
67  Stage 2                        Teunissen, Mike    Netherlands
68  Stage 2                        Turgis, Anthony         France
69  Stage 2                        Ledanois, Kevin         France
70  Stage 2                     Wisniowski, Lukasz         Poland
71  Stage 2                        Konrad, Patrick        Austria
72  Stage 2                     Groenewegen, Dylan    Netherlands
73  Stage 2                        Naesen, Olivier        Belgium
74  Stage 2                    Soler Gimenez, Marc          Spain
75  Stage 2                      Backaert, Fredrik        Belgium
76  Stage 2                         Rosskopf, Joey            USA
77  Stage 2                         Moscon, Gianni          Italy
78  Stage 2                       Meurisse, Xandro        Belgium
79  Stage 2                      Buchmann, Emanuel        Germany
80  Stage 2                     Postlberger, Lukas        Austria
81  Stage 2                        Ciccone, Giulio          Italy
82  Stage 2                  Eiking, Odd Christian         Norway
83  Stage 2                     Muhlberger, Gregor        Austria
84  Stage 2                    Wurtz Schmidt, Mads        Denmark
85  Stage 2                        Asgreen, Kasper        Denmark
86  Stage 2                        Goncalves, Jose       Portugal
87  Stage 2                        Bennett, George    New Zealand
88  Stage 2                  Laengen, Vegard Stake         Norway
89  Stage 2                 Sanchez Gil, Luis Leon          Spain
90  Stage 2                          Roux, Anthony         France
91  Stage 2                        Thomas, Geraint  Great Britain
92  Stage 2                        Fuglsang, Jakob        Denmark
93  Stage 2                           Impey, Daryl   South Africa
94  Stage 2                         Kangert, Tanel        Estonia
95  Stage 2                  Hagen, Edvald Boasson         Norway
96  Stage 2                           Martin, Tony        Germany
97  Stage 2                         Mollema, Bauke    Netherlands
98  Stage 2                         Frank, Mathias    Switzerland
99  Stage 2                         Offredo, Yoann         France
100 Stage 2                          Clarke, Simon      Australia
101 Stage 2                         Taaramae, Rein        Estonia
102 Stage 2                          Simon, Julien         France
103 Stage 2                          Porte, Richie      Australia
104 Stage 2                          Bouet, Maxime         France
105 Stage 2                         Martin, Daniel        Ireland
106 Stage 2                           Kluge, Roger        Germany
107 Stage 2            Faria Da Costa, Rui Alberto       Portugal
108 Stage 2                         Gallopin, Tony         France
109 Stage 2                         Cherel, Mikael         France
110 Stage 2                         Terpstra, Niki    Netherlands
111 Stage 2                         Amador, Andrey     Costa Rica
112 Stage 2                      Burghardt, Marcus        Germany
113 Stage 2                       Bak, Lars Ytting        Denmark
114 Stage 2                       Nibali, Vincenzo          Italy
115 Stage 2                          De Kort, Koen    Netherlands
116 Stage 2                        Monfort, Maxime         France
117 Stage 2                         Roche, Nicolas        Ireland
118 Stage 2                         Erviti, Imanol          Spain
119 Stage 2                         Greipel, Andre        Germany
120 Stage 2                         Moinard, Amael         France
121 Stage 2                       Cummings, Steven  Great Britain
122 Stage 2                     Van Avermaet, Greg        Belgium
123 Stage 2                        Uran, Rigoberto       Colombia
124 Stage 2                        Bonnet, William         France
125 Stage 2                   Langeveld, Sebastian    Netherlands
126 Stage 2                         Pauwels, Serge        Belgium
127 Stage 2                       Kreuziger, Roman Czech Republic
128 Stage 2                        Schaer, Michael    Switzerland
129 Stage 2                    Ladagnous, Matthieu         France
130 Stage 2                        Devenyns, Dries        Belgium
131 Stage 2                    Van Garderen, Tejay            USA
132 Stage 2                            Oss, Daniel          Italy
133 Stage 2                          Haller, Marco        Austria
134 Stage 2                       Nizzolo, Giacomo          Italy
135 Stage 2             Henao Montoya, Sergio Luis       Colombia
136 Stage 2                        Durbridge, Luke      Australia
137 Stage 2                       Hepburn, Michael      Australia
138 Stage 2                         King, Benjamin            USA
139 Stage 2                        Vachon, Florian         France
140 Stage 2                  de Marchi, Alessandro          Italy
141 Stage 2                      Pasqualon, Andrea          Italy
142 Stage 2                        Quintana, Nairo       Colombia
143 Stage 2                          Edet, Nicolas         France
144 Stage 2                     Landa Meana, Mikel          Spain
145 Stage 2                           Tratnik, Jan       Slovenia
146 Stage 2                      van Melsen, Kevin        Belgium
147 Stage 2                      Debusschere, Jens        Belgium
148 Stage 2                   Herrada Lopez, Jesus          Spain
149 Stage 2                          Bilbao, Pello          Spain
150 Stage 2               Juul-Jensen, Christopher        Denmark
151 Stage 2                        Trentin, Matteo          Italy
152 Stage 2                       Kelderman, Wilco    Netherlands
153 Stage 2                    Kwiatkowski, Michal         Poland
154 Stage 2                             Rowe, Luke  Great Britain
155 Stage 2                        Caruso, Damiano          Italy
156 Stage 2                         Sicard, Romain         France
157 Stage 2                    Kristoff, Alexander         Norway
158 Stage 2                       De Gendt, Thomas        Belgium
159 Stage 2                          Viviani, Elia          Italy
160 Stage 2               Izagirre Insausti, Gorka          Spain
161 Stage 2                         Geschke, Simon        Germany
162 Stage 2                          Poels, Wouter    Netherlands
163 Stage 2                      Moerkoev, Michael        Denmark
164 Stage 2  Santos Simoes Oliveira, Nelson Filipe       Portugal
165 Stage 2                         Pinot, Thibaut         France
166 Stage 2                       Colbrelli, Sonny          Italy
167 Stage 2          Castroviejo, Nicolas Jonathan          Spain
168 Stage 2                           Sagan, Peter       Slovakia
169 Stage 2                      Matthews, Michael      Australia
170 Stage 2                          Dennis, Rohan      Australia
171 Stage 2                       Keukeleire, Jens        Belgium
172 Stage 2                         Felline, Fabio          Italy
173 Stage 2                     Kruijswijk, Steven    Netherlands
174 Stage 2                     Delaplace, Anthony         France
175 Stage 2                          Dowsett, Alex  Great Britain
176 Stage 2                              Bol, Cees    Netherlands
                    team_name             team_nat team_time team_ranking
1               Movistar Team                Spain +00:01.05           17
2            Mitchelton-Scott            Australia +00:00.41           11
3            Mitchelton-Scott            Australia +00:00.41           11
4          EF Education First                  USA +00:00.28            6
5      Team Katusha - Alpecin          Switzerland +00:00.26            5
6                Lotto Soudal              Belgium +00:00.59           15
7            Bahrain - Merida              Bahrain +00:00.36            9
8   Deceuninck - Quick - Step              Belgium +00:00.21            3
9      Team Katusha - Alpecin          Switzerland +00:00.26            5
10             Trek–Segafredo                  USA +00:01.18           18
11         EF Education First                  USA +00:00.28            6
12                Team Sunweb          Netherlands +00:00.26            4
13                 Team Ineos        Great Britain +00:00.20            2
14             Direct Energie               France +00:01.42           20
15                    Cofidis               France +00:00.53           13
16                    Cofidis               France +00:00.53           13
17               Lotto Soudal              Belgium +00:00.59           15
18               Lotto Soudal              Belgium +00:00.59           15
19           Bahrain - Merida              Bahrain +00:00.36            9
20         EF Education First                  USA +00:00.28            6
21           Mitchelton-Scott            Australia +00:00.41           11
22        Team Dimension Data         South Africa +00:00.54           14
23             Groupama – FDJ               France +00:00.32            8
24              Movistar Team                Spain +00:01.05           17
25             Groupama – FDJ               France +00:00.32            8
26               Lotto Soudal              Belgium +00:00.59           15
27            Astana Pro Team           Kazakhstan +00:00.41           10
28        Team Dimension Data         South Africa +00:00.54           14
29           Ag2r La Mondiale               France +00:01.19           19
30          UAE Team Emirates United Arab Emirates +00:01.03           16
31            Fortuneo-Samsic               France +00:01.51           21
32           Ag2r La Mondiale               France +00:01.19           19
33  Deceuninck - Quick - Step              Belgium +00:00.21            3
34            Astana Pro Team           Kazakhstan +00:00.41           10
35                Team Sunweb          Netherlands +00:00.26            4
36            Astana Pro Team           Kazakhstan +00:00.41           10
37            Astana Pro Team           Kazakhstan +00:00.41           10
38                    Cofidis               France +00:00.53           13
39             Groupama – FDJ               France +00:00.32            8
40                Team Sunweb          Netherlands +00:00.26            4
41                    Cofidis               France +00:00.53           13
42          UAE Team Emirates United Arab Emirates +00:01.03           16
43           Bora - Hansgrohe              Germany +00:00.46           12
44             Trek–Segafredo                  USA +00:01.18           18
45           Ag2r La Mondiale               France +00:01.19           19
46  Deceuninck - Quick - Step              Belgium +00:00.21            3
47     Team Katusha - Alpecin          Switzerland +00:00.26            5
48             Direct Energie               France +00:01.42           20
49             Trek–Segafredo                  USA +00:01.18           18
50        Wanty Groupe Gobert              Belgium +00:01.58           22
51                 Team Ineos        Great Britain +00:00.20            2
52             Direct Energie               France +00:01.42           20
53        Wanty Groupe Gobert              Belgium +00:01.58           22
54           Bahrain - Merida              Bahrain +00:00.36            9
55         Team Jumbo - Visma          Netherlands  00:28.57            1
56  Deceuninck - Quick - Step              Belgium +00:00.21            3
57                Team Sunweb          Netherlands +00:00.26            4
58             Groupama – FDJ               France +00:00.32            8
59                    Cofidis               France +00:00.53           13
60            Fortuneo-Samsic               France +00:01.51           21
61             Direct Energie               France +00:01.42           20
62         Team Jumbo - Visma          Netherlands  00:28.57            1
63           Ag2r La Mondiale               France +00:01.19           19
64          UAE Team Emirates United Arab Emirates +00:01.03           16
65                   CCC Team               Poland +00:00.31            7
66         Team Jumbo - Visma          Netherlands  00:28.57            1
67         Team Jumbo - Visma          Netherlands  00:28.57            1
68             Direct Energie               France +00:01.42           20
69            Fortuneo-Samsic               France +00:01.51           21
70                   CCC Team               Poland +00:00.31            7
71           Bora - Hansgrohe              Germany +00:00.46           12
72         Team Jumbo - Visma          Netherlands  00:28.57            1
73           Ag2r La Mondiale               France +00:01.19           19
74              Movistar Team                Spain +00:01.05           17
75        Wanty Groupe Gobert              Belgium +00:01.58           22
76                   CCC Team               Poland +00:00.31            7
77                 Team Ineos        Great Britain +00:00.20            2
78        Wanty Groupe Gobert              Belgium +00:01.58           22
79           Bora - Hansgrohe              Germany +00:00.46           12
80           Bora - Hansgrohe              Germany +00:00.46           12
81             Trek–Segafredo                  USA +00:01.18           18
82        Wanty Groupe Gobert              Belgium +00:01.58           22
83           Bora - Hansgrohe              Germany +00:00.46           12
84     Team Katusha - Alpecin          Switzerland +00:00.26            5
85  Deceuninck - Quick - Step              Belgium +00:00.21            3
86     Team Katusha - Alpecin          Switzerland +00:00.26            5
87         Team Jumbo - Visma          Netherlands  00:28.57            1
88          UAE Team Emirates United Arab Emirates +00:01.03           16
89            Astana Pro Team           Kazakhstan +00:00.41           10
90             Groupama – FDJ               France +00:00.32            8
91                 Team Ineos        Great Britain +00:00.20            2
92            Astana Pro Team           Kazakhstan +00:00.41           10
93           Mitchelton-Scott            Australia +00:00.41           11
94         EF Education First                  USA +00:00.28            6
95        Team Dimension Data         South Africa +00:00.54           14
96         Team Jumbo - Visma          Netherlands  00:28.57            1
97             Trek–Segafredo                  USA +00:01.18           18
98           Ag2r La Mondiale               France +00:01.19           19
99        Wanty Groupe Gobert              Belgium +00:01.58           22
100        EF Education First                  USA +00:00.28            6
101            Direct Energie               France +00:01.42           20
102                   Cofidis               France +00:00.53           13
103            Trek–Segafredo                  USA +00:01.18           18
104           Fortuneo-Samsic               France +00:01.51           21
105         UAE Team Emirates United Arab Emirates +00:01.03           16
106              Lotto Soudal              Belgium +00:00.59           15
107         UAE Team Emirates United Arab Emirates +00:01.03           16
108          Ag2r La Mondiale               France +00:01.19           19
109          Ag2r La Mondiale               France +00:01.19           19
110            Direct Energie               France +00:01.42           20
111             Movistar Team                Spain +00:01.05           17
112          Bora - Hansgrohe              Germany +00:00.46           12
113       Team Dimension Data         South Africa +00:00.54           14
114          Bahrain - Merida              Bahrain +00:00.36            9
115            Trek–Segafredo                  USA +00:01.18           18
116              Lotto Soudal              Belgium +00:00.59           15
117               Team Sunweb          Netherlands +00:00.26            4
118             Movistar Team                Spain +00:01.05           17
119           Fortuneo-Samsic               France +00:01.51           21
120           Fortuneo-Samsic               France +00:01.51           21
121       Team Dimension Data         South Africa +00:00.54           14
122                  CCC Team               Poland +00:00.31            7
123        EF Education First                  USA +00:00.28            6
124            Groupama – FDJ               France +00:00.32            8
125        EF Education First                  USA +00:00.28            6
126                  CCC Team               Poland +00:00.31            7
127       Team Dimension Data         South Africa +00:00.54           14
128                  CCC Team               Poland +00:00.31            7
129            Groupama – FDJ               France +00:00.32            8
130 Deceuninck - Quick - Step              Belgium +00:00.21            3
131        EF Education First                  USA +00:00.28            6
132          Bora - Hansgrohe              Germany +00:00.46           12
133    Team Katusha - Alpecin          Switzerland +00:00.26            5
134       Team Dimension Data         South Africa +00:00.54           14
135         UAE Team Emirates United Arab Emirates +00:01.03           16
136          Mitchelton-Scott            Australia +00:00.41           11
137          Mitchelton-Scott            Australia +00:00.41           11
138       Team Dimension Data         South Africa +00:00.54           14
139           Fortuneo-Samsic               France +00:01.51           21
140                  CCC Team               Poland +00:00.31            7
141       Wanty Groupe Gobert              Belgium +00:01.58           22
142             Movistar Team                Spain +00:01.05           17
143                   Cofidis               France +00:00.53           13
144             Movistar Team                Spain +00:01.05           17
145          Bahrain - Merida              Bahrain +00:00.36            9
146       Wanty Groupe Gobert              Belgium +00:01.58           22
147    Team Katusha - Alpecin          Switzerland +00:00.26            5
148                   Cofidis               France +00:00.53           13
149           Astana Pro Team           Kazakhstan +00:00.41           10
150          Mitchelton-Scott            Australia +00:00.41           11
151          Mitchelton-Scott            Australia +00:00.41           11
152               Team Sunweb          Netherlands +00:00.26            4
153                Team Ineos        Great Britain +00:00.20            2
154                Team Ineos        Great Britain +00:00.20            2
155          Bahrain - Merida              Bahrain +00:00.36            9
156            Direct Energie               France +00:01.42           20
157         UAE Team Emirates United Arab Emirates +00:01.03           16
158              Lotto Soudal              Belgium +00:00.59           15
159 Deceuninck - Quick - Step              Belgium +00:00.21            3
160           Astana Pro Team           Kazakhstan +00:00.41           10
161                  CCC Team               Poland +00:00.31            7
162                Team Ineos        Great Britain +00:00.20            2
163 Deceuninck - Quick - Step              Belgium +00:00.21            3
164             Movistar Team                Spain +00:01.05           17
165            Groupama – FDJ               France +00:00.32            8
166          Bahrain - Merida              Bahrain +00:00.36            9
167                Team Ineos        Great Britain +00:00.20            2
168          Bora - Hansgrohe              Germany +00:00.46           12
169               Team Sunweb          Netherlands +00:00.26            4
170          Bahrain - Merida              Bahrain +00:00.36            9
171              Lotto Soudal              Belgium +00:00.59           15
172            Trek–Segafredo                  USA +00:01.18           18
173        Team Jumbo - Visma          Netherlands  00:28.57            1
174           Fortuneo-Samsic               France +00:01.51           21
175    Team Katusha - Alpecin          Switzerland +00:00.26            5
176               Team Sunweb          Netherlands +00:00.26            4
    dep_city arr_city  classification distance                start_date
1   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
2   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
3   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
4   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
5   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
6   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
7   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
8   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
9   Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
10  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
11  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
12  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
13  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
14  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
15  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
16  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
17  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
18  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
19  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
20  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
21  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
22  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
23  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
24  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
25  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
26  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
27  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
28  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
29  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
30  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
31  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
32  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
33  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
34  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
35  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
36  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
37  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
38  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
39  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
40  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
41  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
42  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
43  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
44  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
45  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
46  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
47  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
48  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
49  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
50  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
51  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
52  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
53  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
54  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
55  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
56  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
57  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
58  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
59  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
60  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
61  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
62  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
63  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
64  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
65  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
66  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
67  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
68  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
69  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
70  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
71  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
72  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
73  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
74  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
75  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
76  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
77  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
78  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
79  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
80  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
81  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
82  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
83  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
84  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
85  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
86  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
87  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
88  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
89  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
90  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
91  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
92  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
93  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
94  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
95  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
96  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
97  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
98  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
99  Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
100 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
101 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
102 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
103 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
104 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
105 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
106 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
107 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
108 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
109 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
110 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
111 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
112 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
113 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
114 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
115 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
116 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
117 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
118 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
119 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
120 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
121 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
122 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
123 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
124 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
125 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
126 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
127 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
128 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
129 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
130 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
131 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
132 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
133 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
134 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
135 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
136 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
137 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
138 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
139 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
140 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
141 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
142 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
143 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
144 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
145 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
146 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
147 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
148 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
149 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
150 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
151 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
152 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
153 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
154 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
155 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
156 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
157 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
158 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
159 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
160 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
161 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
162 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
163 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
164 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
165 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
166 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
167 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
168 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
169 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
170 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
171 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
172 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
173 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
174 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
175 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
176 Brussels Brussels Team Time Trial     27,6 2019-07-07T12:30:00+00:00
```


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
  whole_stage <- whole_stage %>%
    select(stage = description, rider_name = name.x, rider_nat = nationality.x, team_name = team.name, team_nat = team.nationality, time = result.time, time_rank = result.time_ranking, team_time = result.team_time, team_rank = result.team_time_ranking, sprint_pts = result.sprint, sprint_rank = result.sprint_ranking, climb_pts = result.climber, climb_rank = result.climber_ranking, young_rider_time = result.young_rider, young_rider_rank = result.young_rider_ranking, dep_city = departure_city, arr_city = arrival_city, classification, distance, start_date = scheduled)
```


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
compile_stage(2)
```

```
                      id                                 name.x gender.x
1    sr:competitor:26658                    Valverde, Alejandro     male
2   sr:competitor:135930                             Haig, Jack     male
3   sr:competitor:123892                            Yates, Adam     male
4   sr:competitor:310616                         Scully, Thomas     male
5   sr:competitor:123378                         Zakarin, Ilnur     male
6   sr:competitor:135922                            Ewan, Caleb     male
7   sr:competitor:135938                         Mohoric, Matej     male
8   sr:competitor:135924                    Alaphilippe, Julian     male
9   sr:competitor:135926                            Zabel, Rick     male
10  sr:competitor:146106                        Stuyven, Jasper     male
11  sr:competitor:135946                       Bettiol, Alberto     male
12  sr:competitor:123886                 Kragh Andersen, Soeren     male
13  sr:competitor:146110                      van Baarle, Dylan     male
14  sr:competitor:147128                     Bonifazio, Niccolo     male
15  sr:competitor:198734                     Rossetto, Stephane     male
16  sr:competitor:208169                    Laporte, Christophe     male
17  sr:competitor:197808                          Benoot, Tiesj     male
18  sr:competitor:171236                       de Buyst, Jasper     male
19  sr:competitor:196712                           Teuns, Dylan     male
20  sr:competitor:174908                         Woods, Michael     male
21  sr:competitor:123888                           Yates, Simon     male
22  sr:competitor:123880              Valgren Andersen, Michael     male
23  sr:competitor:199422                           Kung, Stefan     male
24   sr:competitor:92871             Verona Quintanilla, Carlos     male
25   sr:competitor:78671                           Molard, Rudy     male
26   sr:competitor:80287                           Wellens, Tim     male
27   sr:competitor:80289                            Houle, Hugo     male
28   sr:competitor:81383          Janse van Rensburg, Reinhardt     male
29   sr:competitor:88952                       Gougeard, Alexis     male
30   sr:competitor:82007                             Aru, Fabio     male
31   sr:competitor:91766                        Barguil, Warren     male
32   sr:competitor:91768                     Vuillermoz, Alexis     male
33   sr:competitor:93161                         Lampaert, Yves     male
34  sr:competitor:123874                   Nielsen, Magnus Cort     male
35   sr:competitor:93179                          Arndt, Nikias     male
36   sr:competitor:93813                       Lutsenko, Alexey     male
37   sr:competitor:93811                 Fraile Matarranz, Omar     male
38   sr:competitor:94613                   Perichon, Pierre-Luc     male
39   sr:competitor:95635                 Reichenbach, Sebastien     male
40  sr:competitor:146340                             Haga, Chad     male
41  sr:competitor:101459                       Berhane, Natnael     male
42  sr:competitor:123856                    Bystroem, Sven Erik     male
43  sr:competitor:318361                 Schachmann, Maximilian     male
44  sr:competitor:226716                          Skujins, Toms     male
45   sr:competitor:67014                         Bardet, Romain     male
46  sr:competitor:310574                     Mas Nicolau, Enric     male
47  sr:competitor:249457                           Politt, Nils     male
48  sr:competitor:246981                      Calmejane, Lilian     male
49  sr:competitor:248863                        Bernard, Julien     male
50  sr:competitor:254335                      Martin, Guillaume     male
51  sr:competitor:313921                           Bernal, Egan     male
52  sr:competitor:282491                       Grellier, Fabien     male
53  sr:competitor:286739                         de Gendt, Aime     male
54  sr:competitor:313919                   Garcia Cortina, Ivan     male
55  sr:competitor:319169                Jansen Groendahl, Amund     male
56  sr:competitor:226972 Richeze Araquistain, Ariel Maximiliano     male
57  sr:competitor:317941                         Kamna, Lennard     male
58  sr:competitor:323145                           Gaudu, David     male
59  sr:competitor:325989                         Perez, Anthony     male
60  sr:competitor:329997                          Gesbert, Elie     male
61  sr:competitor:330003                         Ourselin, Paul     male
62  sr:competitor:353504                         Van Aert, Wout     male
63  sr:competitor:379864                      Cosnefroy, Benoit     male
64  sr:competitor:379848                      Philipsen, Jasper     male
65  sr:competitor:241178                         Bevin, Patrick     male
66  sr:competitor:248853                       de Plus, Laurens     male
67  sr:competitor:198722                        Teunissen, Mike     male
68  sr:competitor:198994                        Turgis, Anthony     male
69  sr:competitor:196754                        Ledanois, Kevin     male
70  sr:competitor:254977                     Wisniowski, Lukasz     male
71  sr:competitor:194902                        Konrad, Patrick     male
72  sr:competitor:219922                     Groenewegen, Dylan     male
73  sr:competitor:197934                        Naesen, Olivier     male
74  sr:competitor:196762                    Soler Gimenez, Marc     male
75  sr:competitor:196774                      Backaert, Fredrik     male
76  sr:competitor:198720                         Rosskopf, Joey     male
77  sr:competitor:250457                         Moscon, Gianni     male
78  sr:competitor:323211                       Meurisse, Xandro     male
79  sr:competitor:201073                      Buchmann, Emanuel     male
80  sr:competitor:226826                     Postlberger, Lukas     male
81  sr:competitor:252831                        Ciccone, Giulio     male
82  sr:competitor:246979                  Eiking, Odd Christian     male
83  sr:competitor:247361                     Muhlberger, Gregor     male
84  sr:competitor:318333                    Wurtz Schmidt, Mads     male
85  sr:competitor:318335                        Asgreen, Kasper     male
86  sr:competitor:221492                        Goncalves, Jose     male
87   sr:competitor:69216                        Bennett, George     male
88   sr:competitor:66830                  Laengen, Vegard Stake     male
89   sr:competitor:26697                 Sanchez Gil, Luis Leon     male
90   sr:competitor:27911                          Roux, Anthony     male
91   sr:competitor:27768                        Thomas, Geraint     male
92   sr:competitor:27770                        Fuglsang, Jakob     male
93   sr:competitor:27851                           Impey, Daryl     male
94   sr:competitor:27883                         Kangert, Tanel     male
95   sr:competitor:27884                  Hagen, Edvald Boasson     male
96   sr:competitor:27886                           Martin, Tony     male
97   sr:competitor:27895                         Mollema, Bauke     male
98   sr:competitor:27907                         Frank, Mathias     male
99   sr:competitor:27913                         Offredo, Yoann     male
100  sr:competitor:27667                          Clarke, Simon     male
101  sr:competitor:27916                         Taaramae, Rein     male
102  sr:competitor:27922                          Simon, Julien     male
103  sr:competitor:27926                          Porte, Richie     male
104  sr:competitor:27968                          Bouet, Maxime     male
105  sr:competitor:27970                         Martin, Daniel     male
106  sr:competitor:41621                           Kluge, Roger     male
107  sr:competitor:34530            Faria Da Costa, Rui Alberto     male
108  sr:competitor:44301                         Gallopin, Tony     male
109  sr:competitor:27762                         Cherel, Mikael     male
110  sr:competitor:27654                         Terpstra, Niki     male
111  sr:competitor:34405                         Amador, Andrey     male
112  sr:competitor:27072                      Burghardt, Marcus     male
113  sr:competitor:26766                       Bak, Lars Ytting     male
114  sr:competitor:26792                       Nibali, Vincenzo     male
115  sr:competitor:26822                          De Kort, Koen     male
116  sr:competitor:26862                        Monfort, Maxime     male
117  sr:competitor:26921                         Roche, Nicolas     male
118  sr:competitor:26931                         Erviti, Imanol     male
119  sr:competitor:26973                         Greipel, Andre     male
120  sr:competitor:27050                         Moinard, Amael     male
121  sr:competitor:27183                       Cummings, Steven     male
122  sr:competitor:27623                     Van Avermaet, Greg     male
123  sr:competitor:27345                        Uran, Rigoberto     male
124  sr:competitor:27397                        Bonnet, William     male
125  sr:competitor:27407                   Langeveld, Sebastian     male
126  sr:competitor:27412                         Pauwels, Serge     male
127  sr:competitor:27446                       Kreuziger, Roman     male
128  sr:competitor:27499                        Schaer, Michael     male
129  sr:competitor:27603                    Ladagnous, Matthieu     male
130  sr:competitor:27620                        Devenyns, Dries     male
131  sr:competitor:35498                    Van Garderen, Tejay     male
132  sr:competitor:34406                            Oss, Daniel     male
133  sr:competitor:68002                          Haller, Marco     male
134  sr:competitor:50026                       Nizzolo, Giacomo     male
135  sr:competitor:67711             Henao Montoya, Sergio Luis     male
136  sr:competitor:47984                        Durbridge, Luke     male
137  sr:competitor:47989                       Hepburn, Michael     male
138  sr:competitor:49209                         King, Benjamin     male
139  sr:competitor:49569                        Vachon, Florian     male
140  sr:competitor:49953                  de Marchi, Alessandro     male
141  sr:competitor:49955                      Pasqualon, Andrea     male
142  sr:competitor:50044                        Quintana, Nairo     male
143  sr:competitor:50032                          Edet, Nicolas     male
144  sr:competitor:50287                     Landa Meana, Mikel     male
145  sr:competitor:50048                           Tratnik, Jan     male
146  sr:competitor:50313                      van Melsen, Kevin     male
147  sr:competitor:50588                      Debusschere, Jens     male
148  sr:competitor:50710                   Herrada Lopez, Jesus     male
149  sr:competitor:51780                          Bilbao, Pello     male
150  sr:competitor:55679               Juul-Jensen, Christopher     male
151  sr:competitor:54471                        Trentin, Matteo     male
152  sr:competitor:62830                       Kelderman, Wilco     male
153  sr:competitor:50288                    Kwiatkowski, Michal     male
154  sr:competitor:50285                             Rowe, Luke     male
155  sr:competitor:49690                        Caruso, Damiano     male
156  sr:competitor:39813                         Sicard, Romain     male
157  sr:competitor:41433                    Kristoff, Alexander     male
158  sr:competitor:35401                       De Gendt, Thomas     male
159  sr:competitor:44092                          Viviani, Elia     male
160  sr:competitor:35470               Izagirre Insausti, Gorka     male
161  sr:competitor:35557                         Geschke, Simon     male
162  sr:competitor:35558                          Poels, Wouter     male
163  sr:competitor:36863                      Moerkoev, Michael     male
164  sr:competitor:50262  Santos Simoes Oliveira, Nelson Filipe     male
165  sr:competitor:39816                         Pinot, Thibaut     male
166  sr:competitor:50283                       Colbrelli, Sonny     male
167  sr:competitor:39819          Castroviejo, Nicolas Jonathan     male
168  sr:competitor:39823                           Sagan, Peter     male
169  sr:competitor:39828                      Matthews, Michael     male
170  sr:competitor:39829                          Dennis, Rohan     male
171  sr:competitor:41623                       Keukeleire, Jens     male
172  sr:competitor:41444                         Felline, Fabio     male
173  sr:competitor:41446                     Kruijswijk, Steven     male
174  sr:competitor:42654                     Delaplace, Anthony     male
175  sr:competitor:50281                          Dowsett, Alex     male
176 sr:competitor:532557                              Bol, Cees     male
     nationality.x country_code.x              team.id
1            Spain            ESP  sr:competitor:26600
2        Australia            AUS  sr:competitor:62812
3    Great Britain            GBR  sr:competitor:62812
4      New Zealand            NZL  sr:competitor:27747
5           Russia            RUS  sr:competitor:33029
6        Australia            AUS  sr:competitor:27616
7         Slovenia            SVN  sr:competitor:26395
8           France            FRA  sr:competitor:26520
9          Germany            DEU  sr:competitor:33029
10         Belgium            BEL  sr:competitor:62896
11           Italy            ITA  sr:competitor:27747
12         Denmark            DNK sr:competitor:310638
13     Netherlands            NLD  sr:competitor:39815
14           Italy            ITA sr:competitor:246991
15          France            FRA  sr:competitor:26495
16          France            FRA  sr:competitor:26495
17         Belgium            BEL  sr:competitor:27616
18         Belgium            BEL  sr:competitor:27616
19         Belgium            BEL  sr:competitor:26395
20          Canada            CAN  sr:competitor:27747
21   Great Britain            GBR  sr:competitor:62812
22         Denmark            DNK  sr:competitor:80955
23     Switzerland            CHE  sr:competitor:26516
24           Spain            ESP  sr:competitor:26600
25          France            FRA  sr:competitor:26516
26         Belgium            BEL  sr:competitor:27616
27          Canada            CAN  sr:competitor:26598
28    South Africa            ZAF  sr:competitor:80955
29          France            FRA  sr:competitor:26519
30           Italy            ITA sr:competitor:310636
31          France            FRA sr:competitor:246989
32          France            FRA  sr:competitor:26519
33         Belgium            BEL  sr:competitor:26520
34         Denmark            DNK  sr:competitor:26598
35         Germany            DEU sr:competitor:310638
36      Kazakhstan            KAZ  sr:competitor:26598
37           Spain            ESP  sr:competitor:26598
38          France            FRA  sr:competitor:26495
39     Switzerland            CHE  sr:competitor:26516
40             USA            USA sr:competitor:310638
41         Eritrea            ERI  sr:competitor:26495
42          Norway            NOR sr:competitor:310636
43         Germany            DEU  sr:competitor:50271
44          Latvia            LVA  sr:competitor:62896
45          France            FRA  sr:competitor:26519
46           Spain            ESP  sr:competitor:26520
47         Germany            DEU  sr:competitor:33029
48          France            FRA sr:competitor:246991
49          France            FRA  sr:competitor:62896
50          France            FRA  sr:competitor:49122
51        Colombia            COL  sr:competitor:39815
52          France            FRA sr:competitor:246991
53         Belgium            BEL  sr:competitor:49122
54           Spain            ESP  sr:competitor:26395
55          Norway            NOR sr:competitor:189354
56       Argentina            ARG  sr:competitor:26520
57         Germany            DEU sr:competitor:310638
58          France            FRA  sr:competitor:26516
59          France            FRA  sr:competitor:26495
60          France            FRA sr:competitor:246989
61          France            FRA sr:competitor:246991
62         Belgium            BEL sr:competitor:189354
63          France            FRA  sr:competitor:26519
64         Belgium            BEL sr:competitor:310636
65     New Zealand            NZL  sr:competitor:27981
66         Belgium            BEL sr:competitor:189354
67     Netherlands            NLD sr:competitor:189354
68          France            FRA sr:competitor:246991
69          France            FRA sr:competitor:246989
70          Poland            POL  sr:competitor:27981
71         Austria            AUT  sr:competitor:50271
72     Netherlands            NLD sr:competitor:189354
73         Belgium            BEL  sr:competitor:26519
74           Spain            ESP  sr:competitor:26600
75         Belgium            BEL  sr:competitor:49122
76             USA            USA  sr:competitor:27981
77           Italy            ITA  sr:competitor:39815
78         Belgium            BEL  sr:competitor:49122
79         Germany            DEU  sr:competitor:50271
80         Austria            AUT  sr:competitor:50271
81           Italy            ITA  sr:competitor:62896
82          Norway            NOR  sr:competitor:49122
83         Austria            AUT  sr:competitor:50271
84         Denmark            DNK  sr:competitor:33029
85         Denmark            DNK  sr:competitor:26520
86        Portugal            PRT  sr:competitor:33029
87     New Zealand            NZL sr:competitor:189354
88          Norway            NOR sr:competitor:310636
89           Spain            ESP  sr:competitor:26598
90          France            FRA  sr:competitor:26516
91   Great Britain            GBR  sr:competitor:39815
92         Denmark            DNK  sr:competitor:26598
93    South Africa            ZAF  sr:competitor:62812
94         Estonia            EST  sr:competitor:27747
95          Norway            NOR  sr:competitor:80955
96         Germany            DEU sr:competitor:189354
97     Netherlands            NLD  sr:competitor:62896
98     Switzerland            CHE  sr:competitor:26519
99          France            FRA  sr:competitor:49122
100      Australia            AUS  sr:competitor:27747
101        Estonia            EST sr:competitor:246991
102         France            FRA  sr:competitor:26495
103      Australia            AUS  sr:competitor:62896
104         France            FRA sr:competitor:246989
105        Ireland            IRL sr:competitor:310636
106        Germany            DEU  sr:competitor:27616
107       Portugal            PRT sr:competitor:310636
108         France            FRA  sr:competitor:26519
109         France            FRA  sr:competitor:26519
110    Netherlands            NLD sr:competitor:246991
111     Costa Rica            CRI  sr:competitor:26600
112        Germany            DEU  sr:competitor:50271
113        Denmark            DNK  sr:competitor:80955
114          Italy            ITA  sr:competitor:26395
115    Netherlands            NLD  sr:competitor:62896
116         France            FRA  sr:competitor:27616
117        Ireland            IRL sr:competitor:310638
118          Spain            ESP  sr:competitor:26600
119        Germany            DEU sr:competitor:246989
120         France            FRA sr:competitor:246989
121  Great Britain            GBR  sr:competitor:80955
122        Belgium            BEL  sr:competitor:27981
123       Colombia            COL  sr:competitor:27747
124         France            FRA  sr:competitor:26516
125    Netherlands            NLD  sr:competitor:27747
126        Belgium            BEL  sr:competitor:27981
127 Czech Republic            CZE  sr:competitor:80955
128    Switzerland            CHE  sr:competitor:27981
129         France            FRA  sr:competitor:26516
130        Belgium            BEL  sr:competitor:26520
131            USA            USA  sr:competitor:27747
132          Italy            ITA  sr:competitor:50271
133        Austria            AUT  sr:competitor:33029
134          Italy            ITA  sr:competitor:80955
135       Colombia            COL sr:competitor:310636
136      Australia            AUS  sr:competitor:62812
137      Australia            AUS  sr:competitor:62812
138            USA            USA  sr:competitor:80955
139         France            FRA sr:competitor:246989
140          Italy            ITA  sr:competitor:27981
141          Italy            ITA  sr:competitor:49122
142       Colombia            COL  sr:competitor:26600
143         France            FRA  sr:competitor:26495
144          Spain            ESP  sr:competitor:26600
145       Slovenia            SVN  sr:competitor:26395
146        Belgium            BEL  sr:competitor:49122
147        Belgium            BEL  sr:competitor:33029
148          Spain            ESP  sr:competitor:26495
149          Spain            ESP  sr:competitor:26598
150        Denmark            DNK  sr:competitor:62812
151          Italy            ITA  sr:competitor:62812
152    Netherlands            NLD sr:competitor:310638
153         Poland            POL  sr:competitor:39815
154  Great Britain            GBR  sr:competitor:39815
155          Italy            ITA  sr:competitor:26395
156         France            FRA sr:competitor:246991
157         Norway            NOR sr:competitor:310636
158        Belgium            BEL  sr:competitor:27616
159          Italy            ITA  sr:competitor:26520
160          Spain            ESP  sr:competitor:26598
161        Germany            DEU  sr:competitor:27981
162    Netherlands            NLD  sr:competitor:39815
163        Denmark            DNK  sr:competitor:26520
164       Portugal            PRT  sr:competitor:26600
165         France            FRA  sr:competitor:26516
166          Italy            ITA  sr:competitor:26395
167          Spain            ESP  sr:competitor:39815
168       Slovakia            SVK  sr:competitor:50271
169      Australia            AUS sr:competitor:310638
170      Australia            AUS  sr:competitor:26395
171        Belgium            BEL  sr:competitor:27616
172          Italy            ITA  sr:competitor:62896
173    Netherlands            NLD sr:competitor:189354
174         France            FRA sr:competitor:246989
175  Great Britain            GBR  sr:competitor:33029
176    Netherlands            NLD sr:competitor:310638
                    team.name team.gender     team.nationality
1               Movistar Team        male                Spain
2            Mitchelton-Scott        male            Australia
3            Mitchelton-Scott        male            Australia
4          EF Education First        male                  USA
5      Team Katusha - Alpecin        male          Switzerland
6                Lotto Soudal        male              Belgium
7            Bahrain - Merida        male              Bahrain
8   Deceuninck - Quick - Step        male              Belgium
9      Team Katusha - Alpecin        male          Switzerland
10             Trek–Segafredo        male                  USA
11         EF Education First        male                  USA
12                Team Sunweb        male          Netherlands
13                 Team Ineos        male        Great Britain
14             Direct Energie        male               France
15                    Cofidis        male               France
16                    Cofidis        male               France
17               Lotto Soudal        male              Belgium
18               Lotto Soudal        male              Belgium
19           Bahrain - Merida        male              Bahrain
20         EF Education First        male                  USA
21           Mitchelton-Scott        male            Australia
22        Team Dimension Data        male         South Africa
23             Groupama – FDJ        male               France
24              Movistar Team        male                Spain
25             Groupama – FDJ        male               France
26               Lotto Soudal        male              Belgium
27            Astana Pro Team        male           Kazakhstan
28        Team Dimension Data        male         South Africa
29           Ag2r La Mondiale        male               France
30          UAE Team Emirates        male United Arab Emirates
31            Fortuneo-Samsic        male               France
32           Ag2r La Mondiale        male               France
33  Deceuninck - Quick - Step        male              Belgium
34            Astana Pro Team        male           Kazakhstan
35                Team Sunweb        male          Netherlands
36            Astana Pro Team        male           Kazakhstan
37            Astana Pro Team        male           Kazakhstan
38                    Cofidis        male               France
39             Groupama – FDJ        male               France
40                Team Sunweb        male          Netherlands
41                    Cofidis        male               France
42          UAE Team Emirates        male United Arab Emirates
43           Bora - Hansgrohe        male              Germany
44             Trek–Segafredo        male                  USA
45           Ag2r La Mondiale        male               France
46  Deceuninck - Quick - Step        male              Belgium
47     Team Katusha - Alpecin        male          Switzerland
48             Direct Energie        male               France
49             Trek–Segafredo        male                  USA
50        Wanty Groupe Gobert        male              Belgium
51                 Team Ineos        male        Great Britain
52             Direct Energie        male               France
53        Wanty Groupe Gobert        male              Belgium
54           Bahrain - Merida        male              Bahrain
55         Team Jumbo - Visma        male          Netherlands
56  Deceuninck - Quick - Step        male              Belgium
57                Team Sunweb        male          Netherlands
58             Groupama – FDJ        male               France
59                    Cofidis        male               France
60            Fortuneo-Samsic        male               France
61             Direct Energie        male               France
62         Team Jumbo - Visma        male          Netherlands
63           Ag2r La Mondiale        male               France
64          UAE Team Emirates        male United Arab Emirates
65                   CCC Team        male               Poland
66         Team Jumbo - Visma        male          Netherlands
67         Team Jumbo - Visma        male          Netherlands
68             Direct Energie        male               France
69            Fortuneo-Samsic        male               France
70                   CCC Team        male               Poland
71           Bora - Hansgrohe        male              Germany
72         Team Jumbo - Visma        male          Netherlands
73           Ag2r La Mondiale        male               France
74              Movistar Team        male                Spain
75        Wanty Groupe Gobert        male              Belgium
76                   CCC Team        male               Poland
77                 Team Ineos        male        Great Britain
78        Wanty Groupe Gobert        male              Belgium
79           Bora - Hansgrohe        male              Germany
80           Bora - Hansgrohe        male              Germany
81             Trek–Segafredo        male                  USA
82        Wanty Groupe Gobert        male              Belgium
83           Bora - Hansgrohe        male              Germany
84     Team Katusha - Alpecin        male          Switzerland
85  Deceuninck - Quick - Step        male              Belgium
86     Team Katusha - Alpecin        male          Switzerland
87         Team Jumbo - Visma        male          Netherlands
88          UAE Team Emirates        male United Arab Emirates
89            Astana Pro Team        male           Kazakhstan
90             Groupama – FDJ        male               France
91                 Team Ineos        male        Great Britain
92            Astana Pro Team        male           Kazakhstan
93           Mitchelton-Scott        male            Australia
94         EF Education First        male                  USA
95        Team Dimension Data        male         South Africa
96         Team Jumbo - Visma        male          Netherlands
97             Trek–Segafredo        male                  USA
98           Ag2r La Mondiale        male               France
99        Wanty Groupe Gobert        male              Belgium
100        EF Education First        male                  USA
101            Direct Energie        male               France
102                   Cofidis        male               France
103            Trek–Segafredo        male                  USA
104           Fortuneo-Samsic        male               France
105         UAE Team Emirates        male United Arab Emirates
106              Lotto Soudal        male              Belgium
107         UAE Team Emirates        male United Arab Emirates
108          Ag2r La Mondiale        male               France
109          Ag2r La Mondiale        male               France
110            Direct Energie        male               France
111             Movistar Team        male                Spain
112          Bora - Hansgrohe        male              Germany
113       Team Dimension Data        male         South Africa
114          Bahrain - Merida        male              Bahrain
115            Trek–Segafredo        male                  USA
116              Lotto Soudal        male              Belgium
117               Team Sunweb        male          Netherlands
118             Movistar Team        male                Spain
119           Fortuneo-Samsic        male               France
120           Fortuneo-Samsic        male               France
121       Team Dimension Data        male         South Africa
122                  CCC Team        male               Poland
123        EF Education First        male                  USA
124            Groupama – FDJ        male               France
125        EF Education First        male                  USA
126                  CCC Team        male               Poland
127       Team Dimension Data        male         South Africa
128                  CCC Team        male               Poland
129            Groupama – FDJ        male               France
130 Deceuninck - Quick - Step        male              Belgium
131        EF Education First        male                  USA
132          Bora - Hansgrohe        male              Germany
133    Team Katusha - Alpecin        male          Switzerland
134       Team Dimension Data        male         South Africa
135         UAE Team Emirates        male United Arab Emirates
136          Mitchelton-Scott        male            Australia
137          Mitchelton-Scott        male            Australia
138       Team Dimension Data        male         South Africa
139           Fortuneo-Samsic        male               France
140                  CCC Team        male               Poland
141       Wanty Groupe Gobert        male              Belgium
142             Movistar Team        male                Spain
143                   Cofidis        male               France
144             Movistar Team        male                Spain
145          Bahrain - Merida        male              Bahrain
146       Wanty Groupe Gobert        male              Belgium
147    Team Katusha - Alpecin        male          Switzerland
148                   Cofidis        male               France
149           Astana Pro Team        male           Kazakhstan
150          Mitchelton-Scott        male            Australia
151          Mitchelton-Scott        male            Australia
152               Team Sunweb        male          Netherlands
153                Team Ineos        male        Great Britain
154                Team Ineos        male        Great Britain
155          Bahrain - Merida        male              Bahrain
156            Direct Energie        male               France
157         UAE Team Emirates        male United Arab Emirates
158              Lotto Soudal        male              Belgium
159 Deceuninck - Quick - Step        male              Belgium
160           Astana Pro Team        male           Kazakhstan
161                  CCC Team        male               Poland
162                Team Ineos        male        Great Britain
163 Deceuninck - Quick - Step        male              Belgium
164             Movistar Team        male                Spain
165            Groupama – FDJ        male               France
166          Bahrain - Merida        male              Bahrain
167                Team Ineos        male        Great Britain
168          Bora - Hansgrohe        male              Germany
169               Team Sunweb        male          Netherlands
170          Bahrain - Merida        male              Bahrain
171              Lotto Soudal        male              Belgium
172            Trek–Segafredo        male                  USA
173        Team Jumbo - Visma        male          Netherlands
174           Fortuneo-Samsic        male               France
175    Team Katusha - Alpecin        male          Switzerland
176               Team Sunweb        male          Netherlands
    team.country_code description                    name.y gender.y
1                 ESP     Stage 2             Movistar Team     male
2                 AUS     Stage 2          Mitchelton-Scott     male
3                 AUS     Stage 2          Mitchelton-Scott     male
4                 USA     Stage 2        EF Education First     male
5                 CHE     Stage 2    Team Katusha - Alpecin     male
6                 BEL     Stage 2              Lotto Soudal     male
7                 BHR     Stage 2          Bahrain - Merida     male
8                 BEL     Stage 2 Deceuninck - Quick - Step     male
9                 CHE     Stage 2    Team Katusha - Alpecin     male
10                USA     Stage 2            Trek–Segafredo     male
11                USA     Stage 2        EF Education First     male
12                NLD     Stage 2               Team Sunweb     male
13                GBR     Stage 2                Team Ineos     male
14                FRA     Stage 2            Direct Energie     male
15                FRA     Stage 2                   Cofidis     male
16                FRA     Stage 2                   Cofidis     male
17                BEL     Stage 2              Lotto Soudal     male
18                BEL     Stage 2              Lotto Soudal     male
19                BHR     Stage 2          Bahrain - Merida     male
20                USA     Stage 2        EF Education First     male
21                AUS     Stage 2          Mitchelton-Scott     male
22                ZAF     Stage 2       Team Dimension Data     male
23                FRA     Stage 2            Groupama – FDJ     male
24                ESP     Stage 2             Movistar Team     male
25                FRA     Stage 2            Groupama – FDJ     male
26                BEL     Stage 2              Lotto Soudal     male
27                KAZ     Stage 2           Astana Pro Team     male
28                ZAF     Stage 2       Team Dimension Data     male
29                FRA     Stage 2          Ag2r La Mondiale     male
30                ARE     Stage 2         UAE Team Emirates     male
31                FRA     Stage 2           Fortuneo-Samsic     male
32                FRA     Stage 2          Ag2r La Mondiale     male
33                BEL     Stage 2 Deceuninck - Quick - Step     male
34                KAZ     Stage 2           Astana Pro Team     male
35                NLD     Stage 2               Team Sunweb     male
36                KAZ     Stage 2           Astana Pro Team     male
37                KAZ     Stage 2           Astana Pro Team     male
38                FRA     Stage 2                   Cofidis     male
39                FRA     Stage 2            Groupama – FDJ     male
40                NLD     Stage 2               Team Sunweb     male
41                FRA     Stage 2                   Cofidis     male
42                ARE     Stage 2         UAE Team Emirates     male
43                DEU     Stage 2          Bora - Hansgrohe     male
44                USA     Stage 2            Trek–Segafredo     male
45                FRA     Stage 2          Ag2r La Mondiale     male
46                BEL     Stage 2 Deceuninck - Quick - Step     male
47                CHE     Stage 2    Team Katusha - Alpecin     male
48                FRA     Stage 2            Direct Energie     male
49                USA     Stage 2            Trek–Segafredo     male
50                BEL     Stage 2       Wanty Groupe Gobert     male
51                GBR     Stage 2                Team Ineos     male
52                FRA     Stage 2            Direct Energie     male
53                BEL     Stage 2       Wanty Groupe Gobert     male
54                BHR     Stage 2          Bahrain - Merida     male
55                NLD     Stage 2        Team Jumbo - Visma     male
56                BEL     Stage 2 Deceuninck - Quick - Step     male
57                NLD     Stage 2               Team Sunweb     male
58                FRA     Stage 2            Groupama – FDJ     male
59                FRA     Stage 2                   Cofidis     male
60                FRA     Stage 2           Fortuneo-Samsic     male
61                FRA     Stage 2            Direct Energie     male
62                NLD     Stage 2        Team Jumbo - Visma     male
63                FRA     Stage 2          Ag2r La Mondiale     male
64                ARE     Stage 2         UAE Team Emirates     male
65                POL     Stage 2                  CCC Team     male
66                NLD     Stage 2        Team Jumbo - Visma     male
67                NLD     Stage 2        Team Jumbo - Visma     male
68                FRA     Stage 2            Direct Energie     male
69                FRA     Stage 2           Fortuneo-Samsic     male
70                POL     Stage 2                  CCC Team     male
71                DEU     Stage 2          Bora - Hansgrohe     male
72                NLD     Stage 2        Team Jumbo - Visma     male
73                FRA     Stage 2          Ag2r La Mondiale     male
74                ESP     Stage 2             Movistar Team     male
75                BEL     Stage 2       Wanty Groupe Gobert     male
76                POL     Stage 2                  CCC Team     male
77                GBR     Stage 2                Team Ineos     male
78                BEL     Stage 2       Wanty Groupe Gobert     male
79                DEU     Stage 2          Bora - Hansgrohe     male
80                DEU     Stage 2          Bora - Hansgrohe     male
81                USA     Stage 2            Trek–Segafredo     male
82                BEL     Stage 2       Wanty Groupe Gobert     male
83                DEU     Stage 2          Bora - Hansgrohe     male
84                CHE     Stage 2    Team Katusha - Alpecin     male
85                BEL     Stage 2 Deceuninck - Quick - Step     male
86                CHE     Stage 2    Team Katusha - Alpecin     male
87                NLD     Stage 2        Team Jumbo - Visma     male
88                ARE     Stage 2         UAE Team Emirates     male
89                KAZ     Stage 2           Astana Pro Team     male
90                FRA     Stage 2            Groupama – FDJ     male
91                GBR     Stage 2                Team Ineos     male
92                KAZ     Stage 2           Astana Pro Team     male
93                AUS     Stage 2          Mitchelton-Scott     male
94                USA     Stage 2        EF Education First     male
95                ZAF     Stage 2       Team Dimension Data     male
96                NLD     Stage 2        Team Jumbo - Visma     male
97                USA     Stage 2            Trek–Segafredo     male
98                FRA     Stage 2          Ag2r La Mondiale     male
99                BEL     Stage 2       Wanty Groupe Gobert     male
100               USA     Stage 2        EF Education First     male
101               FRA     Stage 2            Direct Energie     male
102               FRA     Stage 2                   Cofidis     male
103               USA     Stage 2            Trek–Segafredo     male
104               FRA     Stage 2           Fortuneo-Samsic     male
105               ARE     Stage 2         UAE Team Emirates     male
106               BEL     Stage 2              Lotto Soudal     male
107               ARE     Stage 2         UAE Team Emirates     male
108               FRA     Stage 2          Ag2r La Mondiale     male
109               FRA     Stage 2          Ag2r La Mondiale     male
110               FRA     Stage 2            Direct Energie     male
111               ESP     Stage 2             Movistar Team     male
112               DEU     Stage 2          Bora - Hansgrohe     male
113               ZAF     Stage 2       Team Dimension Data     male
114               BHR     Stage 2          Bahrain - Merida     male
115               USA     Stage 2            Trek–Segafredo     male
116               BEL     Stage 2              Lotto Soudal     male
117               NLD     Stage 2               Team Sunweb     male
118               ESP     Stage 2             Movistar Team     male
119               FRA     Stage 2           Fortuneo-Samsic     male
120               FRA     Stage 2           Fortuneo-Samsic     male
121               ZAF     Stage 2       Team Dimension Data     male
122               POL     Stage 2                  CCC Team     male
123               USA     Stage 2        EF Education First     male
124               FRA     Stage 2            Groupama – FDJ     male
125               USA     Stage 2        EF Education First     male
126               POL     Stage 2                  CCC Team     male
127               ZAF     Stage 2       Team Dimension Data     male
128               POL     Stage 2                  CCC Team     male
129               FRA     Stage 2            Groupama – FDJ     male
130               BEL     Stage 2 Deceuninck - Quick - Step     male
131               USA     Stage 2        EF Education First     male
132               DEU     Stage 2          Bora - Hansgrohe     male
133               CHE     Stage 2    Team Katusha - Alpecin     male
134               ZAF     Stage 2       Team Dimension Data     male
135               ARE     Stage 2         UAE Team Emirates     male
136               AUS     Stage 2          Mitchelton-Scott     male
137               AUS     Stage 2          Mitchelton-Scott     male
138               ZAF     Stage 2       Team Dimension Data     male
139               FRA     Stage 2           Fortuneo-Samsic     male
140               POL     Stage 2                  CCC Team     male
141               BEL     Stage 2       Wanty Groupe Gobert     male
142               ESP     Stage 2             Movistar Team     male
143               FRA     Stage 2                   Cofidis     male
144               ESP     Stage 2             Movistar Team     male
145               BHR     Stage 2          Bahrain - Merida     male
146               BEL     Stage 2       Wanty Groupe Gobert     male
147               CHE     Stage 2    Team Katusha - Alpecin     male
148               FRA     Stage 2                   Cofidis     male
149               KAZ     Stage 2           Astana Pro Team     male
150               AUS     Stage 2          Mitchelton-Scott     male
151               AUS     Stage 2          Mitchelton-Scott     male
152               NLD     Stage 2               Team Sunweb     male
153               GBR     Stage 2                Team Ineos     male
154               GBR     Stage 2                Team Ineos     male
155               BHR     Stage 2          Bahrain - Merida     male
156               FRA     Stage 2            Direct Energie     male
157               ARE     Stage 2         UAE Team Emirates     male
158               BEL     Stage 2              Lotto Soudal     male
159               BEL     Stage 2 Deceuninck - Quick - Step     male
160               KAZ     Stage 2           Astana Pro Team     male
161               POL     Stage 2                  CCC Team     male
162               GBR     Stage 2                Team Ineos     male
163               BEL     Stage 2 Deceuninck - Quick - Step     male
164               ESP     Stage 2             Movistar Team     male
165               FRA     Stage 2            Groupama – FDJ     male
166               BHR     Stage 2          Bahrain - Merida     male
167               GBR     Stage 2                Team Ineos     male
168               DEU     Stage 2          Bora - Hansgrohe     male
169               NLD     Stage 2               Team Sunweb     male
170               BHR     Stage 2          Bahrain - Merida     male
171               BEL     Stage 2              Lotto Soudal     male
172               USA     Stage 2            Trek–Segafredo     male
173               NLD     Stage 2        Team Jumbo - Visma     male
174               FRA     Stage 2           Fortuneo-Samsic     male
175               CHE     Stage 2    Team Katusha - Alpecin     male
176               NLD     Stage 2               Team Sunweb     male
           nationality.y country_code.y result.team_time
1                  Spain            ESP        +00:01.05
2              Australia            AUS        +00:00.41
3              Australia            AUS        +00:00.41
4                    USA            USA        +00:00.28
5            Switzerland            CHE        +00:00.26
6                Belgium            BEL        +00:00.59
7                Bahrain            BHR        +00:00.36
8                Belgium            BEL        +00:00.21
9            Switzerland            CHE        +00:00.26
10                   USA            USA        +00:01.18
11                   USA            USA        +00:00.28
12           Netherlands            NLD        +00:00.26
13         Great Britain            GBR        +00:00.20
14                France            FRA        +00:01.42
15                France            FRA        +00:00.53
16                France            FRA        +00:00.53
17               Belgium            BEL        +00:00.59
18               Belgium            BEL        +00:00.59
19               Bahrain            BHR        +00:00.36
20                   USA            USA        +00:00.28
21             Australia            AUS        +00:00.41
22          South Africa            ZAF        +00:00.54
23                France            FRA        +00:00.32
24                 Spain            ESP        +00:01.05
25                France            FRA        +00:00.32
26               Belgium            BEL        +00:00.59
27            Kazakhstan            KAZ        +00:00.41
28          South Africa            ZAF        +00:00.54
29                France            FRA        +00:01.19
30  United Arab Emirates            ARE        +00:01.03
31                France            FRA        +00:01.51
32                France            FRA        +00:01.19
33               Belgium            BEL        +00:00.21
34            Kazakhstan            KAZ        +00:00.41
35           Netherlands            NLD        +00:00.26
36            Kazakhstan            KAZ        +00:00.41
37            Kazakhstan            KAZ        +00:00.41
38                France            FRA        +00:00.53
39                France            FRA        +00:00.32
40           Netherlands            NLD        +00:00.26
41                France            FRA        +00:00.53
42  United Arab Emirates            ARE        +00:01.03
43               Germany            DEU        +00:00.46
44                   USA            USA        +00:01.18
45                France            FRA        +00:01.19
46               Belgium            BEL        +00:00.21
47           Switzerland            CHE        +00:00.26
48                France            FRA        +00:01.42
49                   USA            USA        +00:01.18
50               Belgium            BEL        +00:01.58
51         Great Britain            GBR        +00:00.20
52                France            FRA        +00:01.42
53               Belgium            BEL        +00:01.58
54               Bahrain            BHR        +00:00.36
55           Netherlands            NLD         00:28.57
56               Belgium            BEL        +00:00.21
57           Netherlands            NLD        +00:00.26
58                France            FRA        +00:00.32
59                France            FRA        +00:00.53
60                France            FRA        +00:01.51
61                France            FRA        +00:01.42
62           Netherlands            NLD         00:28.57
63                France            FRA        +00:01.19
64  United Arab Emirates            ARE        +00:01.03
65                Poland            POL        +00:00.31
66           Netherlands            NLD         00:28.57
67           Netherlands            NLD         00:28.57
68                France            FRA        +00:01.42
69                France            FRA        +00:01.51
70                Poland            POL        +00:00.31
71               Germany            DEU        +00:00.46
72           Netherlands            NLD         00:28.57
73                France            FRA        +00:01.19
74                 Spain            ESP        +00:01.05
75               Belgium            BEL        +00:01.58
76                Poland            POL        +00:00.31
77         Great Britain            GBR        +00:00.20
78               Belgium            BEL        +00:01.58
79               Germany            DEU        +00:00.46
80               Germany            DEU        +00:00.46
81                   USA            USA        +00:01.18
82               Belgium            BEL        +00:01.58
83               Germany            DEU        +00:00.46
84           Switzerland            CHE        +00:00.26
85               Belgium            BEL        +00:00.21
86           Switzerland            CHE        +00:00.26
87           Netherlands            NLD         00:28.57
88  United Arab Emirates            ARE        +00:01.03
89            Kazakhstan            KAZ        +00:00.41
90                France            FRA        +00:00.32
91         Great Britain            GBR        +00:00.20
92            Kazakhstan            KAZ        +00:00.41
93             Australia            AUS        +00:00.41
94                   USA            USA        +00:00.28
95          South Africa            ZAF        +00:00.54
96           Netherlands            NLD         00:28.57
97                   USA            USA        +00:01.18
98                France            FRA        +00:01.19
99               Belgium            BEL        +00:01.58
100                  USA            USA        +00:00.28
101               France            FRA        +00:01.42
102               France            FRA        +00:00.53
103                  USA            USA        +00:01.18
104               France            FRA        +00:01.51
105 United Arab Emirates            ARE        +00:01.03
106              Belgium            BEL        +00:00.59
107 United Arab Emirates            ARE        +00:01.03
108               France            FRA        +00:01.19
109               France            FRA        +00:01.19
110               France            FRA        +00:01.42
111                Spain            ESP        +00:01.05
112              Germany            DEU        +00:00.46
113         South Africa            ZAF        +00:00.54
114              Bahrain            BHR        +00:00.36
115                  USA            USA        +00:01.18
116              Belgium            BEL        +00:00.59
117          Netherlands            NLD        +00:00.26
118                Spain            ESP        +00:01.05
119               France            FRA        +00:01.51
120               France            FRA        +00:01.51
121         South Africa            ZAF        +00:00.54
122               Poland            POL        +00:00.31
123                  USA            USA        +00:00.28
124               France            FRA        +00:00.32
125                  USA            USA        +00:00.28
126               Poland            POL        +00:00.31
127         South Africa            ZAF        +00:00.54
128               Poland            POL        +00:00.31
129               France            FRA        +00:00.32
130              Belgium            BEL        +00:00.21
131                  USA            USA        +00:00.28
132              Germany            DEU        +00:00.46
133          Switzerland            CHE        +00:00.26
134         South Africa            ZAF        +00:00.54
135 United Arab Emirates            ARE        +00:01.03
136            Australia            AUS        +00:00.41
137            Australia            AUS        +00:00.41
138         South Africa            ZAF        +00:00.54
139               France            FRA        +00:01.51
140               Poland            POL        +00:00.31
141              Belgium            BEL        +00:01.58
142                Spain            ESP        +00:01.05
143               France            FRA        +00:00.53
144                Spain            ESP        +00:01.05
145              Bahrain            BHR        +00:00.36
146              Belgium            BEL        +00:01.58
147          Switzerland            CHE        +00:00.26
148               France            FRA        +00:00.53
149           Kazakhstan            KAZ        +00:00.41
150            Australia            AUS        +00:00.41
151            Australia            AUS        +00:00.41
152          Netherlands            NLD        +00:00.26
153        Great Britain            GBR        +00:00.20
154        Great Britain            GBR        +00:00.20
155              Bahrain            BHR        +00:00.36
156               France            FRA        +00:01.42
157 United Arab Emirates            ARE        +00:01.03
158              Belgium            BEL        +00:00.59
159              Belgium            BEL        +00:00.21
160           Kazakhstan            KAZ        +00:00.41
161               Poland            POL        +00:00.31
162        Great Britain            GBR        +00:00.20
163              Belgium            BEL        +00:00.21
164                Spain            ESP        +00:01.05
165               France            FRA        +00:00.32
166              Bahrain            BHR        +00:00.36
167        Great Britain            GBR        +00:00.20
168              Germany            DEU        +00:00.46
169          Netherlands            NLD        +00:00.26
170              Bahrain            BHR        +00:00.36
171              Belgium            BEL        +00:00.59
172                  USA            USA        +00:01.18
173          Netherlands            NLD         00:28.57
174               France            FRA        +00:01.51
175          Switzerland            CHE        +00:00.26
176          Netherlands            NLD        +00:00.26
    result.team_time_ranking                 scheduled
1                         17 2019-07-07T12:30:00+00:00
2                         11 2019-07-07T12:30:00+00:00
3                         11 2019-07-07T12:30:00+00:00
4                          6 2019-07-07T12:30:00+00:00
5                          5 2019-07-07T12:30:00+00:00
6                         15 2019-07-07T12:30:00+00:00
7                          9 2019-07-07T12:30:00+00:00
8                          3 2019-07-07T12:30:00+00:00
9                          5 2019-07-07T12:30:00+00:00
10                        18 2019-07-07T12:30:00+00:00
11                         6 2019-07-07T12:30:00+00:00
12                         4 2019-07-07T12:30:00+00:00
13                         2 2019-07-07T12:30:00+00:00
14                        20 2019-07-07T12:30:00+00:00
15                        13 2019-07-07T12:30:00+00:00
16                        13 2019-07-07T12:30:00+00:00
17                        15 2019-07-07T12:30:00+00:00
18                        15 2019-07-07T12:30:00+00:00
19                         9 2019-07-07T12:30:00+00:00
20                         6 2019-07-07T12:30:00+00:00
21                        11 2019-07-07T12:30:00+00:00
22                        14 2019-07-07T12:30:00+00:00
23                         8 2019-07-07T12:30:00+00:00
24                        17 2019-07-07T12:30:00+00:00
25                         8 2019-07-07T12:30:00+00:00
26                        15 2019-07-07T12:30:00+00:00
27                        10 2019-07-07T12:30:00+00:00
28                        14 2019-07-07T12:30:00+00:00
29                        19 2019-07-07T12:30:00+00:00
30                        16 2019-07-07T12:30:00+00:00
31                        21 2019-07-07T12:30:00+00:00
32                        19 2019-07-07T12:30:00+00:00
33                         3 2019-07-07T12:30:00+00:00
34                        10 2019-07-07T12:30:00+00:00
35                         4 2019-07-07T12:30:00+00:00
36                        10 2019-07-07T12:30:00+00:00
37                        10 2019-07-07T12:30:00+00:00
38                        13 2019-07-07T12:30:00+00:00
39                         8 2019-07-07T12:30:00+00:00
40                         4 2019-07-07T12:30:00+00:00
41                        13 2019-07-07T12:30:00+00:00
42                        16 2019-07-07T12:30:00+00:00
43                        12 2019-07-07T12:30:00+00:00
44                        18 2019-07-07T12:30:00+00:00
45                        19 2019-07-07T12:30:00+00:00
46                         3 2019-07-07T12:30:00+00:00
47                         5 2019-07-07T12:30:00+00:00
48                        20 2019-07-07T12:30:00+00:00
49                        18 2019-07-07T12:30:00+00:00
50                        22 2019-07-07T12:30:00+00:00
51                         2 2019-07-07T12:30:00+00:00
52                        20 2019-07-07T12:30:00+00:00
53                        22 2019-07-07T12:30:00+00:00
54                         9 2019-07-07T12:30:00+00:00
55                         1 2019-07-07T12:30:00+00:00
56                         3 2019-07-07T12:30:00+00:00
57                         4 2019-07-07T12:30:00+00:00
58                         8 2019-07-07T12:30:00+00:00
59                        13 2019-07-07T12:30:00+00:00
60                        21 2019-07-07T12:30:00+00:00
61                        20 2019-07-07T12:30:00+00:00
62                         1 2019-07-07T12:30:00+00:00
63                        19 2019-07-07T12:30:00+00:00
64                        16 2019-07-07T12:30:00+00:00
65                         7 2019-07-07T12:30:00+00:00
66                         1 2019-07-07T12:30:00+00:00
67                         1 2019-07-07T12:30:00+00:00
68                        20 2019-07-07T12:30:00+00:00
69                        21 2019-07-07T12:30:00+00:00
70                         7 2019-07-07T12:30:00+00:00
71                        12 2019-07-07T12:30:00+00:00
72                         1 2019-07-07T12:30:00+00:00
73                        19 2019-07-07T12:30:00+00:00
74                        17 2019-07-07T12:30:00+00:00
75                        22 2019-07-07T12:30:00+00:00
76                         7 2019-07-07T12:30:00+00:00
77                         2 2019-07-07T12:30:00+00:00
78                        22 2019-07-07T12:30:00+00:00
79                        12 2019-07-07T12:30:00+00:00
80                        12 2019-07-07T12:30:00+00:00
81                        18 2019-07-07T12:30:00+00:00
82                        22 2019-07-07T12:30:00+00:00
83                        12 2019-07-07T12:30:00+00:00
84                         5 2019-07-07T12:30:00+00:00
85                         3 2019-07-07T12:30:00+00:00
86                         5 2019-07-07T12:30:00+00:00
87                         1 2019-07-07T12:30:00+00:00
88                        16 2019-07-07T12:30:00+00:00
89                        10 2019-07-07T12:30:00+00:00
90                         8 2019-07-07T12:30:00+00:00
91                         2 2019-07-07T12:30:00+00:00
92                        10 2019-07-07T12:30:00+00:00
93                        11 2019-07-07T12:30:00+00:00
94                         6 2019-07-07T12:30:00+00:00
95                        14 2019-07-07T12:30:00+00:00
96                         1 2019-07-07T12:30:00+00:00
97                        18 2019-07-07T12:30:00+00:00
98                        19 2019-07-07T12:30:00+00:00
99                        22 2019-07-07T12:30:00+00:00
100                        6 2019-07-07T12:30:00+00:00
101                       20 2019-07-07T12:30:00+00:00
102                       13 2019-07-07T12:30:00+00:00
103                       18 2019-07-07T12:30:00+00:00
104                       21 2019-07-07T12:30:00+00:00
105                       16 2019-07-07T12:30:00+00:00
106                       15 2019-07-07T12:30:00+00:00
107                       16 2019-07-07T12:30:00+00:00
108                       19 2019-07-07T12:30:00+00:00
109                       19 2019-07-07T12:30:00+00:00
110                       20 2019-07-07T12:30:00+00:00
111                       17 2019-07-07T12:30:00+00:00
112                       12 2019-07-07T12:30:00+00:00
113                       14 2019-07-07T12:30:00+00:00
114                        9 2019-07-07T12:30:00+00:00
115                       18 2019-07-07T12:30:00+00:00
116                       15 2019-07-07T12:30:00+00:00
117                        4 2019-07-07T12:30:00+00:00
118                       17 2019-07-07T12:30:00+00:00
119                       21 2019-07-07T12:30:00+00:00
120                       21 2019-07-07T12:30:00+00:00
121                       14 2019-07-07T12:30:00+00:00
122                        7 2019-07-07T12:30:00+00:00
123                        6 2019-07-07T12:30:00+00:00
124                        8 2019-07-07T12:30:00+00:00
125                        6 2019-07-07T12:30:00+00:00
126                        7 2019-07-07T12:30:00+00:00
127                       14 2019-07-07T12:30:00+00:00
128                        7 2019-07-07T12:30:00+00:00
129                        8 2019-07-07T12:30:00+00:00
130                        3 2019-07-07T12:30:00+00:00
131                        6 2019-07-07T12:30:00+00:00
132                       12 2019-07-07T12:30:00+00:00
133                        5 2019-07-07T12:30:00+00:00
134                       14 2019-07-07T12:30:00+00:00
135                       16 2019-07-07T12:30:00+00:00
136                       11 2019-07-07T12:30:00+00:00
137                       11 2019-07-07T12:30:00+00:00
138                       14 2019-07-07T12:30:00+00:00
139                       21 2019-07-07T12:30:00+00:00
140                        7 2019-07-07T12:30:00+00:00
141                       22 2019-07-07T12:30:00+00:00
142                       17 2019-07-07T12:30:00+00:00
143                       13 2019-07-07T12:30:00+00:00
144                       17 2019-07-07T12:30:00+00:00
145                        9 2019-07-07T12:30:00+00:00
146                       22 2019-07-07T12:30:00+00:00
147                        5 2019-07-07T12:30:00+00:00
148                       13 2019-07-07T12:30:00+00:00
149                       10 2019-07-07T12:30:00+00:00
150                       11 2019-07-07T12:30:00+00:00
151                       11 2019-07-07T12:30:00+00:00
152                        4 2019-07-07T12:30:00+00:00
153                        2 2019-07-07T12:30:00+00:00
154                        2 2019-07-07T12:30:00+00:00
155                        9 2019-07-07T12:30:00+00:00
156                       20 2019-07-07T12:30:00+00:00
157                       16 2019-07-07T12:30:00+00:00
158                       15 2019-07-07T12:30:00+00:00
159                        3 2019-07-07T12:30:00+00:00
160                       10 2019-07-07T12:30:00+00:00
161                        7 2019-07-07T12:30:00+00:00
162                        2 2019-07-07T12:30:00+00:00
163                        3 2019-07-07T12:30:00+00:00
164                       17 2019-07-07T12:30:00+00:00
165                        8 2019-07-07T12:30:00+00:00
166                        9 2019-07-07T12:30:00+00:00
167                        2 2019-07-07T12:30:00+00:00
168                       12 2019-07-07T12:30:00+00:00
169                        4 2019-07-07T12:30:00+00:00
170                        9 2019-07-07T12:30:00+00:00
171                       15 2019-07-07T12:30:00+00:00
172                       18 2019-07-07T12:30:00+00:00
173                        1 2019-07-07T12:30:00+00:00
174                       21 2019-07-07T12:30:00+00:00
175                        5 2019-07-07T12:30:00+00:00
176                        4 2019-07-07T12:30:00+00:00
                scheduled_end  type departure_city arrival_city status
1   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
2   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
3   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
4   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
5   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
6   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
7   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
8   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
9   2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
10  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
11  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
12  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
13  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
14  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
15  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
16  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
17  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
18  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
19  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
20  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
21  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
22  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
23  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
24  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
25  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
26  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
27  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
28  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
29  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
30  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
31  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
32  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
33  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
34  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
35  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
36  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
37  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
38  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
39  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
40  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
41  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
42  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
43  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
44  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
45  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
46  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
47  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
48  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
49  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
50  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
51  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
52  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
53  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
54  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
55  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
56  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
57  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
58  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
59  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
60  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
61  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
62  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
63  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
64  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
65  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
66  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
67  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
68  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
69  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
70  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
71  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
72  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
73  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
74  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
75  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
76  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
77  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
78  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
79  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
80  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
81  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
82  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
83  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
84  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
85  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
86  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
87  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
88  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
89  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
90  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
91  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
92  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
93  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
94  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
95  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
96  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
97  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
98  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
99  2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
100 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
101 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
102 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
103 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
104 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
105 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
106 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
107 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
108 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
109 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
110 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
111 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
112 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
113 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
114 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
115 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
116 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
117 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
118 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
119 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
120 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
121 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
122 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
123 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
124 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
125 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
126 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
127 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
128 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
129 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
130 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
131 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
132 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
133 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
134 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
135 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
136 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
137 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
138 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
139 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
140 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
141 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
142 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
143 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
144 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
145 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
146 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
147 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
148 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
149 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
150 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
151 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
152 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
153 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
154 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
155 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
156 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
157 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
158 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
159 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
160 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
161 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
162 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
163 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
164 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
165 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
166 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
167 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
168 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
169 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
170 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
171 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
172 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
173 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
174 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
175 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
176 2019-07-07T15:00:00+00:00 stage       Brussels     Brussels Closed
     classification distance distance_unit single_event
1   Team Time Trial     27,6            km        FALSE
2   Team Time Trial     27,6            km        FALSE
3   Team Time Trial     27,6            km        FALSE
4   Team Time Trial     27,6            km        FALSE
5   Team Time Trial     27,6            km        FALSE
6   Team Time Trial     27,6            km        FALSE
7   Team Time Trial     27,6            km        FALSE
8   Team Time Trial     27,6            km        FALSE
9   Team Time Trial     27,6            km        FALSE
10  Team Time Trial     27,6            km        FALSE
11  Team Time Trial     27,6            km        FALSE
12  Team Time Trial     27,6            km        FALSE
13  Team Time Trial     27,6            km        FALSE
14  Team Time Trial     27,6            km        FALSE
15  Team Time Trial     27,6            km        FALSE
16  Team Time Trial     27,6            km        FALSE
17  Team Time Trial     27,6            km        FALSE
18  Team Time Trial     27,6            km        FALSE
19  Team Time Trial     27,6            km        FALSE
20  Team Time Trial     27,6            km        FALSE
21  Team Time Trial     27,6            km        FALSE
22  Team Time Trial     27,6            km        FALSE
23  Team Time Trial     27,6            km        FALSE
24  Team Time Trial     27,6            km        FALSE
25  Team Time Trial     27,6            km        FALSE
26  Team Time Trial     27,6            km        FALSE
27  Team Time Trial     27,6            km        FALSE
28  Team Time Trial     27,6            km        FALSE
29  Team Time Trial     27,6            km        FALSE
30  Team Time Trial     27,6            km        FALSE
31  Team Time Trial     27,6            km        FALSE
32  Team Time Trial     27,6            km        FALSE
33  Team Time Trial     27,6            km        FALSE
34  Team Time Trial     27,6            km        FALSE
35  Team Time Trial     27,6            km        FALSE
36  Team Time Trial     27,6            km        FALSE
37  Team Time Trial     27,6            km        FALSE
38  Team Time Trial     27,6            km        FALSE
39  Team Time Trial     27,6            km        FALSE
40  Team Time Trial     27,6            km        FALSE
41  Team Time Trial     27,6            km        FALSE
42  Team Time Trial     27,6            km        FALSE
43  Team Time Trial     27,6            km        FALSE
44  Team Time Trial     27,6            km        FALSE
45  Team Time Trial     27,6            km        FALSE
46  Team Time Trial     27,6            km        FALSE
47  Team Time Trial     27,6            km        FALSE
48  Team Time Trial     27,6            km        FALSE
49  Team Time Trial     27,6            km        FALSE
50  Team Time Trial     27,6            km        FALSE
51  Team Time Trial     27,6            km        FALSE
52  Team Time Trial     27,6            km        FALSE
53  Team Time Trial     27,6            km        FALSE
54  Team Time Trial     27,6            km        FALSE
55  Team Time Trial     27,6            km        FALSE
56  Team Time Trial     27,6            km        FALSE
57  Team Time Trial     27,6            km        FALSE
58  Team Time Trial     27,6            km        FALSE
59  Team Time Trial     27,6            km        FALSE
60  Team Time Trial     27,6            km        FALSE
61  Team Time Trial     27,6            km        FALSE
62  Team Time Trial     27,6            km        FALSE
63  Team Time Trial     27,6            km        FALSE
64  Team Time Trial     27,6            km        FALSE
65  Team Time Trial     27,6            km        FALSE
66  Team Time Trial     27,6            km        FALSE
67  Team Time Trial     27,6            km        FALSE
68  Team Time Trial     27,6            km        FALSE
69  Team Time Trial     27,6            km        FALSE
70  Team Time Trial     27,6            km        FALSE
71  Team Time Trial     27,6            km        FALSE
72  Team Time Trial     27,6            km        FALSE
73  Team Time Trial     27,6            km        FALSE
74  Team Time Trial     27,6            km        FALSE
75  Team Time Trial     27,6            km        FALSE
76  Team Time Trial     27,6            km        FALSE
77  Team Time Trial     27,6            km        FALSE
78  Team Time Trial     27,6            km        FALSE
79  Team Time Trial     27,6            km        FALSE
80  Team Time Trial     27,6            km        FALSE
81  Team Time Trial     27,6            km        FALSE
82  Team Time Trial     27,6            km        FALSE
83  Team Time Trial     27,6            km        FALSE
84  Team Time Trial     27,6            km        FALSE
85  Team Time Trial     27,6            km        FALSE
86  Team Time Trial     27,6            km        FALSE
87  Team Time Trial     27,6            km        FALSE
88  Team Time Trial     27,6            km        FALSE
89  Team Time Trial     27,6            km        FALSE
90  Team Time Trial     27,6            km        FALSE
91  Team Time Trial     27,6            km        FALSE
92  Team Time Trial     27,6            km        FALSE
93  Team Time Trial     27,6            km        FALSE
94  Team Time Trial     27,6            km        FALSE
95  Team Time Trial     27,6            km        FALSE
96  Team Time Trial     27,6            km        FALSE
97  Team Time Trial     27,6            km        FALSE
98  Team Time Trial     27,6            km        FALSE
99  Team Time Trial     27,6            km        FALSE
100 Team Time Trial     27,6            km        FALSE
101 Team Time Trial     27,6            km        FALSE
102 Team Time Trial     27,6            km        FALSE
103 Team Time Trial     27,6            km        FALSE
104 Team Time Trial     27,6            km        FALSE
105 Team Time Trial     27,6            km        FALSE
106 Team Time Trial     27,6            km        FALSE
107 Team Time Trial     27,6            km        FALSE
108 Team Time Trial     27,6            km        FALSE
109 Team Time Trial     27,6            km        FALSE
110 Team Time Trial     27,6            km        FALSE
111 Team Time Trial     27,6            km        FALSE
112 Team Time Trial     27,6            km        FALSE
113 Team Time Trial     27,6            km        FALSE
114 Team Time Trial     27,6            km        FALSE
115 Team Time Trial     27,6            km        FALSE
116 Team Time Trial     27,6            km        FALSE
117 Team Time Trial     27,6            km        FALSE
118 Team Time Trial     27,6            km        FALSE
119 Team Time Trial     27,6            km        FALSE
120 Team Time Trial     27,6            km        FALSE
121 Team Time Trial     27,6            km        FALSE
122 Team Time Trial     27,6            km        FALSE
123 Team Time Trial     27,6            km        FALSE
124 Team Time Trial     27,6            km        FALSE
125 Team Time Trial     27,6            km        FALSE
126 Team Time Trial     27,6            km        FALSE
127 Team Time Trial     27,6            km        FALSE
128 Team Time Trial     27,6            km        FALSE
129 Team Time Trial     27,6            km        FALSE
130 Team Time Trial     27,6            km        FALSE
131 Team Time Trial     27,6            km        FALSE
132 Team Time Trial     27,6            km        FALSE
133 Team Time Trial     27,6            km        FALSE
134 Team Time Trial     27,6            km        FALSE
135 Team Time Trial     27,6            km        FALSE
136 Team Time Trial     27,6            km        FALSE
137 Team Time Trial     27,6            km        FALSE
138 Team Time Trial     27,6            km        FALSE
139 Team Time Trial     27,6            km        FALSE
140 Team Time Trial     27,6            km        FALSE
141 Team Time Trial     27,6            km        FALSE
142 Team Time Trial     27,6            km        FALSE
143 Team Time Trial     27,6            km        FALSE
144 Team Time Trial     27,6            km        FALSE
145 Team Time Trial     27,6            km        FALSE
146 Team Time Trial     27,6            km        FALSE
147 Team Time Trial     27,6            km        FALSE
148 Team Time Trial     27,6            km        FALSE
149 Team Time Trial     27,6            km        FALSE
150 Team Time Trial     27,6            km        FALSE
151 Team Time Trial     27,6            km        FALSE
152 Team Time Trial     27,6            km        FALSE
153 Team Time Trial     27,6            km        FALSE
154 Team Time Trial     27,6            km        FALSE
155 Team Time Trial     27,6            km        FALSE
156 Team Time Trial     27,6            km        FALSE
157 Team Time Trial     27,6            km        FALSE
158 Team Time Trial     27,6            km        FALSE
159 Team Time Trial     27,6            km        FALSE
160 Team Time Trial     27,6            km        FALSE
161 Team Time Trial     27,6            km        FALSE
162 Team Time Trial     27,6            km        FALSE
163 Team Time Trial     27,6            km        FALSE
164 Team Time Trial     27,6            km        FALSE
165 Team Time Trial     27,6            km        FALSE
166 Team Time Trial     27,6            km        FALSE
167 Team Time Trial     27,6            km        FALSE
168 Team Time Trial     27,6            km        FALSE
169 Team Time Trial     27,6            km        FALSE
170 Team Time Trial     27,6            km        FALSE
171 Team Time Trial     27,6            km        FALSE
172 Team Time Trial     27,6            km        FALSE
173 Team Time Trial     27,6            km        FALSE
174 Team Time Trial     27,6            km        FALSE
175 Team Time Trial     27,6            km        FALSE
176 Team Time Trial     27,6            km        FALSE
```

time - cyclist's time or relative time on a given stage (character)
time_rank - rank of cyclist as given in the stage (integer)
sprint_pts - sprint points earned by cyclist on given stage (double)
sprint_rank - rank of cyclist based on sprint points within stage (integer)
climb_pts - climb points earned by cyclist on given stage (double)
climb_rank - rank of cyclist based on climb points within stage (integer)
young_rider_time - young rider time on a given stage (character)
young_rider_rank - rank of cyclist based on young rider time within stage (integer)
