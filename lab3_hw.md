---
title: "Lab 3 Homework"
author: "Tricia Nguyen"
date: "Winter 2019"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our [GitHub repository](https://github.com/FRS417-DataScienceBiologists). I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.

## Load the libraries

```r
library(tidyverse)
```

For this assignment we are going to work with a large dataset from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. The data are messy, so for this assignment I am going to provide some help. The code I use will likely be useful in the future so keep it handy. First, load the data. **Read** the error message.  


```r
fisheries <- readr::read_csv("FAO_1950to2012_111914.csv") 
```

```
## Warning: Duplicated column names deduplicated: 'Species (ISSCAAP group)'
## => 'Species (ISSCAAP group)_1' [4], 'Species (ASFIS species)' => 'Species
## (ASFIS species)_1' [5], 'Species (ASFIS species)' => 'Species (ASFIS
## species)_2' [6]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `Species (ISSCAAP group)` = col_double(),
##   `Fishing area (FAO major fishing area)` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

1. Do you see any potential problems with the column names? Does the error message now make more sense?  
*Column names are duplicated so R manipulated them to unique names*
The columns are all named "Species," which causes the system to get confused.

2. The `make.names()` command is helpful when there are issues with column names. Notice that although the names are still cumbersome, much of the problemtatic syntax is removed.

```r
names(fisheries) = make.names(names(fisheries), unique=T) #changes the column names
names(fisheries)
```

```
##  [1] "Country..Country."                    
##  [2] "Species..ASFIS.species."              
##  [3] "Species..ISSCAAP.group."              
##  [4] "Species..ISSCAAP.group._1"            
##  [5] "Species..ASFIS.species._1"            
##  [6] "Species..ASFIS.species._2"            
##  [7] "Fishing.area..FAO.major.fishing.area."
##  [8] "Measure..Measure."                    
##  [9] "X1950"                                
## [10] "X1951"                                
## [11] "X1952"                                
## [12] "X1953"                                
## [13] "X1954"                                
## [14] "X1955"                                
## [15] "X1956"                                
## [16] "X1957"                                
## [17] "X1958"                                
## [18] "X1959"                                
## [19] "X1960"                                
## [20] "X1961"                                
## [21] "X1962"                                
## [22] "X1963"                                
## [23] "X1964"                                
## [24] "X1965"                                
## [25] "X1966"                                
## [26] "X1967"                                
## [27] "X1968"                                
## [28] "X1969"                                
## [29] "X1970"                                
## [30] "X1971"                                
## [31] "X1972"                                
## [32] "X1973"                                
## [33] "X1974"                                
## [34] "X1975"                                
## [35] "X1976"                                
## [36] "X1977"                                
## [37] "X1978"                                
## [38] "X1979"                                
## [39] "X1980"                                
## [40] "X1981"                                
## [41] "X1982"                                
## [42] "X1983"                                
## [43] "X1984"                                
## [44] "X1985"                                
## [45] "X1986"                                
## [46] "X1987"                                
## [47] "X1988"                                
## [48] "X1989"                                
## [49] "X1990"                                
## [50] "X1991"                                
## [51] "X1992"                                
## [52] "X1993"                                
## [53] "X1994"                                
## [54] "X1995"                                
## [55] "X1996"                                
## [56] "X1997"                                
## [57] "X1998"                                
## [58] "X1999"                                
## [59] "X2000"                                
## [60] "X2001"                                
## [61] "X2002"                                
## [62] "X2003"                                
## [63] "X2004"                                
## [64] "X2005"                                
## [65] "X2006"                                
## [66] "X2007"                                
## [67] "X2008"                                
## [68] "X2009"                                
## [69] "X2010"                                
## [70] "X2011"                                
## [71] "X2012"
```

3. Let's rename the columns. Use `rename()` to adjust the names as follows. Double check to make sure the rename worked correctly. Make sure to replace the old fisheries object with a new one so you can keep the column names.
+ country     = Country..Country.  
+ commname    = Species..ASFIS.species.  
+ sciname     = Species..ASFIS.species._2  
+ spcode      = Species..ASFIS.species._1  
+ spgroup     = Species..ISSCAAP.group.  
+ spgroupname = Species..ISSCAAP.group._1  
+ region      = Fishing.area..FAO.major.fishing.area.  
+ unit        = Measure..Measure.  


```r
fisheries_tidy <- fisheries %>% 
  dplyr::rename(
    country = Country..Country.,
    commname = Species..ASFIS.species.,
    sciname = Species..ASFIS.species._2,
    spcode = Species..ASFIS.species._1,
    spgroupname = Species..ISSCAAP.group._1,
    region = Fishing.area..FAO.major.fishing.area.,
    unit = Measure..Measure.)
```


4. Are these data tidy? Why or why not, and, how do you know?
The data is not tidy because values are not sorted into clean columns under specific names.

5. We need to tidy the data using `gather()`. The code below will not run because it is commented (#) out. I have added a bit of code that will prevent you from needing to type in each year from 1950-2012 but you need to complete the remainder `QQQ` and remove the `#`.

```r
fisheries_tidy <- fisheries %>% 
  dplyr::rename(
    country = Country..Country.,
    commname = Species..ASFIS.species.,
    sciname = Species..ASFIS.species._2,
    spcode = Species..ASFIS.species._1,
    spgroupname = Species..ISSCAAP.group._1,
    region = Fishing.area..FAO.major.fishing.area.,
    unit = Measure..Measure.) %>% 
  gather(num_range('X',1950:2012), key='year', value='catch')
fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname Species..ISSCAA… spgroupname spcode sciname region
##    <chr>   <chr>               <dbl> <chr>       <chr>  <chr>    <dbl>
##  1 Albania Angelsh…               38 Sharks, ra… 10903… Squati…     37
##  2 Albania Atlanti…               36 Tunas, bon… 17501… Sarda …     37
##  3 Albania Barracu…               37 Miscellane… 17710… Sphyra…     37
##  4 Albania Blue an…               45 Shrimps, p… 22802… Ariste…     37
##  5 Albania Blue wh…               32 Cods, hake… 14804… Microm…     37
##  6 Albania Bluefish               37 Miscellane… 17020… Pomato…     37
##  7 Albania Bogue                  33 Miscellane… 17039… Boops …     37
##  8 Albania Caramot…               45 Shrimps, p… 22801… Penaeu…     37
##  9 Albania Catshar…               38 Sharks, ra… 10801… Scylio…     37
## 10 Albania Common …               57 Squids, cu… 32102… Sepia …     37
## # … with 1,114,586 more rows, and 3 more variables: unit <chr>,
## #   year <chr>, catch <chr>
```

6. Use `glimpse()` to look at the categories of the variables. Pay particular attention to `year` and `catch`. What do you notice?  


```r
glimpse(fisheries_tidy)
```

```
## Observations: 1,114,596
## Variables: 10
## $ country                 <chr> "Albania", "Albania", "Albania", "Albani…
## $ commname                <chr> "Angelsharks, sand devils nei", "Atlanti…
## $ Species..ISSCAAP.group. <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, …
## $ spgroupname             <chr> "Sharks, rays, chimaeras", "Tunas, bonit…
## $ spcode                  <chr> "10903XXXXX", "1750100101", "17710001XX"…
## $ sciname                 <chr> "Squatinidae", "Sarda sarda", "Sphyraena…
## $ region                  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, …
## $ unit                    <chr> "Quantity (tonnes)", "Quantity (tonnes)"…
## $ year                    <chr> "X1950", "X1950", "X1950", "X1950", "X19…
## $ catch                   <chr> "...", "...", "...", "...", "...", "..."…
```
For year, many of the values are the same and all start with X. For catch, all I see are ellipses.


7. From question 6 you should see that there are a lot of entries that are missing. In R, these are referred to as NA's but they can be coded in different ways by the scientists in a given study. In order to make the data tidy, we need to deal with them. As a preview to our next lab, run the following code by removing the `#`. It removes the 'X' from the years and changes the `catch` column from a character into a numeric. This forces the blank entries to become NAs. The error "NAs introduced by coercion" indicates their replacement.

```r
fisheries_tidy <- fisheries_tidy %>% 
  mutate(
    year= as.numeric(str_replace(year, 'X', '')), #remove the X from year
    catch= as.numeric(str_replace(catch, c(' F','...','-'), replacement = '')) #replace character strings with NA
    )
```

```
## Warning in evalq(as.numeric(str_replace(catch, c(" F", "...", "-"),
## replacement = "")), : NAs introduced by coercion
```

```r
fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname Species..ISSCAA… spgroupname spcode sciname region
##    <chr>   <chr>               <dbl> <chr>       <chr>  <chr>    <dbl>
##  1 Albania Angelsh…               38 Sharks, ra… 10903… Squati…     37
##  2 Albania Atlanti…               36 Tunas, bon… 17501… Sarda …     37
##  3 Albania Barracu…               37 Miscellane… 17710… Sphyra…     37
##  4 Albania Blue an…               45 Shrimps, p… 22802… Ariste…     37
##  5 Albania Blue wh…               32 Cods, hake… 14804… Microm…     37
##  6 Albania Bluefish               37 Miscellane… 17020… Pomato…     37
##  7 Albania Bogue                  33 Miscellane… 17039… Boops …     37
##  8 Albania Caramot…               45 Shrimps, p… 22801… Penaeu…     37
##  9 Albania Catshar…               38 Sharks, ra… 10801… Scylio…     37
## 10 Albania Common …               57 Squids, cu… 32102… Sepia …     37
## # … with 1,114,586 more rows, and 3 more variables: unit <chr>,
## #   year <dbl>, catch <dbl>
```

8. Are the data tidy? Why?  
The data is tidy because each variable has its own place and the variables are sorted under specific column names. 

9. You are a fisheries scientist studying cephalopod catch during 2008-2012. Identify the top five consumers (by country) of cephalopods (don't worry about species for now). Restrict the data frame only to our variables of interest.


```r
fisheries_tidy <- fisheries_tidy %>% 
  select(country, commname, spgroupname, catch) %>% 
  filter(spgroupname == "Squids, cuttlefishes, octopuses") %>% 
  arrange(desc(catch))
fisheries_tidy
```

```
## # A tibble: 46,935 x 4
##    country commname              spgroupname                      catch
##    <chr>   <chr>                 <chr>                            <dbl>
##  1 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 576900
##  2 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 573800
##  3 Peru    Jumbo flying squid    Squids, cuttlefishes, octopuses 533414
##  4 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 478000
##  5 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 477000
##  6 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 465200
##  7 China   Various squids nei    Squids, cuttlefishes, octopuses 462981
##  8 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 460100
##  9 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 455800
## 10 Japan   Japanese flying squid Squids, cuttlefishes, octopuses 444189
## # … with 46,925 more rows
```
The top five consumers of cephalopods are Japan, Peru, China, Argentina, and Chile.

10. Let's be more specific. Who consumes the most `Common cuttlefish`? Store this as a new object `cuttle`.

```r
cuttlefish <- fisheries_tidy %>% 
  select(country, commname, catch) %>% 
  filter(commname == "Common cuttlefish") %>% 
  arrange(desc(catch))
cuttlefish
```

```
## # A tibble: 1,323 x 3
##    country commname          catch
##    <chr>   <chr>             <dbl>
##  1 France  Common cuttlefish 13217
##  2 France  Common cuttlefish 12966
##  3 France  Common cuttlefish  8076
##  4 Tunisia Common cuttlefish  7995
##  5 Tunisia Common cuttlefish  7717
##  6 Greece  Common cuttlefish  7200
##  7 Tunisia Common cuttlefish  7188
##  8 Tunisia Common cuttlefish  6622
##  9 Tunisia Common cuttlefish  6479
## 10 Tunisia Common cuttlefish  6404
## # … with 1,313 more rows
```
France (along with Tunisia, Greece, Spain, and Turkey) consumes the most cuttlefish.

## Push your final code to [GitHub](https://github.com/FRS417-DataScienceBiologists)
Make sure that you push your code into the appropriate folder. Also, be sure that you have check the `keep md` file in the knit preferences.
