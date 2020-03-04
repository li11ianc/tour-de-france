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
View(tdf)
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
data <- merge(people, stage_info, by = "description", all = TRUE) 
data
```

```
    description                   id                                   name
1       Stage 2  sr:competitor:26658                    Valverde, Alejandro
2       Stage 2 sr:competitor:135930                             Haig, Jack
3       Stage 2 sr:competitor:123892                            Yates, Adam
4       Stage 2 sr:competitor:310616                         Scully, Thomas
5       Stage 2 sr:competitor:123378                         Zakarin, Ilnur
6       Stage 2 sr:competitor:135922                            Ewan, Caleb
7       Stage 2 sr:competitor:135938                         Mohoric, Matej
8       Stage 2 sr:competitor:135924                    Alaphilippe, Julian
9       Stage 2 sr:competitor:135926                            Zabel, Rick
10      Stage 2 sr:competitor:146106                        Stuyven, Jasper
11      Stage 2 sr:competitor:135946                       Bettiol, Alberto
12      Stage 2 sr:competitor:123886                 Kragh Andersen, Soeren
13      Stage 2 sr:competitor:146110                      van Baarle, Dylan
14      Stage 2 sr:competitor:147128                     Bonifazio, Niccolo
15      Stage 2 sr:competitor:198734                     Rossetto, Stephane
16      Stage 2 sr:competitor:208169                    Laporte, Christophe
17      Stage 2 sr:competitor:197808                          Benoot, Tiesj
18      Stage 2 sr:competitor:171236                       de Buyst, Jasper
19      Stage 2 sr:competitor:196712                           Teuns, Dylan
20      Stage 2 sr:competitor:174908                         Woods, Michael
21      Stage 2 sr:competitor:123888                           Yates, Simon
22      Stage 2 sr:competitor:123880              Valgren Andersen, Michael
23      Stage 2 sr:competitor:199422                           Kung, Stefan
24      Stage 2  sr:competitor:92871             Verona Quintanilla, Carlos
25      Stage 2  sr:competitor:78671                           Molard, Rudy
26      Stage 2  sr:competitor:80287                           Wellens, Tim
27      Stage 2  sr:competitor:80289                            Houle, Hugo
28      Stage 2  sr:competitor:81383          Janse van Rensburg, Reinhardt
29      Stage 2  sr:competitor:88952                       Gougeard, Alexis
30      Stage 2  sr:competitor:82007                             Aru, Fabio
31      Stage 2  sr:competitor:91766                        Barguil, Warren
32      Stage 2  sr:competitor:91768                     Vuillermoz, Alexis
33      Stage 2  sr:competitor:93161                         Lampaert, Yves
34      Stage 2 sr:competitor:123874                   Nielsen, Magnus Cort
35      Stage 2  sr:competitor:93179                          Arndt, Nikias
36      Stage 2  sr:competitor:93813                       Lutsenko, Alexey
37      Stage 2  sr:competitor:93811                 Fraile Matarranz, Omar
38      Stage 2  sr:competitor:94613                   Perichon, Pierre-Luc
39      Stage 2  sr:competitor:95635                 Reichenbach, Sebastien
40      Stage 2 sr:competitor:146340                             Haga, Chad
41      Stage 2 sr:competitor:101459                       Berhane, Natnael
42      Stage 2 sr:competitor:123856                    Bystroem, Sven Erik
43      Stage 2 sr:competitor:318361                 Schachmann, Maximilian
44      Stage 2 sr:competitor:226716                          Skujins, Toms
45      Stage 2  sr:competitor:67014                         Bardet, Romain
46      Stage 2 sr:competitor:310574                     Mas Nicolau, Enric
47      Stage 2 sr:competitor:249457                           Politt, Nils
48      Stage 2 sr:competitor:246981                      Calmejane, Lilian
49      Stage 2 sr:competitor:248863                        Bernard, Julien
50      Stage 2 sr:competitor:254335                      Martin, Guillaume
51      Stage 2 sr:competitor:313921                           Bernal, Egan
52      Stage 2 sr:competitor:282491                       Grellier, Fabien
53      Stage 2 sr:competitor:286739                         de Gendt, Aime
54      Stage 2 sr:competitor:313919                   Garcia Cortina, Ivan
55      Stage 2 sr:competitor:319169                Jansen Groendahl, Amund
56      Stage 2 sr:competitor:226972 Richeze Araquistain, Ariel Maximiliano
57      Stage 2 sr:competitor:317941                         Kamna, Lennard
58      Stage 2 sr:competitor:323145                           Gaudu, David
59      Stage 2 sr:competitor:325989                         Perez, Anthony
60      Stage 2 sr:competitor:329997                          Gesbert, Elie
61      Stage 2 sr:competitor:330003                         Ourselin, Paul
62      Stage 2 sr:competitor:353504                         Van Aert, Wout
63      Stage 2 sr:competitor:379864                      Cosnefroy, Benoit
64      Stage 2 sr:competitor:379848                      Philipsen, Jasper
65      Stage 2 sr:competitor:241178                         Bevin, Patrick
66      Stage 2 sr:competitor:248853                       de Plus, Laurens
67      Stage 2 sr:competitor:198722                        Teunissen, Mike
68      Stage 2 sr:competitor:198994                        Turgis, Anthony
69      Stage 2 sr:competitor:196754                        Ledanois, Kevin
70      Stage 2 sr:competitor:254977                     Wisniowski, Lukasz
71      Stage 2 sr:competitor:194902                        Konrad, Patrick
72      Stage 2 sr:competitor:219922                     Groenewegen, Dylan
73      Stage 2 sr:competitor:197934                        Naesen, Olivier
74      Stage 2 sr:competitor:196762                    Soler Gimenez, Marc
75      Stage 2 sr:competitor:196774                      Backaert, Fredrik
76      Stage 2 sr:competitor:198720                         Rosskopf, Joey
77      Stage 2 sr:competitor:250457                         Moscon, Gianni
78      Stage 2 sr:competitor:323211                       Meurisse, Xandro
79      Stage 2 sr:competitor:201073                      Buchmann, Emanuel
80      Stage 2 sr:competitor:226826                     Postlberger, Lukas
81      Stage 2 sr:competitor:252831                        Ciccone, Giulio
82      Stage 2 sr:competitor:246979                  Eiking, Odd Christian
83      Stage 2 sr:competitor:247361                     Muhlberger, Gregor
84      Stage 2 sr:competitor:318333                    Wurtz Schmidt, Mads
85      Stage 2 sr:competitor:318335                        Asgreen, Kasper
86      Stage 2 sr:competitor:221492                        Goncalves, Jose
87      Stage 2  sr:competitor:69216                        Bennett, George
88      Stage 2  sr:competitor:66830                  Laengen, Vegard Stake
89      Stage 2  sr:competitor:26697                 Sanchez Gil, Luis Leon
90      Stage 2  sr:competitor:27911                          Roux, Anthony
91      Stage 2  sr:competitor:27768                        Thomas, Geraint
92      Stage 2  sr:competitor:27770                        Fuglsang, Jakob
93      Stage 2  sr:competitor:27851                           Impey, Daryl
94      Stage 2  sr:competitor:27883                         Kangert, Tanel
95      Stage 2  sr:competitor:27884                  Hagen, Edvald Boasson
96      Stage 2  sr:competitor:27886                           Martin, Tony
97      Stage 2  sr:competitor:27895                         Mollema, Bauke
98      Stage 2  sr:competitor:27907                         Frank, Mathias
99      Stage 2  sr:competitor:27913                         Offredo, Yoann
100     Stage 2  sr:competitor:27667                          Clarke, Simon
101     Stage 2  sr:competitor:27916                         Taaramae, Rein
102     Stage 2  sr:competitor:27922                          Simon, Julien
103     Stage 2  sr:competitor:27926                          Porte, Richie
104     Stage 2  sr:competitor:27968                          Bouet, Maxime
105     Stage 2  sr:competitor:27970                         Martin, Daniel
106     Stage 2  sr:competitor:41621                           Kluge, Roger
107     Stage 2  sr:competitor:34530            Faria Da Costa, Rui Alberto
108     Stage 2  sr:competitor:44301                         Gallopin, Tony
109     Stage 2  sr:competitor:27762                         Cherel, Mikael
110     Stage 2  sr:competitor:27654                         Terpstra, Niki
111     Stage 2  sr:competitor:34405                         Amador, Andrey
112     Stage 2  sr:competitor:27072                      Burghardt, Marcus
113     Stage 2  sr:competitor:26766                       Bak, Lars Ytting
114     Stage 2  sr:competitor:26792                       Nibali, Vincenzo
115     Stage 2  sr:competitor:26822                          De Kort, Koen
116     Stage 2  sr:competitor:26862                        Monfort, Maxime
117     Stage 2  sr:competitor:26921                         Roche, Nicolas
118     Stage 2  sr:competitor:26931                         Erviti, Imanol
119     Stage 2  sr:competitor:26973                         Greipel, Andre
120     Stage 2  sr:competitor:27050                         Moinard, Amael
121     Stage 2  sr:competitor:27183                       Cummings, Steven
122     Stage 2  sr:competitor:27623                     Van Avermaet, Greg
123     Stage 2  sr:competitor:27345                        Uran, Rigoberto
124     Stage 2  sr:competitor:27397                        Bonnet, William
125     Stage 2  sr:competitor:27407                   Langeveld, Sebastian
126     Stage 2  sr:competitor:27412                         Pauwels, Serge
127     Stage 2  sr:competitor:27446                       Kreuziger, Roman
128     Stage 2  sr:competitor:27499                        Schaer, Michael
129     Stage 2  sr:competitor:27603                    Ladagnous, Matthieu
130     Stage 2  sr:competitor:27620                        Devenyns, Dries
131     Stage 2  sr:competitor:35498                    Van Garderen, Tejay
132     Stage 2  sr:competitor:34406                            Oss, Daniel
133     Stage 2  sr:competitor:68002                          Haller, Marco
134     Stage 2  sr:competitor:50026                       Nizzolo, Giacomo
135     Stage 2  sr:competitor:67711             Henao Montoya, Sergio Luis
136     Stage 2  sr:competitor:47984                        Durbridge, Luke
137     Stage 2  sr:competitor:47989                       Hepburn, Michael
138     Stage 2  sr:competitor:49209                         King, Benjamin
139     Stage 2  sr:competitor:49569                        Vachon, Florian
140     Stage 2  sr:competitor:49953                  de Marchi, Alessandro
141     Stage 2  sr:competitor:49955                      Pasqualon, Andrea
142     Stage 2  sr:competitor:50044                        Quintana, Nairo
143     Stage 2  sr:competitor:50032                          Edet, Nicolas
144     Stage 2  sr:competitor:50287                     Landa Meana, Mikel
145     Stage 2  sr:competitor:50048                           Tratnik, Jan
146     Stage 2  sr:competitor:50313                      van Melsen, Kevin
147     Stage 2  sr:competitor:50588                      Debusschere, Jens
148     Stage 2  sr:competitor:50710                   Herrada Lopez, Jesus
149     Stage 2  sr:competitor:51780                          Bilbao, Pello
150     Stage 2  sr:competitor:55679               Juul-Jensen, Christopher
151     Stage 2  sr:competitor:54471                        Trentin, Matteo
152     Stage 2  sr:competitor:62830                       Kelderman, Wilco
153     Stage 2  sr:competitor:50288                    Kwiatkowski, Michal
154     Stage 2  sr:competitor:50285                             Rowe, Luke
155     Stage 2  sr:competitor:49690                        Caruso, Damiano
156     Stage 2  sr:competitor:39813                         Sicard, Romain
157     Stage 2  sr:competitor:41433                    Kristoff, Alexander
158     Stage 2  sr:competitor:35401                       De Gendt, Thomas
159     Stage 2  sr:competitor:44092                          Viviani, Elia
160     Stage 2  sr:competitor:35470               Izagirre Insausti, Gorka
161     Stage 2  sr:competitor:35557                         Geschke, Simon
162     Stage 2  sr:competitor:35558                          Poels, Wouter
163     Stage 2  sr:competitor:36863                      Moerkoev, Michael
164     Stage 2  sr:competitor:50262  Santos Simoes Oliveira, Nelson Filipe
165     Stage 2  sr:competitor:39816                         Pinot, Thibaut
166     Stage 2  sr:competitor:50283                       Colbrelli, Sonny
167     Stage 2  sr:competitor:39819          Castroviejo, Nicolas Jonathan
168     Stage 2  sr:competitor:39823                           Sagan, Peter
169     Stage 2  sr:competitor:39828                      Matthews, Michael
170     Stage 2  sr:competitor:39829                          Dennis, Rohan
171     Stage 2  sr:competitor:41623                       Keukeleire, Jens
172     Stage 2  sr:competitor:41444                         Felline, Fabio
173     Stage 2  sr:competitor:41446                     Kruijswijk, Steven
174     Stage 2  sr:competitor:42654                     Delaplace, Anthony
175     Stage 2  sr:competitor:50281                          Dowsett, Alex
176     Stage 2 sr:competitor:532557                              Bol, Cees
    gender    nationality country_code              team.id
