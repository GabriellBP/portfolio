---
layout: post
title: Exploratory Data Analysis Introduction with R
description: >
  An introduction of commands to data analysis in R.
image: /assets/img/blog/data-science/RStudio-Ball.png
noindex: true
---

For this post I will use the [Forest Fires in Brazil](https://www.kaggle.com/gustavomodelli/forest-fires-in-brazil/) dataset, 
don't forget to download it. _Forest Fires in Brazil_ is a dataset that report the number of forest fires in Brazil 
divided by states. The series comprises the period of approximately 10 years (1998 to 2017), and include 5 features: 
year, state, month, number and date.

To run the codes I've used [RStudio](https://rstudio.com/).

## Importing data

To import the data and assign it to a variable, you can use the Import Dataset tool of RStudio or execute the following code:

```r
# Importing and assigning data to a variable
dataset = read.csv(paste("your_path","forest_fires_in_brazil.csv", sep=""))
```

To have a initial view of the dataset, we can use the `summary()` command

```R
summary(dataset)
```
>
```R
       year         state              month               number     
   Min.   :1998   Length:6454        Length:6454        Min.   :  0.0  
   1st Qu.:2002   Class :character   Class :character   1st Qu.:  3.0  
   Median :2007   Mode  :character   Mode  :character   Median : 24.0  
   Mean   :2007                                         Mean   :108.3  
   3rd Qu.:2012                                         3rd Qu.:113.0  
   Max.   :2017                                         Max.   :998.0  
       date          
   Length:6454     
   Class :character  
   Mode  :character
 ```

In the output of the command above, we can see some important information, like the name of the features, the type of 
the data in them, the median and the mean value in the numeric features, the length, among other things. All of this 
information may be helpful during data engineering.

## Exploring some commands

To have another kind of visualization we can use diverse commands, with the command `str()` per example, we can see the 
the total number of observations and variables that we have on the dataset, we can see the name of the features and its 
type, besides some values.

```R
str(dataset)
```
>
```R
   'data.frame':	6454 obs. of  5 variables:
    $ year  : int  1998 1999 2000 2001 2002 2003 2004 2005 2006 2007 ...
    $ state : chr  "Acre" "Acre" "Acre" "Acre" ...
    $ month : chr  "Janeiro" "Janeiro" "Janeiro" "Janeiro" ...
    $ number: num  0 0 0 0 0 10 0 12 4 0 ...
    $ date  : chr  "1998-01-01" "1999-01-01" "2000-01-01" "2001-01-01" ...
 ```

With the command `glimpse()`, we can see the same information of the `str()` command, but in another organization's way. 

_Obs.: to use `Glimpse()`, you have to install the **dplyr library**, for that, you can use the command `install.packages("dplyr")`
then import it using `library(dplyr)`_

```R
library(dplyr)
glimpse(dataset)
```
>
```R
   Observations: 6,454
   Variables: 5
   $ year   <int> 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, ...
   $ state  <chr> "Acre", "Acre", "Acre", "Acre", "Acre", "Acre", "Acre", ...
   $ month  <chr> "Janeiro", "Janeiro", "Janeiro", "Janeiro", "Janeiro", ...
   $ number <dbl> 0, 0, 0, 0, 0, 10, 0, 12, 4, 0, 0, 0, 1, 0, 0, 0, 0, 1, 12, ...
   $ date   <chr> "1998-01-01", "1999-01-01", "2000-01-01", "2001-01-01", ...
 ```

With the command `table()`, we can see how many observations there are for an specified feature. If we wanna see how many observations
we have in each year, we use the following code: 

```R
table(dataset$year)
```
>
```R
   1998 1999 2000 2001 2002 2003 2004 2005 2006 2007 2008 2009 2010 2011 2012 2013 
    324  324  324  324  324  324  324  324  324  324  324  324  324  324  324  324 
   2014 2015 2016 2017 
    324  324  324  298 
 ```

And if we wanna see the concentration of forest fires per state? To that we can do:

```R
table(dataset$year)
```
>
```R
        Acre          Alagoas            Amapa         Amazonas 
         239              240              239              239 
       Bahia            Ceara Distrito Federal   Espirito Santo 
         239              239              239              239 
       Goias         Maranhao      Mato Grosso     Minas Gerais 
         239              239              478              239 
        Pará          Paraiba       Pernambuco             Piau 
         239              478              239              239 
         Rio         Rondonia          Roraima   Santa Catarina 
         717              239              239              239 
    Sao Paulo          Sergipe        Tocantins 
         239              239              239  
 ```

With this kind of visualization we can infer, just looking, that in our data, Rio have the major part of forest fires 
and that over the years, Brazil has almost the same number of forest fires.

And if we wanna see all the features for just the last year in the Acre state? We can do this using the `filter()` command:

```R
last_year_data = filter(dataset, year == 2017 & state == "Acre")
str(last_year_data)
```
>
```R
    'data.frame':	11 obs. of  5 variables:
     $ year  : int  2017 2017 2017 2017 2017 2017 2017 2017 2017 2017 ...
     $ state : chr  "Acre" "Acre" "Acre" "Acre" ...
     $ month : chr  "Janeiro" "Fevereiro" "Março" "Abril" ...
     $ number: num  0 1 0 1 10 ...
     $ date  : chr  "2017-01-01" "2017-01-01" "2017-01-01" "2017-01-01" ...
 ```

Therefore, we can only see the specified data and observe that there are only eleven observations in this condition.

## Conclusion
Visualizing the data and exploring it is very important and is the first thing we need to do before we start making some
adjustments to the data and running machine learning models. For this, we need to know the tools we have available and 
thus find out which one is most useful in each case. 

