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
# to get stage : tdf[[n]]$stage$description for n 1-3
# to get ridername : tdf[[i]]$stage$competitors[[j]]$name for i 1-3 and all j, length(tdf[[i]]$stage$competitors
# to get ridernationality : tdf[[i]]$stage$competitors[[j]]$nationality for i 1-3 and all j, length(tdf[[i]]$stage$competitors


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