1     male          Spain          ESP  sr:competitor:26600
2     male      Australia          AUS  sr:competitor:62812
3     male  Great Britain          GBR  sr:competitor:62812
4     male    New Zealand          NZL  sr:competitor:27747
5     male         Russia          RUS  sr:competitor:33029
6     male      Australia          AUS  sr:competitor:27616
7     male       Slovenia          SVN  sr:competitor:26395
8     male         France          FRA  sr:competitor:26520
9     male        Germany          DEU  sr:competitor:33029
10    male        Belgium          BEL  sr:competitor:62896
11    male          Italy          ITA  sr:competitor:27747
12    male        Denmark          DNK sr:competitor:310638
13    male    Netherlands          NLD  sr:competitor:39815
14    male          Italy          ITA sr:competitor:246991
15    male         France          FRA  sr:competitor:26495
16    male         France          FRA  sr:competitor:26495
17    male        Belgium          BEL  sr:competitor:27616
18    male        Belgium          BEL  sr:competitor:27616
19    male        Belgium          BEL  sr:competitor:26395
20    male         Canada          CAN  sr:competitor:27747
21    male  Great Britain          GBR  sr:competitor:62812
22    male        Denmark          DNK  sr:competitor:80955
23    male    Switzerland          CHE  sr:competitor:26516
24    male          Spain          ESP  sr:competitor:26600
25    male         France          FRA  sr:competitor:26516
26    male        Belgium          BEL  sr:competitor:27616
27    male         Canada          CAN  sr:competitor:26598
28    male   South Africa          ZAF  sr:competitor:80955
29    male         France          FRA  sr:competitor:26519
30    male          Italy          ITA sr:competitor:310636
31    male         France          FRA sr:competitor:246989
32    male         France          FRA  sr:competitor:26519
33    male        Belgium          BEL  sr:competitor:26520
34    male        Denmark          DNK  sr:competitor:26598
35    male        Germany          DEU sr:competitor:310638
36    male     Kazakhstan          KAZ  sr:competitor:26598
37    male          Spain          ESP  sr:competitor:26598
38    male         France          FRA  sr:competitor:26495
39    male    Switzerland          CHE  sr:competitor:26516
40    male            USA          USA sr:competitor:310638
41    male        Eritrea          ERI  sr:competitor:26495
42    male         Norway          NOR sr:competitor:310636
43    male        Germany          DEU  sr:competitor:50271
44    male         Latvia          LVA  sr:competitor:62896
45    male         France          FRA  sr:competitor:26519
46    male          Spain          ESP  sr:competitor:26520
47    male        Germany          DEU  sr:competitor:33029
48    male         France          FRA sr:competitor:246991
49    male         France          FRA  sr:competitor:62896
50    male         France          FRA  sr:competitor:49122
51    male       Colombia          COL  sr:competitor:39815
52    male         France          FRA sr:competitor:246991
53    male        Belgium          BEL  sr:competitor:49122
54    male          Spain          ESP  sr:competitor:26395
55    male         Norway          NOR sr:competitor:189354
56    male      Argentina          ARG  sr:competitor:26520
57    male        Germany          DEU sr:competitor:310638
58    male         France          FRA  sr:competitor:26516
59    male         France          FRA  sr:competitor:26495
60    male         France          FRA sr:competitor:246989
61    male         France          FRA sr:competitor:246991
62    male        Belgium          BEL sr:competitor:189354
63    male         France          FRA  sr:competitor:26519
64    male        Belgium          BEL sr:competitor:310636
65    male    New Zealand          NZL  sr:competitor:27981
66    male        Belgium          BEL sr:competitor:189354
67    male    Netherlands          NLD sr:competitor:189354
68    male         France          FRA sr:competitor:246991
69    male         France          FRA sr:competitor:246989
70    male         Poland          POL  sr:competitor:27981
71    male        Austria          AUT  sr:competitor:50271
72    male    Netherlands          NLD sr:competitor:189354
73    male        Belgium          BEL  sr:competitor:26519
74    male          Spain          ESP  sr:competitor:26600
75    male        Belgium          BEL  sr:competitor:49122
76    male            USA          USA  sr:competitor:27981
77    male          Italy          ITA  sr:competitor:39815
78    male        Belgium          BEL  sr:competitor:49122
79    male        Germany          DEU  sr:competitor:50271
80    male        Austria          AUT  sr:competitor:50271
81    male          Italy          ITA  sr:competitor:62896
82    male         Norway          NOR  sr:competitor:49122
83    male        Austria          AUT  sr:competitor:50271
84    male        Denmark          DNK  sr:competitor:33029
85    male        Denmark          DNK  sr:competitor:26520
86    male       Portugal          PRT  sr:competitor:33029
87    male    New Zealand          NZL sr:competitor:189354
88    male         Norway          NOR sr:competitor:310636
89    male          Spain          ESP  sr:competitor:26598
90    male         France          FRA  sr:competitor:26516
91    male  Great Britain          GBR  sr:competitor:39815
92    male        Denmark          DNK  sr:competitor:26598
93    male   South Africa          ZAF  sr:competitor:62812
94    male        Estonia          EST  sr:competitor:27747
95    male         Norway          NOR  sr:competitor:80955
96    male        Germany          DEU sr:competitor:189354
97    male    Netherlands          NLD  sr:competitor:62896
98    male    Switzerland          CHE  sr:competitor:26519
99    male         France          FRA  sr:competitor:49122
100   male      Australia          AUS  sr:competitor:27747
101   male        Estonia          EST sr:competitor:246991
102   male         France          FRA  sr:competitor:26495
103   male      Australia          AUS  sr:competitor:62896
104   male         France          FRA sr:competitor:246989
105   male        Ireland          IRL sr:competitor:310636
106   male        Germany          DEU  sr:competitor:27616
107   male       Portugal          PRT sr:competitor:310636
108   male         France          FRA  sr:competitor:26519
109   male         France          FRA  sr:competitor:26519
110   male    Netherlands          NLD sr:competitor:246991
111   male     Costa Rica          CRI  sr:competitor:26600
112   male        Germany          DEU  sr:competitor:50271
113   male        Denmark          DNK  sr:competitor:80955
114   male          Italy          ITA  sr:competitor:26395
115   male    Netherlands          NLD  sr:competitor:62896
116   male         France          FRA  sr:competitor:27616
117   male        Ireland          IRL sr:competitor:310638
118   male          Spain          ESP  sr:competitor:26600
119   male        Germany          DEU sr:competitor:246989
120   male         France          FRA sr:competitor:246989
121   male  Great Britain          GBR  sr:competitor:80955
122   male        Belgium          BEL  sr:competitor:27981
123   male       Colombia          COL  sr:competitor:27747
124   male         France          FRA  sr:competitor:26516
125   male    Netherlands          NLD  sr:competitor:27747
126   male        Belgium          BEL  sr:competitor:27981
127   male Czech Republic          CZE  sr:competitor:80955
128   male    Switzerland          CHE  sr:competitor:27981
129   male         France          FRA  sr:competitor:26516
130   male        Belgium          BEL  sr:competitor:26520
131   male            USA          USA  sr:competitor:27747
132   male          Italy          ITA  sr:competitor:50271
133   male        Austria          AUT  sr:competitor:33029
134   male          Italy          ITA  sr:competitor:80955
135   male       Colombia          COL sr:competitor:310636
136   male      Australia          AUS  sr:competitor:62812
137   male      Australia          AUS  sr:competitor:62812
138   male            USA          USA  sr:competitor:80955
139   male         France          FRA sr:competitor:246989
140   male          Italy          ITA  sr:competitor:27981
141   male          Italy          ITA  sr:competitor:49122
142   male       Colombia          COL  sr:competitor:26600
143   male         France          FRA  sr:competitor:26495
144   male          Spain          ESP  sr:competitor:26600
145   male       Slovenia          SVN  sr:competitor:26395
146   male        Belgium          BEL  sr:competitor:49122
147   male        Belgium          BEL  sr:competitor:33029
148   male          Spain          ESP  sr:competitor:26495
149   male          Spain          ESP  sr:competitor:26598
150   male        Denmark          DNK  sr:competitor:62812
151   male          Italy          ITA  sr:competitor:62812
152   male    Netherlands          NLD sr:competitor:310638
153   male         Poland          POL  sr:competitor:39815
154   male  Great Britain          GBR  sr:competitor:39815
155   male          Italy          ITA  sr:competitor:26395
156   male         France          FRA sr:competitor:246991
157   male         Norway          NOR sr:competitor:310636
158   male        Belgium          BEL  sr:competitor:27616
159   male          Italy          ITA  sr:competitor:26520
160   male          Spain          ESP  sr:competitor:26598
161   male        Germany          DEU  sr:competitor:27981
162   male    Netherlands          NLD  sr:competitor:39815
163   male        Denmark          DNK  sr:competitor:26520
164   male       Portugal          PRT  sr:competitor:26600
165   male         France          FRA  sr:competitor:26516
166   male          Italy          ITA  sr:competitor:26395
167   male          Spain          ESP  sr:competitor:39815
168   male       Slovakia          SVK  sr:competitor:50271
169   male      Australia          AUS sr:competitor:310638
170   male      Australia          AUS  sr:competitor:26395
171   male        Belgium          BEL  sr:competitor:27616
172   male          Italy          ITA  sr:competitor:62896
173   male    Netherlands          NLD sr:competitor:189354
174   male         France          FRA sr:competitor:246989
175   male  Great Britain          GBR  sr:competitor:33029
176   male    Netherlands          NLD sr:competitor:310638
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
    team.country_code                 scheduled             scheduled_end  type
