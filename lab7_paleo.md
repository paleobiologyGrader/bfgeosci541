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
> maxOccurrences <- DataPBDB %>% group_by(genus) %>% summarize(max_occur=max(length(occurrence_no)))
> max(maxOccurrences$max_occur)
[1] 1916
```
