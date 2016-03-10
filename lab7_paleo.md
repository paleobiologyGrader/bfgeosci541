2)
```
oldGenus <- DataPBDB %>% group_by(genus) %>% summarize(oldest=max(max_ma))
```
3)
```
youngGenus <- DataPBDB %>% group_by(genus) %>% summarize(youngest=min(min_ma))
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
5) 66 million years
```
data.frame(oldGenus[which(oldGenus$genus=="Anadara"),], youngGenus[which(youngGenus$genus=="Anadara"),]) %>%
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
3)
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
1) Ecologically, this method is based on the assumption that community and population dynamics between and amongst species had no effect on where and when potentially fossilizable material would one day be deposited. Obviously that is an unfounded assumption. For example, if we were 200 million years in the future doing this analysis on human fossils, we wouldn't assume they are randomly distributed in time. There is constant flux in trade, interaction, and population flow happening between and within cities that would be taken into account when extrapolating so far into the past. Not to mention human interaction with the biosphere has caused irreparable damage which would probably affect deposition of sediments and taphonomic processes.

2) Geologically 