1                 ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
2                 AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
3                 AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
4                 USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
5                 CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
6                 BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
7                 BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
8                 BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
9                 CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
10                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
11                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
12                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
13                GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
14                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
15                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
16                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
17                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
18                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
19                BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
20                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
21                AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
22                ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
23                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
24                ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
25                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
26                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
27                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
28                ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
29                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
30                ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
31                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
32                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
33                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
34                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
35                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
36                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
37                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
38                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
39                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
40                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
41                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
42                ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
43                DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
44                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
45                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
46                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
47                CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
48                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
49                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
50                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
51                GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
52                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
53                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
54                BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
55                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
56                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
57                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
58                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
59                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
60                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
61                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
62                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
63                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
64                ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
65                POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
66                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
67                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
68                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
69                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
70                POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
71                DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
72                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
73                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
74                ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
75                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
76                POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
77                GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
78                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
79                DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
80                DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
81                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
82                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
83                DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
84                CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
85                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
86                CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
87                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
88                ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
89                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
90                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
91                GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
92                KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
93                AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
94                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
95                ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
96                NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
97                USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
98                FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
99                BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
100               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
101               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
102               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
103               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
104               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
105               ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
106               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
107               ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
108               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
109               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
110               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
111               ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
112               DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
113               ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
114               BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
115               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
116               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
117               NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
118               ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
119               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
120               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
121               ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
122               POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
123               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
124               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
125               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
126               POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
127               ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
128               POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
129               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
130               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
131               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
132               DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
133               CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
134               ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
135               ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
136               AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
137               AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
138               ZAF 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
139               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
140               POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
141               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
142               ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
143               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
144               ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
145               BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
146               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
147               CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
148               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
149               KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
150               AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
151               AUS 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
152               NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
153               GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
154               GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
155               BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
156               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
157               ARE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
158               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
159               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
160               KAZ 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
161               POL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
162               GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
163               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
164               ESP 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
165               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
166               BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
167               GBR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
168               DEU 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
169               NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
170               BHR 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
171               BEL 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
172               USA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
173               NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
174               FRA 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
175               CHE 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
176               NLD 2019-07-07T12:30:00+00:00 2019-07-07T15:00:00+00:00 stage
    departure_city arrival_city status  classification distance distance_unit
