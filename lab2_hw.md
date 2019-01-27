---
title: "Lab 2 Homework"
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
library("tidyverse")
```

```
## ── Attaching packages ──────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
## ✔ readr   1.3.1     ✔ forcats 0.3.0
```

```
## ── Conflicts ─────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

## Mammals Sleep
For this assignment, we are going to use built-in data on mammal sleep patterns.  


```r
msleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl>
##  1 Chee… Acin… carni Carn… lc                  12.1      NA        NA    
##  2 Owl … Aotus omni  Prim… <NA>                17         1.8      NA    
##  3 Moun… Aplo… herbi Rode… nt                  14.4       2.4      NA    
##  4 Grea… Blar… omni  Sori… lc                  14.9       2.3       0.133
##  5 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667
##  6 Thre… Brad… herbi Pilo… <NA>                14.4       2.2       0.767
##  7 Nort… Call… carni Carn… vu                   8.7       1.4       0.383
##  8 Vesp… Calo… <NA>  Rode… <NA>                 7        NA        NA    
##  9 Dog   Canis carni Carn… domesticated        10.1       2.9       0.333
## 10 Roe … Capr… herbi Arti… lc                   3        NA        NA    
## # … with 73 more rows, and 3 more variables: awake <dbl>, brainwt <dbl>,
## #   bodywt <dbl>
```

1. From which publication are these data taken from? Don't do an internet search; show the code that you would use to find out in R.


```r
?msleep
```


These data are taken from a framework published in the Proceedings of the National Academy of Sciences by V.M. Savage and G.B. West.

2. Provide some summary information about the data to get you started; feel free to use the functions that you find most helpful.


```r
summary(msleep)
```

```
##      name              genus               vore          
##  Length:83          Length:83          Length:83         
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##     order           conservation        sleep_total      sleep_rem    
##  Length:83          Length:83          Min.   : 1.90   Min.   :0.100  
##  Class :character   Class :character   1st Qu.: 7.85   1st Qu.:0.900  
##  Mode  :character   Mode  :character   Median :10.10   Median :1.500  
##                                        Mean   :10.43   Mean   :1.875  
##                                        3rd Qu.:13.75   3rd Qu.:2.400  
##                                        Max.   :19.90   Max.   :6.600  
##                                                        NA's   :22     
##   sleep_cycle         awake          brainwt            bodywt        
##  Min.   :0.1167   Min.   : 4.10   Min.   :0.00014   Min.   :   0.005  
##  1st Qu.:0.1833   1st Qu.:10.25   1st Qu.:0.00290   1st Qu.:   0.174  
##  Median :0.3333   Median :13.90   Median :0.01240   Median :   1.670  
##  Mean   :0.4396   Mean   :13.57   Mean   :0.28158   Mean   : 166.136  
##  3rd Qu.:0.5792   3rd Qu.:16.15   3rd Qu.:0.12550   3rd Qu.:  41.750  
##  Max.   :1.5000   Max.   :22.10   Max.   :5.71200   Max.   :6654.000  
##  NA's   :51                       NA's   :27
```


```r
str(msleep)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	83 obs. of  11 variables:
##  $ name        : chr  "Cheetah" "Owl monkey" "Mountain beaver" "Greater short-tailed shrew" ...
##  $ genus       : chr  "Acinonyx" "Aotus" "Aplodontia" "Blarina" ...
##  $ vore        : chr  "carni" "omni" "herbi" "omni" ...
##  $ order       : chr  "Carnivora" "Primates" "Rodentia" "Soricomorpha" ...
##  $ conservation: chr  "lc" NA "nt" "lc" ...
##  $ sleep_total : num  12.1 17 14.4 14.9 4 14.4 8.7 7 10.1 3 ...
##  $ sleep_rem   : num  NA 1.8 2.4 2.3 0.7 2.2 1.4 NA 2.9 NA ...
##  $ sleep_cycle : num  NA NA NA 0.133 0.667 ...
##  $ awake       : num  11.9 7 9.6 9.1 20 9.6 15.3 17 13.9 21 ...
##  $ brainwt     : num  NA 0.0155 NA 0.00029 0.423 NA NA NA 0.07 0.0982 ...
##  $ bodywt      : num  50 0.48 1.35 0.019 600 ...
```

```r
head(msleep)
```

