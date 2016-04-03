#The migration of paleocontinents
###Problem set 1
1) Modern North America is West of its Cretaceous position.

2) This code is plotting ModernMap and adding it (```add=TRUE```) to an existing plot. The ```col``` argument takes a color specification (in this case an rgb value for red, at an opacity of 0.33), ```lty``` takes any one of a number of line types specified by an integer, and the ```add``` argument, as mentioned already, adds to a preexisting plot without creating an entirely new one.

3)```AlbianMap <- downloadPaleogeography(Age=110)```

4) ```plot(AlbianMap, col=rgb(0,1,0,0.33), lty=0, add=TRUE)```

5) In the Eastern Hemisphere, more movement North and South than East and West is visible.

6) In the Western Hemisphere, more Westward movement is visible than Northern and Southern movement.

###Problem set 2
1)
```
PalEo <- downloadPaleogeography(Age=56)
plot(PalEo, col=rgb(0,0,1,0.5), lty=0)
```

```
Anthozoa <- downloadPBDB("Anthozoa", StartInterval="Paleocene", StopInterval="Eocene")
```
3) 2,847 occurrences were downloaded.

4) There are 26 columns. Occurrence number has an obvious meaning, it merely references the corresponding occurrence for each observation of the 25 remaining variables. Record type is the type of observation being returned, and in every observation of this data frame it has the value of occurrence (occ). ```reid_no``` denotes the reidentification column, and only contains a value if the occurrence was reidentified at some point. ```flags``` will only have a value (of R) if there is a more recent identification of the occurrence, and it will be empty for most. ```collection_no``` tells us what collection each occurrence belongs to. ```accepted_name```,  ```accepted_rank```, and ```accepted_no``` differ from ```identified_name```, ```identified_rank```, and ```identified_no``` only in that identified categories may be of a dubious or ambiguous nature. the ```difference``` column provides the reasons for any disparity between them. If ```late_interval``` is also given, ```early_interval``` corresponds to the beginning of the geologic time range of the occurrence. If ```late_interval``` is not present, it just means the geologic time range and not the beginning of the range. ```max_ma``` and ```min_ma``` correspond to the early and late bounds, respectively, of the geologic time range of the occurrence in millions of years. 

5)
```
points(Anthozoa$paleolng, Anthozoa$paleolat, col="red", cex=0.5)
```
6)