1         Brussels     Brussels Closed Team Time Trial     27,6            km
2         Brussels     Brussels Closed Team Time Trial     27,6            km
3         Brussels     Brussels Closed Team Time Trial     27,6            km
4         Brussels     Brussels Closed Team Time Trial     27,6            km
5         Brussels     Brussels Closed Team Time Trial     27,6            km
6         Brussels     Brussels Closed Team Time Trial     27,6            km
7         Brussels     Brussels Closed Team Time Trial     27,6            km
8         Brussels     Brussels Closed Team Time Trial     27,6            km
9         Brussels     Brussels Closed Team Time Trial     27,6            km
10        Brussels     Brussels Closed Team Time Trial     27,6            km
11        Brussels     Brussels Closed Team Time Trial     27,6            km
12        Brussels     Brussels Closed Team Time Trial     27,6            km
13        Brussels     Brussels Closed Team Time Trial     27,6            km
14        Brussels     Brussels Closed Team Time Trial     27,6            km
15        Brussels     Brussels Closed Team Time Trial     27,6            km
16        Brussels     Brussels Closed Team Time Trial     27,6            km
17        Brussels     Brussels Closed Team Time Trial     27,6            km
18        Brussels     Brussels Closed Team Time Trial     27,6            km
19        Brussels     Brussels Closed Team Time Trial     27,6            km
20        Brussels     Brussels Closed Team Time Trial     27,6            km
21        Brussels     Brussels Closed Team Time Trial     27,6            km
22        Brussels     Brussels Closed Team Time Trial     27,6            km
23        Brussels     Brussels Closed Team Time Trial     27,6            km
24        Brussels     Brussels Closed Team Time Trial     27,6            km
25        Brussels     Brussels Closed Team Time Trial     27,6            km
26        Brussels     Brussels Closed Team Time Trial     27,6            km
27        Brussels     Brussels Closed Team Time Trial     27,6            km
28        Brussels     Brussels Closed Team Time Trial     27,6            km
29        Brussels     Brussels Closed Team Time Trial     27,6            km
30        Brussels     Brussels Closed Team Time Trial     27,6            km
31        Brussels     Brussels Closed Team Time Trial     27,6            km
32        Brussels     Brussels Closed Team Time Trial     27,6            km
33        Brussels     Brussels Closed Team Time Trial     27,6            km
34        Brussels     Brussels Closed Team Time Trial     27,6            km
35        Brussels     Brussels Closed Team Time Trial     27,6            km
36        Brussels     Brussels Closed Team Time Trial     27,6            km
37        Brussels     Brussels Closed Team Time Trial     27,6            km
38        Brussels     Brussels Closed Team Time Trial     27,6            km
39        Brussels     Brussels Closed Team Time Trial     27,6            km
40        Brussels     Brussels Closed Team Time Trial     27,6            km
41        Brussels     Brussels Closed Team Time Trial     27,6            km
42        Brussels     Brussels Closed Team Time Trial     27,6            km
43        Brussels     Brussels Closed Team Time Trial     27,6            km
44        Brussels     Brussels Closed Team Time Trial     27,6            km
45        Brussels     Brussels Closed Team Time Trial     27,6            km
46        Brussels     Brussels Closed Team Time Trial     27,6            km
47        Brussels     Brussels Closed Team Time Trial     27,6            km
48        Brussels     Brussels Closed Team Time Trial     27,6            km
49        Brussels     Brussels Closed Team Time Trial     27,6            km
50        Brussels     Brussels Closed Team Time Trial     27,6            km
51        Brussels     Brussels Closed Team Time Trial     27,6            km
52        Brussels     Brussels Closed Team Time Trial     27,6            km
53        Brussels     Brussels Closed Team Time Trial     27,6            km
54        Brussels     Brussels Closed Team Time Trial     27,6            km
55        Brussels     Brussels Closed Team Time Trial     27,6            km
56        Brussels     Brussels Closed Team Time Trial     27,6            km
57        Brussels     Brussels Closed Team Time Trial     27,6            km
58        Brussels     Brussels Closed Team Time Trial     27,6            km
59        Brussels     Brussels Closed Team Time Trial     27,6            km
60        Brussels     Brussels Closed Team Time Trial     27,6            km
61        Brussels     Brussels Closed Team Time Trial     27,6            km
62        Brussels     Brussels Closed Team Time Trial     27,6            km
63        Brussels     Brussels Closed Team Time Trial     27,6            km
64        Brussels     Brussels Closed Team Time Trial     27,6            km
65        Brussels     Brussels Closed Team Time Trial     27,6            km
66        Brussels     Brussels Closed Team Time Trial     27,6            km
67        Brussels     Brussels Closed Team Time Trial     27,6            km
68        Brussels     Brussels Closed Team Time Trial     27,6            km
69        Brussels     Brussels Closed Team Time Trial     27,6            km
70        Brussels     Brussels Closed Team Time Trial     27,6            km
71        Brussels     Brussels Closed Team Time Trial     27,6            km
72        Brussels     Brussels Closed Team Time Trial     27,6            km
73        Brussels     Brussels Closed Team Time Trial     27,6            km
74        Brussels     Brussels Closed Team Time Trial     27,6            km
75        Brussels     Brussels Closed Team Time Trial     27,6            km
76        Brussels     Brussels Closed Team Time Trial     27,6            km
77        Brussels     Brussels Closed Team Time Trial     27,6            km
78        Brussels     Brussels Closed Team Time Trial     27,6            km
79        Brussels     Brussels Closed Team Time Trial     27,6            km
80        Brussels     Brussels Closed Team Time Trial     27,6            km
81        Brussels     Brussels Closed Team Time Trial     27,6            km
82        Brussels     Brussels Closed Team Time Trial     27,6            km
83        Brussels     Brussels Closed Team Time Trial     27,6            km
84        Brussels     Brussels Closed Team Time Trial     27,6            km
85        Brussels     Brussels Closed Team Time Trial     27,6            km
86        Brussels     Brussels Closed Team Time Trial     27,6            km
87        Brussels     Brussels Closed Team Time Trial     27,6            km
88        Brussels     Brussels Closed Team Time Trial     27,6            km
89        Brussels     Brussels Closed Team Time Trial     27,6            km
90        Brussels     Brussels Closed Team Time Trial     27,6            km
91        Brussels     Brussels Closed Team Time Trial     27,6            km
92        Brussels     Brussels Closed Team Time Trial     27,6            km
93        Brussels     Brussels Closed Team Time Trial     27,6            km
94        Brussels     Brussels Closed Team Time Trial     27,6            km
95        Brussels     Brussels Closed Team Time Trial     27,6            km
96        Brussels     Brussels Closed Team Time Trial     27,6            km
97        Brussels     Brussels Closed Team Time Trial     27,6            km
98        Brussels     Brussels Closed Team Time Trial     27,6            km
99        Brussels     Brussels Closed Team Time Trial     27,6            km
100       Brussels     Brussels Closed Team Time Trial     27,6            km
101       Brussels     Brussels Closed Team Time Trial     27,6            km
102       Brussels     Brussels Closed Team Time Trial     27,6            km
103       Brussels     Brussels Closed Team Time Trial     27,6            km
104       Brussels     Brussels Closed Team Time Trial     27,6            km
105       Brussels     Brussels Closed Team Time Trial     27,6            km
106       Brussels     Brussels Closed Team Time Trial     27,6            km
107       Brussels     Brussels Closed Team Time Trial     27,6            km
108       Brussels     Brussels Closed Team Time Trial     27,6            km
109       Brussels     Brussels Closed Team Time Trial     27,6            km
110       Brussels     Brussels Closed Team Time Trial     27,6            km
111       Brussels     Brussels Closed Team Time Trial     27,6            km
112       Brussels     Brussels Closed Team Time Trial     27,6            km
113       Brussels     Brussels Closed Team Time Trial     27,6            km
114       Brussels     Brussels Closed Team Time Trial     27,6            km
115       Brussels     Brussels Closed Team Time Trial     27,6            km
116       Brussels     Brussels Closed Team Time Trial     27,6            km
117       Brussels     Brussels Closed Team Time Trial     27,6            km
118       Brussels     Brussels Closed Team Time Trial     27,6            km
119       Brussels     Brussels Closed Team Time Trial     27,6            km
120       Brussels     Brussels Closed Team Time Trial     27,6            km
121       Brussels     Brussels Closed Team Time Trial     27,6            km
122       Brussels     Brussels Closed Team Time Trial     27,6            km
123       Brussels     Brussels Closed Team Time Trial     27,6            km
124       Brussels     Brussels Closed Team Time Trial     27,6            km
125       Brussels     Brussels Closed Team Time Trial     27,6            km
126       Brussels     Brussels Closed Team Time Trial     27,6            km
127       Brussels     Brussels Closed Team Time Trial     27,6            km
128       Brussels     Brussels Closed Team Time Trial     27,6            km
129       Brussels     Brussels Closed Team Time Trial     27,6            km
130       Brussels     Brussels Closed Team Time Trial     27,6            km
131       Brussels     Brussels Closed Team Time Trial     27,6            km
132       Brussels     Brussels Closed Team Time Trial     27,6            km
133       Brussels     Brussels Closed Team Time Trial     27,6            km
134       Brussels     Brussels Closed Team Time Trial     27,6            km
135       Brussels     Brussels Closed Team Time Trial     27,6            km
136       Brussels     Brussels Closed Team Time Trial     27,6            km
137       Brussels     Brussels Closed Team Time Trial     27,6            km
138       Brussels     Brussels Closed Team Time Trial     27,6            km
139       Brussels     Brussels Closed Team Time Trial     27,6            km
140       Brussels     Brussels Closed Team Time Trial     27,6            km
141       Brussels     Brussels Closed Team Time Trial     27,6            km
142       Brussels     Brussels Closed Team Time Trial     27,6            km
143       Brussels     Brussels Closed Team Time Trial     27,6            km
144       Brussels     Brussels Closed Team Time Trial     27,6            km
145       Brussels     Brussels Closed Team Time Trial     27,6            km
146       Brussels     Brussels Closed Team Time Trial     27,6            km
147       Brussels     Brussels Closed Team Time Trial     27,6            km
148       Brussels     Brussels Closed Team Time Trial     27,6            km
149       Brussels     Brussels Closed Team Time Trial     27,6            km
150       Brussels     Brussels Closed Team Time Trial     27,6            km
151       Brussels     Brussels Closed Team Time Trial     27,6            km
152       Brussels     Brussels Closed Team Time Trial     27,6            km
153       Brussels     Brussels Closed Team Time Trial     27,6            km
154       Brussels     Brussels Closed Team Time Trial     27,6            km
155       Brussels     Brussels Closed Team Time Trial     27,6            km
156       Brussels     Brussels Closed Team Time Trial     27,6            km
157       Brussels     Brussels Closed Team Time Trial     27,6            km
158       Brussels     Brussels Closed Team Time Trial     27,6            km
159       Brussels     Brussels Closed Team Time Trial     27,6            km
160       Brussels     Brussels Closed Team Time Trial     27,6            km
161       Brussels     Brussels Closed Team Time Trial     27,6            km
162       Brussels     Brussels Closed Team Time Trial     27,6            km
163       Brussels     Brussels Closed Team Time Trial     27,6            km
164       Brussels     Brussels Closed Team Time Trial     27,6            km
165       Brussels     Brussels Closed Team Time Trial     27,6            km
166       Brussels     Brussels Closed Team Time Trial     27,6            km
167       Brussels     Brussels Closed Team Time Trial     27,6            km
168       Brussels     Brussels Closed Team Time Trial     27,6            km
169       Brussels     Brussels Closed Team Time Trial     27,6            km
170       Brussels     Brussels Closed Team Time Trial     27,6            km
171       Brussels     Brussels Closed Team Time Trial     27,6            km
172       Brussels     Brussels Closed Team Time Trial     27,6            km
173       Brussels     Brussels Closed Team Time Trial     27,6            km
174       Brussels     Brussels Closed Team Time Trial     27,6            km
175       Brussels     Brussels Closed Team Time Trial     27,6            km
176       Brussels     Brussels Closed Team Time Trial     27,6            km
    single_event
