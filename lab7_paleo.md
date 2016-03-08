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
5) The 2.5th and 97.5th percentiles correspond to the values at indices 25 and 975 respectively.
```
> ResampledMeans[25]
[1] 21.81826
> ResampledMeans[975]
[1] 26.2861
```
6) 95% of the data falls between those two x values, and by adding vertical lines at those points on the kernal density plot it is quite plain to see.
