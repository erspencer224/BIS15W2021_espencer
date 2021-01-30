---
title: "Lab 7 Homework"
author: "Emily Spencer"
date: "2021-01-30"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

## Data
**1. For this homework, we will use two different data sets. Please load `amniota` and `amphibio`.**  

`amniota` data:  
Myhrvold N, Baldridge E, Chan B, Sivam D, Freeman DL, Ernest SKM (2015). “An amniote life-history
database to perform comparative analyses with birds, mammals, and reptiles.” _Ecology_, *96*, 3109.
doi: 10.1890/15-0846.1 (URL: https://doi.org/10.1890/15-0846.1).

```r
amniota <- readr::read_csv("data/amniota.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   common_name = col_character()
## )
## i Use `spec()` for the full column specifications.
```

`amphibio` data:  
Oliveira BF, São-Pedro VA, Santos-Barrera G, Penone C, Costa GC (2017). “AmphiBIO, a global database
for amphibian ecological traits.” _Scientific Data_, *4*, 170123. doi: 10.1038/sdata.2017.123 (URL:
https://doi.org/10.1038/sdata.2017.123).

```r
amphibio <- readr::read_csv("data/amphibio.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   id = col_character(),
##   Order = col_character(),
##   Family = col_character(),
##   Genus = col_character(),
##   Species = col_character(),
##   Seeds = col_logical(),
##   OBS = col_logical()
## )
## i Use `spec()` for the full column specifications.
```

```
## Warning: 125 parsing failures.
##  row col           expected                                                           actual                file
## 1410 OBS 1/0/T/F/TRUE/FALSE Identified as P. appendiculata in Boquimpani-Freitas et al. 2002 'data/amphibio.csv'
## 1416 OBS 1/0/T/F/TRUE/FALSE Identified as T. miliaris in Giaretta and Facure 2004            'data/amphibio.csv'
## 1447 OBS 1/0/T/F/TRUE/FALSE Considered endangered by Soto-Azat et al. 2013                   'data/amphibio.csv'
## 1448 OBS 1/0/T/F/TRUE/FALSE Considered extinct by Soto-Azat et al. 2013                      'data/amphibio.csv'
## 1471 OBS 1/0/T/F/TRUE/FALSE nomem dubitum                                                    'data/amphibio.csv'
## .... ... .................. ................................................................ ...................
## See problems(...) for more details.
```

## Questions  
**2. Do some exploratory analysis of the `amniota` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  


```r
glimpse(amniota)
```

```
## Rows: 21,322
## Columns: 36
## $ class                                 <chr> "Aves", "Aves", "Aves", "Aves...
## $ order                                 <chr> "Accipitriformes", "Accipitri...
## $ family                                <chr> "Accipitridae", "Accipitridae...
## $ genus                                 <chr> "Accipiter", "Accipiter", "Ac...
## $ species                               <chr> "albogularis", "badius", "bic...
## $ subspecies                            <dbl> -999, -999, -999, -999, -999,...
## $ common_name                           <chr> "Pied Goshawk", "Shikra", "Bi...
## $ female_maturity_d                     <dbl> -999.000, 363.468, -999.000, ...
## $ litter_or_clutch_size_n               <dbl> -999.000, 3.250, 2.700, -999....
## $ litters_or_clutches_per_y             <dbl> -999, 1, -999, -999, 1, -999,...
## $ adult_body_mass_g                     <dbl> 251.500, 140.000, 345.000, 14...
## $ maximum_longevity_y                   <dbl> -999.00000, -999.00000, -999....
## $ gestation_d                           <dbl> -999, -999, -999, -999, -999,...
## $ weaning_d                             <dbl> -999, -999, -999, -999, -999,...
## $ birth_or_hatching_weight_g            <dbl> -999, -999, -999, -999, -999,...
## $ weaning_weight_g                      <dbl> -999, -999, -999, -999, -999,...
## $ egg_mass_g                            <dbl> -999.00, 21.00, 32.00, -999.0...
## $ incubation_d                          <dbl> -999.00, 30.00, -999.00, -999...
## $ fledging_age_d                        <dbl> -999.00, 32.00, -999.00, -999...
## $ longevity_y                           <dbl> -999.00000, -999.00000, -999....
## $ male_maturity_d                       <dbl> -999, -999, -999, -999, -999,...
## $ inter_litter_or_interbirth_interval_y <dbl> -999, -999, -999, -999, -999,...
## $ female_body_mass_g                    <dbl> 352.500, 168.500, 390.000, -9...
## $ male_body_mass_g                      <dbl> 223.000, 125.000, 212.000, 14...
## $ no_sex_body_mass_g                    <dbl> -999.0, 123.0, -999.0, -999.0...
## $ egg_width_mm                          <dbl> -999, -999, -999, -999, -999,...
## $ egg_length_mm                         <dbl> -999, -999, -999, -999, -999,...
## $ fledging_mass_g                       <dbl> -999, -999, -999, -999, -999,...
## $ adult_svl_cm                          <dbl> -999.00, 30.00, 39.50, -999.0...
## $ male_svl_cm                           <dbl> -999, -999, -999, -999, -999,...
## $ female_svl_cm                         <dbl> -999, -999, -999, -999, -999,...
## $ birth_or_hatching_svl_cm              <dbl> -999, -999, -999, -999, -999,...
## $ female_svl_at_maturity_cm             <dbl> -999, -999, -999, -999, -999,...
## $ female_body_mass_at_maturity_g        <dbl> -999, -999, -999, -999, -999,...
## $ no_sex_svl_cm                         <dbl> -999, -999, -999, -999, -999,...
## $ no_sex_maturity_d                     <dbl> -999, -999, -999, -999, -999,...
```

```r
amniota %>% 
  summarise_all(~(sum(is.na(.))))
```

```
## # A tibble: 1 x 36
##   class order family genus species subspecies common_name female_maturity~
##   <int> <int>  <int> <int>   <int>      <int>       <int>            <int>
## 1     0     0      0     0       0          0           0                0
## # ... with 28 more variables: litter_or_clutch_size_n <int>,
## #   litters_or_clutches_per_y <int>, adult_body_mass_g <int>,
## #   maximum_longevity_y <int>, gestation_d <int>, weaning_d <int>,
## #   birth_or_hatching_weight_g <int>, weaning_weight_g <int>, egg_mass_g <int>,
## #   incubation_d <int>, fledging_age_d <int>, longevity_y <int>,
## #   male_maturity_d <int>, inter_litter_or_interbirth_interval_y <int>,
## #   female_body_mass_g <int>, male_body_mass_g <int>, no_sex_body_mass_g <int>,
## #   egg_width_mm <int>, egg_length_mm <int>, fledging_mass_g <int>,
## #   adult_svl_cm <int>, male_svl_cm <int>, female_svl_cm <int>,
## #   birth_or_hatching_svl_cm <int>, female_svl_at_maturity_cm <int>,
## #   female_body_mass_at_maturity_g <int>, no_sex_svl_cm <int>,
## #   no_sex_maturity_d <int>
```
*NAs are represented with "-999" in this data.*

**3. Do some exploratory analysis of the `amphibio` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  


```r
glimpse(amphibio)
```

```
## Rows: 6,776
## Columns: 38
## $ id                      <chr> "Anf0001", "Anf0002", "Anf0003", "Anf0004",...
## $ Order                   <chr> "Anura", "Anura", "Anura", "Anura", "Anura"...
## $ Family                  <chr> "Allophrynidae", "Alytidae", "Alytidae", "A...
## $ Genus                   <chr> "Allophryne", "Alytes", "Alytes", "Alytes",...
## $ Species                 <chr> "Allophryne ruthveni", "Alytes cisternasii"...
## $ Fos                     <dbl> NA, NA, NA, NA, NA, 1, 1, 1, 1, 1, 1, 1, 1,...
## $ Ter                     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
## $ Aqu                     <dbl> 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, ...
## $ Arb                     <dbl> 1, 1, 1, 1, 1, 1, NA, NA, NA, NA, NA, NA, N...
## $ Leaves                  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Flowers                 <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Seeds                   <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Fruits                  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Arthro                  <dbl> 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1, 1, NA, N...
## $ Vert                    <dbl> NA, NA, NA, NA, NA, NA, 1, NA, NA, NA, 1, 1...
## $ Diu                     <dbl> 1, NA, NA, NA, NA, NA, 1, 1, 1, NA, 1, 1, N...
## $ Noc                     <dbl> 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1, 1, 1, NA...
## $ Crepu                   <dbl> 1, NA, NA, NA, NA, 1, NA, NA, NA, NA, NA, N...
## $ Wet_warm                <dbl> NA, NA, NA, NA, 1, 1, NA, NA, NA, NA, 1, NA...
## $ Wet_cold                <dbl> 1, NA, NA, NA, NA, NA, 1, NA, NA, NA, NA, N...
## $ Dry_warm                <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Dry_cold                <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ Body_mass_g             <dbl> 31.00, 6.10, NA, NA, 2.31, 13.40, 21.80, NA...
## $ Age_at_maturity_min_y   <dbl> NA, 2.0, 2.0, NA, 3.0, 2.0, 3.0, NA, NA, NA...
## $ Age_at_maturity_max_y   <dbl> NA, 2.0, 2.0, NA, 3.0, 3.0, 5.0, NA, NA, NA...
## $ Body_size_mm            <dbl> 31.0, 50.0, 55.0, NA, 40.0, 55.0, 80.0, 60....
## $ Size_at_maturity_min_mm <dbl> NA, 27, NA, NA, NA, 35, NA, NA, NA, NA, NA,...
## $ Size_at_maturity_max_mm <dbl> NA, 36.0, NA, NA, NA, 40.5, NA, NA, NA, NA,...
## $ Longevity_max_y         <dbl> NA, 6, NA, NA, NA, 7, 9, NA, NA, NA, NA, NA...
## $ Litter_size_min_n       <dbl> 300, 60, 40, NA, 7, 53, 300, 1500, 1000, NA...
## $ Litter_size_max_n       <dbl> 300, 180, 40, NA, 20, 171, 1500, 1500, 1000...
## $ Reproductive_output_y   <dbl> 1, 4, 1, 4, 1, 4, 6, 1, 1, 1, 1, 1, 1, 1, N...
## $ Offspring_size_min_mm   <dbl> NA, 2.6, NA, NA, 5.4, 2.6, 1.5, NA, 1.5, NA...
## $ Offspring_size_max_mm   <dbl> NA, 3.5, NA, NA, 7.0, 5.0, 2.0, NA, 1.5, NA...
## $ Dir                     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
## $ Lar                     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
## $ Viv                     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
## $ OBS                     <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
```

```r
amphibio %>% 
  summarise_all(~(sum(is.na(.))))
```

```
## # A tibble: 1 x 38
##      id Order Family Genus Species   Fos   Ter   Aqu   Arb Leaves Flowers Seeds
##   <int> <int>  <int> <int>   <int> <int> <int> <int> <int>  <int>   <int> <int>
## 1     0     0      0     0       0  6053  1104  2810  4347   6752    6772  6772
## # ... with 26 more variables: Fruits <int>, Arthro <int>, Vert <int>,
## #   Diu <int>, Noc <int>, Crepu <int>, Wet_warm <int>, Wet_cold <int>,
## #   Dry_warm <int>, Dry_cold <int>, Body_mass_g <int>,
## #   Age_at_maturity_min_y <int>, Age_at_maturity_max_y <int>,
## #   Body_size_mm <int>, Size_at_maturity_min_mm <int>,
## #   Size_at_maturity_max_mm <int>, Longevity_max_y <int>,
## #   Litter_size_min_n <int>, Litter_size_max_n <int>,
## #   Reproductive_output_y <int>, Offspring_size_min_mm <int>,
## #   Offspring_size_max_mm <int>, Dir <int>, Lar <int>, Viv <int>, OBS <int>
```
*NAs are represented with "NA" in this data.*

**4. How many total NA's are in each data set? Do these values make sense? Are NA's represented by values?**   


```r
amniota %>% 
  summarize(number_nas = sum(is.na(.)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1          0
```
*This makes sense because NAs in this data are represented by "-999" not "NA".*


```r
amphibio %>% 
  summarize(number_nas = sum(is.na(.)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1     170691
```
*This makes snese because NAs in this data are represented by "NA".*

**5. Make any necessary replacements in the data such that all NA's appear as "NA".**   

```r
amniota_tidy <- amniota %>% 
  na_if("-999")

amniota_tidy %>% 
  summarize(number_nas = sum(is.na(.)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1     528196
```


```r
amphibio %>% 
  summarize(number_nas = sum(is.na(.)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1     170691
```

**6. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amniota` data.**  

```r
naniar::miss_var_summary(amniota_tidy)
```

```
## # A tibble: 36 x 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <dbl>
##  1 subspecies                      21322    100  
##  2 female_body_mass_at_maturity_g  21318    100. 
##  3 female_svl_at_maturity_cm       21120     99.1
##  4 fledging_mass_g                 21111     99.0
##  5 male_svl_cm                     21040     98.7
##  6 no_sex_maturity_d               20860     97.8
##  7 egg_width_mm                    20727     97.2
##  8 egg_length_mm                   20702     97.1
##  9 weaning_weight_g                20258     95.0
## 10 female_svl_cm                   20242     94.9
## # ... with 26 more rows
```

**7. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amphibio` data.**

```r
naniar::miss_var_summary(amphibio)
```

```
## # A tibble: 38 x 3
##    variable n_miss pct_miss
##    <chr>     <int>    <dbl>
##  1 OBS        6776    100  
##  2 Fruits     6774    100. 
##  3 Flowers    6772     99.9
##  4 Seeds      6772     99.9
##  5 Leaves     6752     99.6
##  6 Dry_cold   6735     99.4
##  7 Vert       6657     98.2
##  8 Wet_cold   6625     97.8
##  9 Crepu      6608     97.5
## 10 Dry_warm   6572     97.0
## # ... with 28 more rows
```

**8. For the `amniota` data, calculate the number of NAs in the `egg_mass_g` column sorted by taxonomic class; i.e. how many NA's are present in the `egg_mass_g` column in birds, mammals, and reptiles? Does this results make sense biologically? How do these results affect your interpretation of NA's?**  


```r
amniota_tidy %>% 
  select(class, egg_mass_g) %>% 
  group_by(class) %>% 
  naniar::miss_var_summary(order=T)
```

```
## # A tibble: 3 x 4
## # Groups:   class [3]
##   class    variable   n_miss pct_miss
##   <chr>    <chr>       <int>    <dbl>
## 1 Aves     egg_mass_g   4914     50.1
## 2 Mammalia egg_mass_g   4953    100  
## 3 Reptilia egg_mass_g   6040     92.0
```

**9. The `amphibio` data have variables that classify species as fossorial (burrowing), terrestrial, aquatic, or arboreal.Calculate the number of NA's in each of these variables. Do you think that the authors intend us to think that there are NA's in these columns or could they represent something else? Explain.**

```r
amphibio %>% 
  select(Fos, Ter, Aqu, Arb) %>% 
  summarise_all(~(sum(is.na(.))))
```

```
## # A tibble: 1 x 4
##     Fos   Ter   Aqu   Arb
##   <int> <int> <int> <int>
## 1  6053  1104  2810  4347
```
*I don't think the author intended us to think of the NAs as missing data, but instead as an indication that a species is not for example, an arboreal species. If a species is a fossorial species then for Ter, Aqu, and Arb the data will show NA because the species isn't defined as those things.* 

**10. Now that we know how NA's are represented in the `amniota` data, how would you load the data such that the values which represent NA's are automatically converted?**

```r
amniota_2 <- readr::read_csv("data/amniota.csv") %>% 
  na_if("-999")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   common_name = col_character()
## )
## i Use `spec()` for the full column specifications.
```
*below code is to check work*

```r
amniota_2 %>% 
  summarise_all(~(sum(is.na(.))))
```

```
## # A tibble: 1 x 36
##   class order family genus species subspecies common_name female_maturity~
##   <int> <int>  <int> <int>   <int>      <int>       <int>            <int>
## 1     0     0      0     0       0      21322        1641            17849
## # ... with 28 more variables: litter_or_clutch_size_n <int>,
## #   litters_or_clutches_per_y <int>, adult_body_mass_g <int>,
## #   maximum_longevity_y <int>, gestation_d <int>, weaning_d <int>,
## #   birth_or_hatching_weight_g <int>, weaning_weight_g <int>, egg_mass_g <int>,
## #   incubation_d <int>, fledging_age_d <int>, longevity_y <int>,
## #   male_maturity_d <int>, inter_litter_or_interbirth_interval_y <int>,
## #   female_body_mass_g <int>, male_body_mass_g <int>, no_sex_body_mass_g <int>,
## #   egg_width_mm <int>, egg_length_mm <int>, fledging_mass_g <int>,
## #   adult_svl_cm <int>, male_svl_cm <int>, female_svl_cm <int>,
## #   birth_or_hatching_svl_cm <int>, female_svl_at_maturity_cm <int>,
## #   female_body_mass_at_maturity_g <int>, no_sex_svl_cm <int>,
## #   no_sex_maturity_d <int>
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
