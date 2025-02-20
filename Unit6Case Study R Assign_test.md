---
title: "Untitled"
author: "Marvin Scott"
date: "June 15, 2016"
output: 
md_document:
    variant: markdown_github
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

### **Introduction**
The objective of this document is to illustrate via R programming  the data munging and analytical processes invloved between datasets listed below

#####        1) GDP Rank
#####        2) Ed Stats

### **Dowload Process:-**

#####        1) GDP Rank

```{r echo=TRUE}
######LOAD FILE INTO WORKSPACE AFTER SAVING INTO DIRECTORY 
gross <-read.csv("GDP.csv", stringsAsFactors = FALSE, skip= 5, nrows = 231,  header  =FALSE)

```

#####        2) Ed Stats

```{r echo=TRUE}
######LOAD FILE INTO WORKSPACE AFTER SAVING INTO DIRECTORY 
edstat <-read.csv("Edstats_Country.csv", stringsAsFactors = TRUE,   header  =TRUE)

```

### **Tidying Process**
#####        1) GDP Rank


```{r echo=TRUE}
######NAME VARIBLES
names(gross)<- c("COUNTRYCODE", "RANKING", "JUNK1", "ECONOMY","US_DOLLARS_MILLIONS", "JUNK2", "JUNK3", "JUNK4", "JUNK5", "JUNK6")

######NAME vARIBLES
names(edstat)[2]<- "SHORTNAME"
names(edstat)[9]<- "INCOMEGROUP"
names(edstat)[1]<- "COUNTRYCODE"

```

```{r echo=TRUE}
######LOAD PACKAGES
library(plyr)
library(dplyr)

```

```{r echo=TRUE}

######SPECIFIY VARIABLE SELECTION REQ'D FOR ANALYSIS
grossx<-select(gross, COUNTRYCODE,RANKING, ECONOMY , US_DOLLARS_MILLIONS)

######NAME vARIBLES
names(edstat)[2]<- "SHORTNAME"
names(edstat)[9]<- "INCOMEGROUP"
names(edstat)[1]<- "COUNTRYCODE"

```


```{r echo=TRUE}

######SPECIFIY VARIABLE SELECTION REQ'D FOR ANALYSIS
grossx<-select(gross, COUNTRYCODE,ECONOMY ,RANKING,  US_DOLLARS_MILLIONS)


######SPECIFIY VARIABLE SELECTION REQ'D FOR ANALYSIS
edstat_gdp<-select(edstat, COUNTRYCODE,INCOMEGROUP, SHORTNAME)

```

```{r echo=TRUE}

######CHANGE DATA TYPE TO "FACTOR"
grossx$COUNTRYCODE<-as.factor(grossx$COUNTRYCODE)

######CHANGE DATA TYPE TO "FACTOR"
grossx$ECONOMY<-as.factor(grossx$ECONOMY)
```


```{r echo=TRUE}

######CHECK MISSING VALUES/NAs
summary(grossx)

######CHECK MISSING VALUES/NAs
str(edstat_gdp)
summary(edstat_gdp)

```

### **Merging Process For 1) GDP Rank & 2)Ed Stats DATASETS**

```{r echo=TRUE}

######MERGE DATA BY "**COUNTRYCODE**"
mergedata1<-merge(x=edstat_gdp, y= grossx , by = "COUNTRYCODE", all= TRUE)
head(mergedata1)

```
