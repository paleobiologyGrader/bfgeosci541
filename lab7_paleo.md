2)
```
OldGenus <- DataPBDB %>% group_by(genus) %>% summarize(oldest=max(max_ma))
```
3)
```
YoungGenus <- DataPBDB %>% group_by(genus) %>% summarize(youngest=min(min_ma))
```
4)
```
maxOccurrence <- DataPBDB %>% group_by(genus) %>% summarize(max_occur=max(length(occurrence_no))) %>%
slice(which(.$max_occur==max(.$max_occur)))

maxOccurrence
Source: local data frame [1 x 2]

    genus max_occur
    (chr)     (int)
1 Anadara      1916
```
5) 66 million years, the whole of the Cenozoic.
```
data.frame(OldGenus[which(OldGenus$genus=="Anadara"),], YoungGenus[which(YoungGenus$genus=="Anadara"),]) %>%
select(genus, youngest, oldest) %>% mutate(difference = oldest - youngest, oldest=NULL, youngest=NULL)
    genus difference
1 Anadara         66
```

##Problem Set 2
1) To describe it from the inside out, a sample from the ```paleolng``` column of the ```Lucina``` genus data is being taken - with replacement - which has a length equal to the number of elements in ```paleolng```. The mean of the sample is subsequently taken, and in the case of ```ResampledMeans``` this whole process is repeated 1000 times.

2)
```
plot(density(ResampledMeans))
```
3) Using an arbitrary cutoff of 0.05 for similarity, the mean of ```ResampledMeans``` is indeed similar to the original mean of the data.
```
mean(ResampledMeans)-24.1997
[1] 0.04221836
```
4)
```
ResampledMeans <- sort(ResampledMeans, decreasing=FALSE)
```
5) The 2.5th and 97.5th percentiles correspond to the values in the sorted list at indices 25 and 975 respectively.
```
> ResampledMeans[25]
[1] 21.81826
> ResampledMeans[975]
[1] 26.2861
```
6) 95% of the data falls between those two x values, and by adding vertical lines at those points on the kernal density plot it is quite plain to see.

##Problem set 3
1) I would have to say it is likely that *Lucina* is still alive because 0.0 is the present, and negative numbers would mean extinction at some point in the future. 

2) 
```
estimateExtinction(Dallarca[,"min_ma"], 0.95)
Earliest   Latest 
 2.58800 -3.88749
```
3) Based purely on the confidence interval, it is *possible* that the genus is still extant today because we currently lie right in the middle of the two bounds.

4) The lower bound (2.58800) corresponds almost exactly to the younger bound for the last appearance according to the Encyclopedia of Life, given at 2.59 ma. So in this particular case it would make more sense to trust the fossil record over the confidence interval.

##Problem Set 4
1) Ecologically, this method is based on the assumption that community and population dynamics between and amongst species had no effect on where and when potentially fossilizable material would one day be deposited. Obviously that is an unfounded assumption. For example, if we were 200 million years in the future doing this analysis on human fossils, we wouldn't assume they are randomly distributed in time. There is constant flux in trade, interaction, and population flow happening between and within cities that would be taken into account when extrapolating so far into the past. Not to mention human interaction with the biosphere has caused irreparable change which would probably affect deposition of sediments and taphonomic processes.

2) Geologically, processes which affect the deposition of sediment should not be overlooked. Things such as recession and transgression of seas, geographical changes affecting sediment quantity and composition, as well as more stochastic processes such as orogeny and severe bouts of volcanic activity would all have huge impacts on how or if fossilizable material is preserved. 

##Problem Set 5
1) ```DataPBDB``` has 67,617 occurrences, and ```ExtantData``` has 59,096.
```
length(DataPBDB$occurrence_no) - length(ExtantData$occurrence_no)
[1] 8521
```
2) ```DataPBDB``` has 1,018 unique genera, ```ExtantData``` has 532. This constitutes 52.2% of all Cenozoic genera.
```
length(unique(DataPBDB$genus)) - length(unique(ExtantData$genus))
[1] 486
```
3)
```
YoungGenus <- ExtantData %>% group_by(genus) %>% summarize(youngest=min(min_ma))

OldGenus <- ExtantData %>% group_by(genus) %>% summarize(oldest=max(max_ma))

StratRange <- data.frame(OldGenus, YoungGenus) %>% select(genus, oldest, youngest) %>%
mutate(Range=oldest-youngest, oldest=NULL, youngest=NULL)
```
4)
```
YoungGenus[which(YoungGenus$youngest!=0),]
```
5) Created subsets of each genus before estimating the confidence intervals below. Genus *Aloides* only had one occurrence, which explains the inability of the function to find an upper range for the extinction age.
```
estimateExtinction(Scrobicularia[,"min_ma"], 0.95)
 Earliest    Latest 
  0.01170 -34.70966
estimateExtinction(Meiocardia[,"min_ma"], 0.95)
 Earliest    Latest 
 0.011700 -5.329574
estimateExtinction(Dimya[,"min_ma"], 0.95)
 Earliest    Latest 
 0.781000 -2.054688
estimateExtinction(Digitaria[,"min_ma"], 0.95)
 Earliest    Latest 
 0.781000 -3.761154
estimateExtinction(Cuspidaria[,"min_ma"], 0.95)
 Earliest    Latest 
2.5880000 0.7771965 
estimateExtinction(Arctica[,"min_ma"], 0.95)
 Earliest    Latest 
 0.011700 -1.799104 
estimateExtinction(Aloides[,"min_ma"], 0.95)
Earliest   Latest 
   5.333     -Inf 
estimateExtinction(Kurtiella[,"min_ma"], 0.95)
 Earliest    Latest 
  0.01170 -34.70966 
estimateExtinction(Gouldia[,"min_ma"], 0.95)
 Earliest    Latest 
 0.011700 -2.047386 
estimateExtinction(Acrosterigma[,"min_ma"], 0.95)
 Earliest    Latest 
 0.011700 -3.481128
``` 