1          FALSE
2          FALSE
3          FALSE
4          FALSE
5          FALSE
6          FALSE
7          FALSE
8          FALSE
9          FALSE
10         FALSE
11         FALSE
12         FALSE
13         FALSE
14         FALSE
15         FALSE
16         FALSE
17         FALSE
18         FALSE
19         FALSE
20         FALSE
21         FALSE
22         FALSE
23         FALSE
24         FALSE
25         FALSE
26         FALSE
27         FALSE
28         FALSE
29         FALSE
30         FALSE
31         FALSE
32         FALSE
33         FALSE
34         FALSE
35         FALSE
36         FALSE
37         FALSE
38         FALSE
39         FALSE
40         FALSE
41         FALSE
42         FALSE
43         FALSE
44         FALSE
45         FALSE
46         FALSE
47         FALSE
48         FALSE
49         FALSE
50         FALSE
51         FALSE
52         FALSE
53         FALSE
54         FALSE
55         FALSE
56         FALSE
57         FALSE
58         FALSE
59         FALSE
60         FALSE
61         FALSE
62         FALSE
63         FALSE
64         FALSE
65         FALSE
66         FALSE
67         FALSE
68         FALSE
69         FALSE
70         FALSE
71         FALSE
72         FALSE
73         FALSE
74         FALSE
75         FALSE
76         FALSE
77         FALSE
78         FALSE
79         FALSE
80         FALSE
81         FALSE
82         FALSE
83         FALSE
84         FALSE
85         FALSE
86         FALSE
87         FALSE
88         FALSE
89         FALSE
90         FALSE
91         FALSE
92         FALSE
93         FALSE
94         FALSE
95         FALSE
96         FALSE
97         FALSE
98         FALSE
99         FALSE
100        FALSE
101        FALSE
102        FALSE
103        FALSE
104        FALSE
105        FALSE
106        FALSE
107        FALSE
108        FALSE
109        FALSE
110        FALSE
111        FALSE
112        FALSE
113        FALSE
114        FALSE
115        FALSE
116        FALSE
117        FALSE
118        FALSE
119        FALSE
120        FALSE
121        FALSE
122        FALSE
123        FALSE
124        FALSE
125        FALSE
126        FALSE
127        FALSE
128        FALSE
129        FALSE
130        FALSE
131        FALSE
132        FALSE
133        FALSE
134        FALSE
135        FALSE
136        FALSE
137        FALSE
138        FALSE
139        FALSE
140        FALSE
141        FALSE
142        FALSE
143        FALSE
144        FALSE
145        FALSE
146        FALSE
147        FALSE
148        FALSE
149        FALSE
150        FALSE
151        FALSE
152        FALSE
153        FALSE
154        FALSE
155        FALSE
156        FALSE
157        FALSE
158        FALSE
159        FALSE
160        FALSE
161        FALSE
162        FALSE
163        FALSE
164        FALSE
165        FALSE
166        FALSE
167        FALSE
168        FALSE
169        FALSE
170        FALSE
171        FALSE
172        FALSE
173        FALSE
174        FALSE
175        FALSE
176        FALSE
```

```r
data %>%
  select(stage = description, rider_name = name, rider_nat = nationality, team_name = team.name, team_nat = team.nationality, dep_city = departure_city, arr_city = arrival_city, classification, distance, start_date = scheduled)
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
                    team_name             team_nat dep_city arr_city