```
## # A tibble: 6 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl>
## 1 Chee… Acin… carni Carn… lc                  12.1      NA        NA    
## 2 Owl … Aotus omni  Prim… <NA>                17         1.8      NA    
## 3 Moun… Aplo… herbi Rode… nt                  14.4       2.4      NA    
## 4 Grea… Blar… omni  Sori… lc                  14.9       2.3       0.133
## 5 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667
## 6 Thre… Brad… herbi Pilo… <NA>                14.4       2.2       0.767
## # … with 3 more variables: awake <dbl>, brainwt <dbl>, bodywt <dbl>
```

3. Make a new data frame focused on body weight, but be sure to indicate the common name and genus of each mammal. Sort the data in descending order by body weight.


```r
msleep %>% 
  select(name, order, bodywt) %>% 
  arrange(desc(bodywt))
```

```
## # A tibble: 83 x 3
##    name                 order          bodywt
##    <chr>                <chr>           <dbl>
##  1 African elephant     Proboscidea     6654 
##  2 Asian elephant       Proboscidea     2547 
##  3 Giraffe              Artiodactyla     900.
##  4 Pilot whale          Cetacea          800 
##  5 Cow                  Artiodactyla     600 
##  6 Horse                Perissodactyla   521 
##  7 Brazilian tapir      Perissodactyla   208.
##  8 Donkey               Perissodactyla   187 
##  9 Bottle-nosed dolphin Cetacea          173.
## 10 Tiger                Carnivora        163.
## # … with 73 more rows
```


4. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. For our study, we are interested in body weight and sleep total Make two new data frames (large and small) based on these parameters. Sort the data in descending order by body weight.

# Small

```r
msleep %>% 
  select(name, order, bodywt) %>% 
  arrange(desc(bodywt)) %>% 
  filter(bodywt <= 1)
```

```
## # A tibble: 36 x 3
##    name                      order           bodywt
##    <chr>                     <chr>            <dbl>
##  1 African giant pouched rat Rodentia         1    
##  2 Arctic ground squirrel    Rodentia         0.92 
##  3 Tenrec                    Afrosoricida     0.9  
##  4 European hedgehog         Erinaceomorpha   0.77 
##  5 Squirrel monkey           Primates         0.743
##  6 Guinea pig                Rodentia         0.728
##  7 Desert hedgehog           Erinaceomorpha   0.55 
##  8 Owl monkey                Primates         0.48 
##  9 Chinchilla                Rodentia         0.42 
## 10 Thick-tailed opposum      Didelphimorphia  0.37 
## # … with 26 more rows
```
# Large

```r
msleep %>% 
  select(name, order, bodywt) %>% 
  arrange(desc(bodywt)) %>% 
  filter(bodywt >= 200)
```

```
## # A tibble: 7 x 3
##   name             order          bodywt
##   <chr>            <chr>           <dbl>
## 1 African elephant Proboscidea     6654 
## 2 Asian elephant   Proboscidea     2547 
## 3 Giraffe          Artiodactyla     900.
## 4 Pilot whale      Cetacea          800 
## 5 Cow              Artiodactyla     600 
## 6 Horse            Perissodactyla   521 
## 7 Brazilian tapir  Perissodactyla   208.
```

5. Let's try to figure out if large mammals sleep, on average, longer than small mammals. What is the average sleep duration for large mammals as we have defined them?


```r
msleep %>% 
  filter(bodywt >= 200) %>% 
  summarise(avg_sleep = mean(sleep_total))
```

```
## # A tibble: 1 x 1
##   avg_sleep
##       <dbl>
## 1       3.3
```

6. What is the average sleep duration for small mammals as we have defined them?


```r
msleep %>% 
  filter(bodywt <= 1) %>% 
  summarise(avg_sleep = mean(sleep_total))
```

```
## # A tibble: 1 x 1
##   avg_sleep
##       <dbl>
## 1      12.7
```


7. Make two new variables in the msleep data frame: 1. the proportion of rem sleep, and 2. body weight in grams.


```r
msleep %>% 
    mutate(rem_proportion = sleep_rem / sleep_total) %>%
    arrange(desc(rem_proportion))
```

