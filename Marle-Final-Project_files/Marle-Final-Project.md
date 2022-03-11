---
title: "Marle Final Project"
author: "Marle Lamountry"
date: "3/8/2022"
output: 
  html_document: 
    keep_md: yes
---




```r
library(here)
```

```
## here() starts at /Users/numfon/Desktop/bis15lw2022group11
```

```r
library(readr)
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ dplyr   1.0.8
## ✓ tibble  3.1.6     ✓ stringr 1.4.0
## ✓ tidyr   1.2.0     ✓ forcats 0.5.1
## ✓ purrr   0.3.4
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(shiny)
library(shinydashboard)
```

```
## 
## Attaching package: 'shinydashboard'
```

```
## The following object is masked from 'package:graphics':
## 
##     box
```

```r
getwd()
```

```
## [1] "/Users/numfon/Desktop/bis15lw2022group11"
```



```r
bird<-read_csv(here("BirdFuncDat.csv"))
```

```
## Warning: One or more parsing issues, see `problems()` for details
```

```
## Rows: 9995 Columns: 40
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (15): PassNonPass, IOCOrder, BLFamilyLatin, BLFamilyEnglish, Taxo, Scien...
## dbl (24): SpecID, BLFamSequID, Diet-Inv, Diet-Vend, Diet-Vect, Diet-Vfish, D...
## lgl  (1): Record-Comment
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
glimpse(bird)
```

```
## Rows: 9,995
## Columns: 40
## $ SpecID                   <dbl> 28, 37, 38, 45, 46, 47, 48, 55, 57, 58, 65, 6…
## $ PassNonPass              <chr> "Nonpasseriformes", "Nonpasseriformes", "Nonp…
## $ IOCOrder                 <chr> "Struthioniformes", "Rheiformes", "Rheiformes…
## $ BLFamilyLatin            <chr> "Struthionidae", "Rheidae", "Rheidae", "Casua…
## $ BLFamilyEnglish          <chr> "Ostriches", "Rheas", "Rheas", "Cassowaries",…
## $ BLFamSequID              <dbl> 2, 3, 3, 4, 4, 4, 5, 6, 6, 6, 1, 1, 1, 1, 1, …
## $ Taxo                     <chr> "BL3", "BL3", "BL3", "BL3", "BL3", "BL3", "BL…
## $ Scientific               <chr> "Struthio camelus", "Rhea americana", "Rhea p…
## $ English                  <chr> "Ostrich", "Greater Rhea", "Lesser Rhea", "So…
## $ `Diet-Inv`               <dbl> 10, 20, 20, 10, 10, 20, 20, 80, 80, 100, 10, …
## $ `Diet-Vend`              <dbl> 0, 10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
## $ `Diet-Vect`              <dbl> 0, 10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 10, 0…
## $ `Diet-Vfish`             <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `Diet-Vunk`              <dbl> 10, 0, 10, 10, 10, 10, 0, 0, 0, 0, 0, 0, 0, 0…
## $ `Diet-Scav`              <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `Diet-Fruit`             <dbl> 0, 20, 0, 80, 80, 60, 30, 10, 10, 0, 40, 40, …
## $ `Diet-Nect`              <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `Diet-Seed`              <dbl> 30, 20, 30, 0, 0, 0, 30, 0, 0, 0, 30, 20, 40,…
## $ `Diet-PlantO`            <dbl> 50, 20, 40, 0, 0, 10, 20, 10, 10, 0, 20, 20, …
## $ `Diet-5Cat`              <chr> "PlantSeed", "Omnivore", "PlantSeed", "FruiNe…
## $ `Diet-Source`            <chr> "Ref_1", "Ref_1", "Ref_1", "Ref_1", "Ref_1", …
## $ `Diet-Certainty`         <chr> "A", "A", "A", "A", "B", "A", "A", "A", "A", …
## $ `Diet-EnteredBy`         <chr> "Jennifer", "Jennifer", "Jennifer", "Jennifer…
## $ `ForStrat-watbelowsurf`  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `ForStrat-wataroundsurf` <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `ForStrat-ground`        <dbl> 100, 100, 100, 80, 80, 80, 20, 100, 80, 80, 1…
## $ `ForStrat-understory`    <dbl> 0, 0, 0, 20, 20, 20, 80, 0, 20, 20, 0, 0, 0, …
## $ `ForStrat-midhigh`       <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `ForStrat-canopy`        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `ForStrat-aerial`        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ PelagicSpecialist        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ `ForStrat-Source`        <chr> "Ref_1", "Ref_1", "Ref_1", "Ref_1", "Ref_1", …
## $ `ForStrat-SpecLevel`     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, …
## $ `ForStrat-EnteredBy`     <chr> "Jessica", "Jessica", "Jessica", "Jessica", "…
## $ Nocturnal                <dbl> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, …
## $ `BodyMass-Value`         <dbl> 111000.00, 23000.00, 23900.00, 44000.00, 3499…
## $ `BodyMass-Source`        <chr> "Dunning08", "Dunning08", "Dunning08", "Dunni…
## $ `BodyMass-SpecLevel`     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ `BodyMass-Comment`       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ `Record-Comment`         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
```