1               Movistar Team                Spain Brussels Brussels
2            Mitchelton-Scott            Australia Brussels Brussels
3            Mitchelton-Scott            Australia Brussels Brussels
4          EF Education First                  USA Brussels Brussels
5      Team Katusha - Alpecin          Switzerland Brussels Brussels
6                Lotto Soudal              Belgium Brussels Brussels
7            Bahrain - Merida              Bahrain Brussels Brussels
8   Deceuninck - Quick - Step              Belgium Brussels Brussels
9      Team Katusha - Alpecin          Switzerland Brussels Brussels
10             Trek–Segafredo                  USA Brussels Brussels
11         EF Education First                  USA Brussels Brussels
12                Team Sunweb          Netherlands Brussels Brussels
13                 Team Ineos        Great Britain Brussels Brussels
14             Direct Energie               France Brussels Brussels
15                    Cofidis               France Brussels Brussels
16                    Cofidis               France Brussels Brussels
17               Lotto Soudal              Belgium Brussels Brussels
18               Lotto Soudal              Belgium Brussels Brussels
19           Bahrain - Merida              Bahrain Brussels Brussels
20         EF Education First                  USA Brussels Brussels
21           Mitchelton-Scott            Australia Brussels Brussels
22        Team Dimension Data         South Africa Brussels Brussels
23             Groupama – FDJ               France Brussels Brussels
24              Movistar Team                Spain Brussels Brussels
25             Groupama – FDJ               France Brussels Brussels
26               Lotto Soudal              Belgium Brussels Brussels
27            Astana Pro Team           Kazakhstan Brussels Brussels
28        Team Dimension Data         South Africa Brussels Brussels
29           Ag2r La Mondiale               France Brussels Brussels
30          UAE Team Emirates United Arab Emirates Brussels Brussels
31            Fortuneo-Samsic               France Brussels Brussels
32           Ag2r La Mondiale               France Brussels Brussels
33  Deceuninck - Quick - Step              Belgium Brussels Brussels
34            Astana Pro Team           Kazakhstan Brussels Brussels
35                Team Sunweb          Netherlands Brussels Brussels
36            Astana Pro Team           Kazakhstan Brussels Brussels
37            Astana Pro Team           Kazakhstan Brussels Brussels
38                    Cofidis               France Brussels Brussels
39             Groupama – FDJ               France Brussels Brussels
40                Team Sunweb          Netherlands Brussels Brussels
41                    Cofidis               France Brussels Brussels
42          UAE Team Emirates United Arab Emirates Brussels Brussels
43           Bora - Hansgrohe              Germany Brussels Brussels
44             Trek–Segafredo                  USA Brussels Brussels
45           Ag2r La Mondiale               France Brussels Brussels
46  Deceuninck - Quick - Step              Belgium Brussels Brussels
47     Team Katusha - Alpecin          Switzerland Brussels Brussels
48             Direct Energie               France Brussels Brussels
49             Trek–Segafredo                  USA Brussels Brussels
50        Wanty Groupe Gobert              Belgium Brussels Brussels
51                 Team Ineos        Great Britain Brussels Brussels
52             Direct Energie               France Brussels Brussels
53        Wanty Groupe Gobert              Belgium Brussels Brussels
54           Bahrain - Merida              Bahrain Brussels Brussels
55         Team Jumbo - Visma          Netherlands Brussels Brussels
56  Deceuninck - Quick - Step              Belgium Brussels Brussels
57                Team Sunweb          Netherlands Brussels Brussels
58             Groupama – FDJ               France Brussels Brussels
59                    Cofidis               France Brussels Brussels
60            Fortuneo-Samsic               France Brussels Brussels
61             Direct Energie               France Brussels Brussels
62         Team Jumbo - Visma          Netherlands Brussels Brussels
63           Ag2r La Mondiale               France Brussels Brussels
64          UAE Team Emirates United Arab Emirates Brussels Brussels
65                   CCC Team               Poland Brussels Brussels
66         Team Jumbo - Visma          Netherlands Brussels Brussels
67         Team Jumbo - Visma          Netherlands Brussels Brussels
68             Direct Energie               France Brussels Brussels
69            Fortuneo-Samsic               France Brussels Brussels
70                   CCC Team               Poland Brussels Brussels
71           Bora - Hansgrohe              Germany Brussels Brussels
72         Team Jumbo - Visma          Netherlands Brussels Brussels
73           Ag2r La Mondiale               France Brussels Brussels
74              Movistar Team                Spain Brussels Brussels
75        Wanty Groupe Gobert              Belgium Brussels Brussels
76                   CCC Team               Poland Brussels Brussels
77                 Team Ineos        Great Britain Brussels Brussels
78        Wanty Groupe Gobert              Belgium Brussels Brussels
79           Bora - Hansgrohe              Germany Brussels Brussels
80           Bora - Hansgrohe              Germany Brussels Brussels
81             Trek–Segafredo                  USA Brussels Brussels
82        Wanty Groupe Gobert              Belgium Brussels Brussels
83           Bora - Hansgrohe              Germany Brussels Brussels
84     Team Katusha - Alpecin          Switzerland Brussels Brussels
85  Deceuninck - Quick - Step              Belgium Brussels Brussels
86     Team Katusha - Alpecin          Switzerland Brussels Brussels
87         Team Jumbo - Visma          Netherlands Brussels Brussels
88          UAE Team Emirates United Arab Emirates Brussels Brussels
89            Astana Pro Team           Kazakhstan Brussels Brussels
90             Groupama – FDJ               France Brussels Brussels
91                 Team Ineos        Great Britain Brussels Brussels
92            Astana Pro Team           Kazakhstan Brussels Brussels
93           Mitchelton-Scott            Australia Brussels Brussels
94         EF Education First                  USA Brussels Brussels
95        Team Dimension Data         South Africa Brussels Brussels
96         Team Jumbo - Visma          Netherlands Brussels Brussels
97             Trek–Segafredo                  USA Brussels Brussels
98           Ag2r La Mondiale               France Brussels Brussels
99        Wanty Groupe Gobert              Belgium Brussels Brussels
100        EF Education First                  USA Brussels Brussels
101            Direct Energie               France Brussels Brussels
102                   Cofidis               France Brussels Brussels
103            Trek–Segafredo                  USA Brussels Brussels
104           Fortuneo-Samsic               France Brussels Brussels
105         UAE Team Emirates United Arab Emirates Brussels Brussels
106              Lotto Soudal              Belgium Brussels Brussels
107         UAE Team Emirates United Arab Emirates Brussels Brussels
108          Ag2r La Mondiale               France Brussels Brussels
109          Ag2r La Mondiale               France Brussels Brussels
110            Direct Energie               France Brussels Brussels
111             Movistar Team                Spain Brussels Brussels
112          Bora - Hansgrohe              Germany Brussels Brussels
113       Team Dimension Data         South Africa Brussels Brussels
114          Bahrain - Merida              Bahrain Brussels Brussels
115            Trek–Segafredo                  USA Brussels Brussels
116              Lotto Soudal              Belgium Brussels Brussels
117               Team Sunweb          Netherlands Brussels Brussels
118             Movistar Team                Spain Brussels Brussels
119           Fortuneo-Samsic               France Brussels Brussels
120           Fortuneo-Samsic               France Brussels Brussels
121       Team Dimension Data         South Africa Brussels Brussels
122                  CCC Team               Poland Brussels Brussels
123        EF Education First                  USA Brussels Brussels
124            Groupama – FDJ               France Brussels Brussels
125        EF Education First                  USA Brussels Brussels
126                  CCC Team               Poland Brussels Brussels
127       Team Dimension Data         South Africa Brussels Brussels
128                  CCC Team               Poland Brussels Brussels
129            Groupama – FDJ               France Brussels Brussels
130 Deceuninck - Quick - Step              Belgium Brussels Brussels
131        EF Education First                  USA Brussels Brussels
132          Bora - Hansgrohe              Germany Brussels Brussels
133    Team Katusha - Alpecin          Switzerland Brussels Brussels
134       Team Dimension Data         South Africa Brussels Brussels
135         UAE Team Emirates United Arab Emirates Brussels Brussels
136          Mitchelton-Scott            Australia Brussels Brussels
137          Mitchelton-Scott            Australia Brussels Brussels
138       Team Dimension Data         South Africa Brussels Brussels
139           Fortuneo-Samsic               France Brussels Brussels
140                  CCC Team               Poland Brussels Brussels
141       Wanty Groupe Gobert              Belgium Brussels Brussels
142             Movistar Team                Spain Brussels Brussels
143                   Cofidis               France Brussels Brussels
144             Movistar Team                Spain Brussels Brussels
145          Bahrain - Merida              Bahrain Brussels Brussels
146       Wanty Groupe Gobert              Belgium Brussels Brussels
147    Team Katusha - Alpecin          Switzerland Brussels Brussels
148                   Cofidis               France Brussels Brussels
149           Astana Pro Team           Kazakhstan Brussels Brussels
150          Mitchelton-Scott            Australia Brussels Brussels
151          Mitchelton-Scott            Australia Brussels Brussels
152               Team Sunweb          Netherlands Brussels Brussels
153                Team Ineos        Great Britain Brussels Brussels
154                Team Ineos        Great Britain Brussels Brussels
155          Bahrain - Merida              Bahrain Brussels Brussels
156            Direct Energie               France Brussels Brussels
157         UAE Team Emirates United Arab Emirates Brussels Brussels
158              Lotto Soudal              Belgium Brussels Brussels
159 Deceuninck - Quick - Step              Belgium Brussels Brussels
160           Astana Pro Team           Kazakhstan Brussels Brussels
161                  CCC Team               Poland Brussels Brussels
162                Team Ineos        Great Britain Brussels Brussels
163 Deceuninck - Quick - Step              Belgium Brussels Brussels
164             Movistar Team                Spain Brussels Brussels
165            Groupama – FDJ               France Brussels Brussels
166          Bahrain - Merida              Bahrain Brussels Brussels
167                Team Ineos        Great Britain Brussels Brussels
168          Bora - Hansgrohe              Germany Brussels Brussels
169               Team Sunweb          Netherlands Brussels Brussels
170          Bahrain - Merida              Bahrain Brussels Brussels
171              Lotto Soudal              Belgium Brussels Brussels
172            Trek–Segafredo                  USA Brussels Brussels
173        Team Jumbo - Visma          Netherlands Brussels Brussels
174           Fortuneo-Samsic               France Brussels Brussels
175    Team Katusha - Alpecin          Switzerland Brussels Brussels
176               Team Sunweb          Netherlands Brussels Brussels
     classification distance                start_date