```
## # A tibble: 83 x 12
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl>
##  1 Euro… Erin… omni  Erin… lc                  10.1       3.5       0.283
##  2 Thic… Lutr… carni Dide… lc                  19.4       6.6      NA    
##  3 Gian… Prio… inse… Cing… en                  18.1       6.1      NA    
##  4 Tree… Tupa… omni  Scan… <NA>                 8.9       2.6       0.233
##  5 Dog   Canis carni Carn… domesticated        10.1       2.9       0.333
##  6 Nort… Dide… omni  Dide… lc                  18         4.9       0.333
##  7 Pig   Sus   omni  Arti… domesticated         9.1       2.4       0.5  
##  8 Dese… Para… <NA>  Erin… lc                  10.3       2.7      NA    
##  9 Dome… Felis carni Carn… domesticated        12.5       3.2       0.417
## 10 East… Scal… inse… Sori… lc                   8.4       2.1       0.167
## # … with 73 more rows, and 4 more variables: awake <dbl>, brainwt <dbl>,
## #   bodywt <dbl>, rem_proportion <dbl>
```

```r
msleep %>% 
    mutate(bodywtgrams = bodywt * 1000) %>%
    arrange(desc(bodywtgrams))
```

```
## # A tibble: 83 x 12
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl>
##  1 Afri… Loxo… herbi Prob… vu                   3.3      NA        NA    
##  2 Asia… Elep… herbi Prob… en                   3.9      NA        NA    
##  3 Gira… Gira… herbi Arti… cd                   1.9       0.4      NA    
##  4 Pilo… Glob… carni Ceta… cd                   2.7       0.1      NA    
##  5 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667
##  6 Horse Equus herbi Peri… domesticated         2.9       0.6       1    
##  7 Braz… Tapi… herbi Peri… vu                   4.4       1         0.9  
##  8 Donk… Equus herbi Peri… domesticated         3.1       0.4      NA    
##  9 Bott… Turs… carni Ceta… <NA>                 5.2      NA        NA    
## 10 Tiger Pant… carni Carn… en                  15.8      NA        NA    
## # … with 73 more rows, and 4 more variables: awake <dbl>, brainwt <dbl>,
## #   bodywt <dbl>, bodywtgrams <dbl>
```

8. What are the top five mammals with the greatest proportion of rem sleep? Include their body weights for comparison.

The European hedgehog, thick-tailed opposum, giant armadillo, tree shrew, and dog have the greatest proportion of REM sleep among mammals.


```r
msleep %>% 
  mutate(rem_proportion = sleep_rem / sleep_total) %>%
  arrange(desc(rem_proportion)) %>% 
  select(name, bodywt, rem_proportion)
```

```
## # A tibble: 83 x 3
##    name                   bodywt rem_proportion
##    <chr>                   <dbl>          <dbl>
##  1 European hedgehog       0.77           0.347
##  2 Thick-tailed opposum    0.37           0.340
##  3 Giant armadillo        60              0.337
##  4 Tree shrew              0.104          0.292
##  5 Dog                    14              0.287
##  6 North American Opossum  1.7            0.272
##  7 Pig                    86.2            0.264
##  8 Desert hedgehog         0.55           0.262
##  9 Domestic cat            3.3            0.256
## 10 Eastern american mole   0.075          0.25 
## # … with 73 more rows
```

9. Which animals sleep at least 18 hours per day? Be sure to show the name, genus, order, and sleep total. Sort by order and sleep total.


```r
msleep %>% 
    select(name, genus, order, sleep_total) %>%
    arrange(order, sleep_total) %>% 
    filter(sleep_total >= 18)
```

```
## # A tibble: 5 x 4
##   name                   genus      order           sleep_total
##   <chr>                  <chr>      <chr>                 <dbl>
## 1 Big brown bat          Eptesicus  Chiroptera             19.7
## 2 Little brown bat       Myotis     Chiroptera             19.9
## 3 Giant armadillo        Priodontes Cingulata              18.1
## 4 North American Opossum Didelphis  Didelphimorphia        18  
## 5 Thick-tailed opposum   Lutreolina Didelphimorphia        19.4
```
The big brown bat, little brown bat, giant armadillo, North American opossum, and thick-tailed opposum sleep at least 18 hours a day.

## Push your final code to [GitHub](https://github.com/FRS417-DataScienceBiologists)
Make sure that you push your code into the appropriate folder. Also, be sure that you have check the `keep md` file in the knit preferences.
