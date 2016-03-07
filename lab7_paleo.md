2)
```
oldGenus <- DataPBDB %>% group_by(genus) %>% summarize(oldest = max(max_ma))
```