```r
bird_new<-read_csv(here("bird_tidy.csv"))
```

```
## Rows: 9995 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (5): ioc_order, bl_family_english, scientific, english, diet_5cat
## dbl (19): diet_inv, diet_vend, diet_vect, diet_vfish, diet_vunk, diet_scav, ...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

#which diet types are nocturnal

```r
bird_new%>%
  na.exclude()%>%
  filter(nocturnal=="1")%>%
  ggplot(aes(x=ioc_order,y=diet_5cat,fill=nocturnal))+
  geom_tile()+
  scale_fill_gradient(low = "#fbb4ae")+
  geom_path(size=1)+
  theme_linedraw()+
  theme(axis.title.x = element_text(size = rel(1)))+coord_flip()+
  labs(title = 'Each Orders Diet and if They are Nocturnal',
       x="Order", y="Diet")
```

![](Marle-Final-Project_files/figure-html/unnamed-chunk-5-1.png)<!-- -->
#which diets have which migratory strategies

```r
diet_migration<-bird_new%>%
  select(diet_5cat,contains("for_strat_"))
```

```r
migration_long1<-diet_migration%>%
  pivot_longer(names_to = "Migration",
               names_prefix="for_strat_",
               values_to="Population",
               'for_strat_watbelowsurf':'for_strat_aerial')
```
#Amount of each Migration Strategy for each Diet Type

```r
migration_long1%>%
  na.exclude()%>%
  ggplot(aes(x=Population,y=Migration,fill=diet_5cat))+
  geom_col()+
  geom_path()+
  facet_wrap(~diet_5cat)+
  theme_linedraw()+
  theme(axis.line.x = element_line(size = rel(1)))+
    labs(title = "Pop of Migration Strategies with Diet Types",
       y="Migration", x= "Population")
```

![](Marle-Final-Project_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
#Migration strats for Nocturnal Species

```r
nocturnal_species<-bird_new%>%
  select(ioc_order,nocturnal,contains("for_strat_"))%>%
  filter(nocturnal=="1")
```

```r
nocturnal_species_long<-nocturnal_species%>%
  pivot_longer(names_to = "Migration",
               names_prefix="for_strat_",
               values_to="Population",
               'for_strat_watbelowsurf':'for_strat_aerial')
```

```r
nocturnal_species_long%>%
  ggplot(aes(x=Population,y=Migration,fill=nocturnal))+
  geom_col()+
  facet_wrap(~ioc_order)+
  theme_linedraw()+
  theme(axis.line.x = element_line(size = rel(1)))+
  labs(title = "Migration Strategies of Each Nocturnal Order")
```

![](Marle-Final-Project_files/figure-html/unnamed-chunk-11-1.png)<!-- -->