1   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
2   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
3   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
4   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
5   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
6   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
7   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
8   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
9   Team Time Trial     27,6 2019-07-07T12:30:00+00:00
10  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
11  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
12  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
13  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
14  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
15  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
16  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
17  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
18  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
19  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
20  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
21  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
22  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
23  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
24  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
25  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
26  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
27  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
28  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
29  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
30  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
31  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
32  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
33  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
34  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
35  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
36  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
37  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
38  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
39  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
40  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
41  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
42  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
43  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
44  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
45  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
46  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
47  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
48  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
49  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
50  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
51  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
52  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
53  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
54  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
55  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
56  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
57  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
58  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
59  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
60  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
61  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
62  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
63  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
64  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
65  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
66  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
67  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
68  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
69  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
70  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
71  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
72  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
73  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
74  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
75  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
76  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
77  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
78  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
79  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
80  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
81  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
82  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
83  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
84  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
85  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
86  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
87  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
88  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
89  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
90  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
91  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
92  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
93  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
94  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
95  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
96  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
97  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
98  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
99  Team Time Trial     27,6 2019-07-07T12:30:00+00:00
100 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
101 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
102 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
103 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
104 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
105 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
106 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
107 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
108 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
109 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
110 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
111 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
112 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
113 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
114 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
115 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
116 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
117 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
118 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
119 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
120 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
121 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
122 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
123 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
124 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
125 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
126 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
127 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
128 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
129 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
130 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
131 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
132 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
133 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
134 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
135 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
136 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
137 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
138 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
139 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
140 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
141 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
142 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
143 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
144 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
145 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
146 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
147 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
148 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
149 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
150 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
151 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
152 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
153 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
154 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
155 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
156 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
157 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
158 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
159 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
160 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
161 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
162 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
163 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
164 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
165 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
166 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
167 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
168 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
169 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
170 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
171 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
172 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
173 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
174 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
175 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
176 Team Time Trial     27,6 2019-07-07T12:30:00+00:00
```


```r
for (n in (1:length(tdf[[1]]$stage$competitors))) {
  print(tdf[[1]]$stage$competitors[[n]]$name)
}
```

```
[1] "Teunissen, Mike"
[1] "Sagan, Peter"
[1] "Ewan, Caleb"
[1] "Nizzolo, Giacomo"
[1] "Colbrelli, Sonny"
[1] "Matthews, Michael"
[1] "Trentin, Matteo"
[1] "Naesen, Olivier"
[1] "Viviani, Elia"
[1] "Stuyven, Jasper"
[1] "Van Avermaet, Greg"
[1] "Bettiol, Alberto"
[1] "Pasqualon, Andrea"
[1] "Kristoff, Alexander"
[1] "Jansen Groendahl, Amund"
[1] "Simon, Julien"
[1] "Van Aert, Wout"
[1] "Laporte, Christophe"
[1] "Greipel, Andre"
[1] "Impey, Daryl"
[1] "Martin, Guillaume"
[1] "Alaphilippe, Julian"
[1] "Offredo, Yoann"
[1] "Clarke, Simon"
[1] "Nibali, Vincenzo"
[1] "Bevin, Patrick"
[1] "Meurisse, Xandro"
[1] "Langeveld, Sebastian"
[1] "de Buyst, Jasper"
[1] "Richeze Araquistain, Ariel Maximiliano"
[1] "Debusschere, Jens"
[1] "Hagen, Edvald Boasson"
[1] "Asgreen, Kasper"
[1] "Bol, Cees"
[1] "Garcia Cortina, Ivan"
[1] "Burghardt, Marcus"
[1] "Bonifazio, Niccolo"
[1] "Moerkoev, Michael"
[1] "Tratnik, Jan"
[1] "Roche, Nicolas"
[1] "Zabel, Rick"
[1] "Konrad, Patrick"
[1] "Philipsen, Jasper"
[1] "Keukeleire, Jens"
[1] "Hepburn, Michael"
[1] "Yates, Adam"
[1] "Kreuziger, Roman"
[1] "Teuns, Dylan"
[1] "Kluge, Roger"
[1] "Lampaert, Yves"
[1] "Mas Nicolau, Enric"
[1] "Benoot, Tiesj"
[1] "Quintana, Nairo"
[1] "Lutsenko, Alexey"
[1] "Perichon, Pierre-Luc"
[1] "Kruijswijk, Steven"
[1] "Amador, Andrey"
[1] "Calmejane, Lilian"
[1] "Politt, Nils"
[1] "Ciccone, Giulio"
[1] "Oss, Daniel"
[1] "Eiking, Odd Christian"
[1] "Backaert, Fredrik"
[1] "Porte, Richie"
[1] "Gaudu, David"
[1] "Molard, Rudy"
[1] "Valverde, Alejandro"
[1] "Valgren Andersen, Michael"
[1] "Felline, Fabio"
[1] "Schachmann, Maximilian"
[1] "Muhlberger, Gregor"
[1] "Ladagnous, Matthieu"
[1] "Kelderman, Wilco"
[1] "Izagirre Insausti, Gorka"
[1] "Van Garderen, Tejay"
[1] "Pinot, Thibaut"
[1] "Sicard, Romain"
[1] "Martin, Tony"
[1] "Sanchez Gil, Luis Leon"
[1] "Moscon, Gianni"
[1] "Bernal, Egan"
[1] "Uran, Rigoberto"
[1] "Soler Gimenez, Marc"
[1] "Henao Montoya, Sergio Luis"
[1] "Janse van Rensburg, Reinhardt"
[1] "Kamna, Lennard"
[1] "Woods, Michael"
[1] "Landa Meana, Mikel"
[1] "Cherel, Mikael"
[1] "de Plus, Laurens"
[1] "Houle, Hugo"
[1] "Bardet, Romain"
[1] "Fuglsang, Jakob"
[1] "Santos Simoes Oliveira, Nelson Filipe"
[1] "Ourselin, Paul"
[1] "Nielsen, Magnus Cort"
[1] "Fraile Matarranz, Omar"
[1] "Wurtz Schmidt, Mads"
[1] "Turgis, Anthony"
[1] "Berhane, Natnael"
[1] "Barguil, Warren"
[1] "Goncalves, Jose"
[1] "Zakarin, Ilnur"
[1] "Durbridge, Luke"
[1] "Aru, Fabio"
[1] "Laengen, Vegard Stake"
[1] "Kragh Andersen, Soeren"
[1] "Taaramae, Rein"
[1] "Kangert, Tanel"
[1] "Dowsett, Alex"
[1] "Thomas, Geraint"
[1] "Schaer, Michael"
[1] "Caruso, Damiano"
[1] "Rosskopf, Joey"
[1] "Geschke, Simon"
[1] "De Kort, Koen"
[1] "Bernard, Julien"
[1] "Edet, Nicolas"
[1] "Arndt, Nikias"
[1] "Faria Da Costa, Rui Alberto"
[1] "Martin, Daniel"
[1] "van Melsen, Kevin"
[1] "Poels, Wouter"
[1] "Wellens, Tim"
[1] "Kung, Stefan"
[1] "Moinard, Amael"
[1] "Delaplace, Anthony"
[1] "de Gendt, Aime"
[1] "Bilbao, Pello"
[1] "De Gendt, Thomas"
[1] "Monfort, Maxime"
[1] "King, Benjamin"
[1] "Roux, Anthony"
[1] "Bonnet, William"
[1] "Frank, Mathias"
[1] "Gallopin, Tony"
[1] "Reichenbach, Sebastien"
[1] "Bak, Lars Ytting"
[1] "Bouet, Maxime"
[1] "Scully, Thomas"
[1] "Herrada Lopez, Jesus"
[1] "Cummings, Steven"
[1] "Grellier, Fabien"
[1] "Perez, Anthony"
[1] "Haga, Chad"
[1] "Yates, Simon"
[1] "Haig, Jack"
[1] "Vachon, Florian"
[1] "Ledanois, Kevin"
[1] "Erviti, Imanol"
[1] "de Marchi, Alessandro"
[1] "Pauwels, Serge"
[1] "Bystroem, Sven Erik"
[1] "van Baarle, Dylan"
[1] "Mollema, Bauke"
[1] "Gougeard, Alexis"
[1] "Terpstra, Niki"
[1] "Dennis, Rohan"
[1] "Mohoric, Matej"
[1] "Kwiatkowski, Michal"
[1] "Juul-Jensen, Christopher"
[1] "Rowe, Luke"
[1] "Rossetto, Stephane"
[1] "Vuillermoz, Alexis"
[1] "Skujins, Toms"
[1] "Verona Quintanilla, Carlos"
[1] "Haller, Marco"
[1] "Gesbert, Elie"
[1] "Devenyns, Dries"
[1] "Wisniowski, Lukasz"
[1] "Castroviejo, Nicolas Jonathan"
[1] "Bennett, George"
[1] "Buchmann, Emanuel"
[1] "Postlberger, Lukas"
[1] "Groenewegen, Dylan"
[1] "Cosnefroy, Benoit"
```
