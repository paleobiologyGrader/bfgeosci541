#Triassic and Jurassic Macrostratigraphy
##Part one
###Problem set one
1)
```
TriassicUnits <- read.csv("https://macrostrat.org/api/units?interval_name=Triassic&format=csv&response=long")
```

2)838 observations were downloaded, corresponding to 838 Triassic rock units.
```
str(TriassicUnits)
```

3) The major composition of the first 10 observations is igneous and metamorphic rock. Sedimentary rock is the best for fossil preservation.
```
TriassicUnits$lith[1:10]
```

4) ```b_age``` gives the starting age, ```t_age``` represents the truncation age, and both are given in millions of years before present.

5) While all 10 units started in the Triassic, every one of them also ranges beyond the Triassic to the Cretaceous.

###Problem set two
1) 713 units were downloaded this time.
```
TriassicUnits <- read.csv("https://macrostrat.org/api/units?interval_name=Triassic&format=csv&lith_class=sedimentary")
```

2) Restricted data to 604 units.
```
Periods <- downloadTime(Timescale="international periods")
TriassicUnits %<>% filter(b_age<=Periods$b_age[6], t_age>=Periods$t_age[6])
```

3)
```
MacStrat <- read.csv("https://macrostrat.org/api/units?format=csv&lith_class=sedimentary")
macroSort <- function(MacStrat, Periods) {
Output <- array(data=NA, dim=nrow(Periods), dimnames=list(Periods[,"name"]))
for (i in 1:nrow(Periods)) {
Output[i] <- nrow(MacStrat %>% filter(t_age>=Periods$t_age[i], b_age<=Periods$b_age[i]))
}
return(Output)
}

```

4)
```
UnitFreqs <- macroSort(MacStrat, Periods)[4:11]
UnitFreqs
   Cretaceous      Jurassic      Triassic       Permian Carboniferous      Devonian      Silurian    Ordovician 
         4588           998           604           903          3020          2059          1205          2161

```

5) The number of Triassic units lies about 1.15 standard deviations away from the mean.
```
dimnames(UnitFreqs) <- NULL
mean(UnitFreqs[-3])
[1] 2133.429
sd(UnitFreqs[-3])
[1] 1321.764
(2133.429-604)/1321.764
[1] 1.157112
```

6) Considering the fact that most data on a distribution falls within two standard deviations of the mean, I would have to say that the Triassic does not have a statistically lower number of units than the others included in the sample.

7) Even when considering both the Jurassic and Triassic as outliers, the result is similar. In this case the mean is shifted to a higher value, but so is the standard deviation. This time the Triassic lies 1.28 standard deviations away from the mean. And again, based on this value I cannot be certain (statistically) that the Triassic has a lower number of units than the other periods.
```
mean(UnitFreqs[c(-2,-3)])
[1] 2322.667
sd(UnitFreqs[c(-2,-3)])
[1] 1340.022
(2322.667-604)/1340.022
[1] 1.282566
```

##Part two
###Problem set three
1)
```
URL <- "https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
GotURL <- getURL(URL)
AllMap <- readOGR(GotURL, "OGRGeoJSON", verbose=FALSE)
plot(AllMap)
```

2)
```
URL <- "https://macrostrat.org/api/columns?format=geojson_bare&age_top=242&age_bottom=252&project_id=1"
GotURL <- getURL(URL)
Induan <- readOGR(GotURL, "OGRGeoJSON", verbose=FALSE)
plot(Induan, add=TRUE, col="#B051A5")
```

3)
```
InAnimal <- downloadPBDB("Animalia", StartInterval="Induan", StopInterval="Anisian")
points(InAnimal$lng, InAnimal$lat, pch=20, col="red")
```

4)
```
URL <- "https://macrostrat.org/api/columns?format=geojson_bare&age_top=252&age_bottom=260&project_id=1"
GotURL <- getURL(URL)
Loping <- readOGR(GotURL, "OGRGeoJSON", verbose=FALSE)
windows()
plot(AllMap)
plot(Loping, add=TRUE, col="#FBA794")
```

5)
```
LoAnimal <- downloadPBDB("Animalia", StartInterval="Lopingian", StopInterval="Lopingian")
points(LoAnimal$lng, LoAnimal$lat, pch=20)
```

6) While there was a drop between the Lopingian and the Induan-Anisian in the amount of sedimentary units, the Induan-Anisian sediments show a large increase in the percentage of sedimentary units with reported fossils in them.

