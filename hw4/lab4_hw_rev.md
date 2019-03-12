---
title: "Lab 4 Homework"
author: "Tricia Nguyen"
date: "Winter 2019"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our [GitHub repository](https://github.com/FRS417-DataScienceBiologists). I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Life History
Aren't mammals fun? Let's load up some more mammal data. This will be life history data for mammals. The [data](http://esapubs.org/archive/ecol/E084/093/) are from: *S. K. Morgan Ernest. 2003. Life history characteristics of placental non-volant mammals. Ecology 84:3402.*  


```r
life_history <- readr::read_csv("data/mammal_lifehistories_v2.csv")
```

```
## Parsed with column specification:
## cols(
##   order = col_character(),
##   family = col_character(),
##   Genus = col_character(),
##   species = col_character(),
##   mass = col_double(),
##   gestation = col_double(),
##   newborn = col_double(),
##   weaning = col_double(),
##   `wean mass` = col_double(),
##   AFR = col_double(),
##   `max. life` = col_double(),
##   `litter size` = col_double(),
##   `litters/year` = col_double()
## )
```

Rename some of the variables. Notice that I am replacing the old `life_history` data.

```r
life_history <- 
  life_history %>% 
  dplyr::rename(
          genus        = Genus,
          wean_mass    = `wean mass`,
          max_life     = `max. life`,
          litter_size  = `litter size`,
          litters_yr   = `litters/year`
          )
```

1. Explore the data using the method that you prefer. Below, I am using a new package called `skimr`. If you want to use this, make sure that it is installed.

```r
install.packages("skimr",repos="https://cran.rstudio.com")
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/03/zj74q9xx4h9600dtn2mv48jh0000gn/T//RtmpzFIHvM/downloaded_packages
```


```r
library("skimr")
```


```r
life_history %>% 
  skimr::skim()
```

```
## Skim summary statistics
##  n obs: 1440 
##  n variables: 13 
## 
## ── Variable type:character ──────────────────────────────────────────────────────────────────────────────────────
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## ── Variable type:numeric ────────────────────────────────────────────────────────────────────────────────────────
##     variable missing complete    n      mean         sd   p0  p25     p50
##          AFR       0     1440 1440   -408.12     504.97 -999 -999    2.5 
##    gestation       0     1440 1440   -287.25     455.36 -999 -999    1.05
##  litter_size       0     1440 1440    -55.63     234.88 -999    1    2.27
##   litters_yr       0     1440 1440   -477.14     500.03 -999 -999    0.38
##         mass       0     1440 1440 383576.72 5055162.92 -999   50  403.02
##     max_life       0     1440 1440   -490.26     615.3  -999 -999 -999   
##      newborn       0     1440 1440   6703.15   90912.52 -999 -999    2.65
##    wean_mass       0     1440 1440  16048.93   5e+05    -999 -999 -999   
##      weaning       0     1440 1440   -427.17     496.71 -999 -999    0.73
##      p75          p100     hist
##    15.61     210       ▆▁▁▁▁▁▇▁
##     4.5       21.46    ▃▁▁▁▁▁▁▇
##     3.83      14.18    ▁▁▁▁▁▁▁▇
##     1.15       7.5     ▇▁▁▁▁▁▁▇
##  7009.17       1.5e+08 ▇▁▁▁▁▁▁▁
##   147.25    1368       ▇▁▁▃▂▁▁▁
##    98    2250000       ▇▁▁▁▁▁▁▁
##    10          1.9e+07 ▇▁▁▁▁▁▁▁
##     2         48       ▆▁▁▁▁▁▁▇
```

2. Run the code below. Are there any NA's in the data? Does this seem likely?

```r
life_history %>% 
  summarize(number_nas= sum(is.na(life_history)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1          0
```
No, there are no NAs, but does not seem likely.

3. Are there any missing data (NA's) represented by different values? How much and where? In which variables do we have the most missing data? Can you think of a reason why so much data are missing in this variable?

There are many missing data, which are represented by -999. 

```r
life_history2 <- 
  life_history %>% 
  na_if("-999")
life_history2
```

```
## # A tibble: 1,440 x 13
##    order family genus species   mass gestation newborn weaning wean_mass
##    <chr> <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>
##  1 Arti… Antil… Anti… americ… 4.54e4      8.13   3246.    3         8900
##  2 Arti… Bovid… Addax nasoma… 1.82e5      9.39   5480     6.5         NA
##  3 Arti… Bovid… Aepy… melamp… 4.15e4      6.35   5093     5.63     15900
##  4 Arti… Bovid… Alce… busela… 1.50e5      7.9   10167.    6.5         NA
##  5 Arti… Bovid… Ammo… clarkei 2.85e4      6.8      NA    NA           NA
##  6 Arti… Bovid… Ammo… lervia  5.55e4      5.08   3810     4           NA
##  7 Arti… Bovid… Anti… marsup… 3.00e4      5.72   3910     4.04        NA
##  8 Arti… Bovid… Anti… cervic… 3.75e4      5.5    3846     2.13        NA
##  9 Arti… Bovid… Bison bison   4.98e5      8.93  20000    10.7     157500
## 10 Arti… Bovid… Bison bonasus 5.00e5      9.14  23000.    6.6         NA
## # … with 1,430 more rows, and 4 more variables: AFR <dbl>, max_life <dbl>,
## #   litter_size <dbl>, litters_yr <dbl>
```

```r
life_history2 %>% 
  summarize(number_nas= sum(is.na(life_history2)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1       4977
```

4. Compared to the `msleep` data, we have better representation among taxa. Produce a summary that shows the number of observations by taxonomic order.


```r
life_history2 %>% 
  group_by(order) %>% 
  summarize(total=n())
```

```
## # A tibble: 17 x 2
##    order          total
##    <chr>          <int>
##  1 Artiodactyla     161
##  2 Carnivora        197
##  3 Cetacea           55
##  4 Dermoptera         2
##  5 Hyracoidea         4
##  6 Insectivora       91
##  7 Lagomorpha        42
##  8 Macroscelidea     10
##  9 Perissodactyla    15
## 10 Pholidota          7
## 11 Primates         156
## 12 Proboscidea        2
## 13 Rodentia         665
## 14 Scandentia         7
## 15 Sirenia            5
## 16 Tubulidentata      1
## 17 Xenarthra         20
```


5. Mammals have a range of life histories, including lifespan. Produce a summary of lifespan in years by order. Be sure to include the minimum, maximum, mean, standard deviation, and total n.


```r
life_history2 %>% 
  group_by(order) %>% 
  summarize(min_lifespan=min(max_life,na.rm=TRUE),
            max_lifespan=max(max_life,na.rm=TRUE),
            mean_lifespan=mean(max_life,na.rm=TRUE),
            sd_lifespan=sd(max_life,na.rm=TRUE),
            total=n())
```

```
## # A tibble: 17 x 6
##    order          min_lifespan max_lifespan mean_lifespan sd_lifespan total
##    <chr>                 <dbl>        <dbl>         <dbl>       <dbl> <int>
##  1 Artiodactyla             81          732         248.         92.4   161
##  2 Carnivora                60          672         253.        113.    197
##  3 Cetacea                 156         1368         586.        332.     55
##  4 Dermoptera              210          210         210          NA       2
##  5 Hyracoidea              132          147         140.         10.6     4
##  6 Insectivora              14          156          46.2        34.8    91
##  7 Lagomorpha               72          216         108.         46.2    42
##  8 Macroscelidea            36          105          68.2        28.7    10
##  9 Perissodactyla          252          600         426.        122.     15
## 10 Pholidota               240          240         240          NA       7
## 11 Primates                106          726         309.        132.    156
## 12 Proboscidea             840          960         900          84.9     2
## 13 Rodentia                 12          420          83.8        63.6   665
## 14 Scandentia               32          149         106.         64.6     7
## 15 Sirenia                 150          876         518         363.      5
## 16 Tubulidentata           288          288         288          NA       1
## 17 Xenarthra               108          480         255.        119.     20
```

6. Let's look closely at gestation and newborns. Summarize the mean gestation, newborn mass, and weaning mass by order. Add a new column that shows mean gestation in years and sort in descending order. Which group has the longest mean gestation? What is the common name for these mammals?

```r
life_history2 %>% 
  group_by(order) %>% 
  summarize(mean_gestation=mean(gestation,na.rm=TRUE),
            mean_newborn=mean(newborn,na.rm=TRUE),
            mean_wean_mass=mean(wean_mass,na.rm=TRUE)) %>% 
  arrange(desc(mean_gestation, mean_newborn, mean_wean_mass)) %>% 
  mutate(mean_gestation_inyears=(mean_gestation/12))
```

```
## # A tibble: 17 x 5
##    order      mean_gestation mean_newborn mean_wean_mass mean_gestation_in…
##    <chr>               <dbl>        <dbl>          <dbl>              <dbl>
##  1 Proboscid…          21.3      99523.         600000               1.77  
##  2 Perissoda…          13.0      27015.         382191.              1.09  
##  3 Cetacea             11.8     343077.        4796125               0.983 
##  4 Sirenia             10.8      22878.          67500               0.9   
##  5 Hyracoidea           7.4        231.            500               0.617 
##  6 Artiodact…           7.26      7082.          51025.              0.605 
##  7 Tubuliden…           7.08      1734            6250               0.59  
##  8 Primates             5.47       287.           2115.              0.456 
##  9 Xenarthra            4.95       314.            420               0.412 
## 10 Carnivora            3.69      3657.          21020.              0.308 
## 11 Pholidota            3.63       276.           2006.              0.302 
## 12 Dermoptera           2.75        35.9           NaN               0.229 
## 13 Macroscel…           1.91        24.5           104.              0.159 
## 14 Scandentia           1.63        12.8           102.              0.136 
## 15 Rodentia             1.31        35.5           135.              0.109 
## 16 Lagomorpha           1.18        57.0           715.              0.0979
## 17 Insectivo…           1.15         6.06           33.1             0.0958
```
Proboscidea has the longest mean gestation. The common name for these mammals is elephants!


## Push your final code to [GitHub](https://github.com/FRS417-DataScienceBiologists)
Make sure that you push your code into the appropriate folder. Also, be sure that you have check the `keep md` file in the knit preferences.
