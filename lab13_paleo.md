#Diversity Partioning Across Mass Extinction Boundaries
##Problem set one
1)
```R
ncol(OrdovicianMatrix)
[1] 211
ncol(SilurianMatrix)
[1] 423
```
alternatively
```R
source("https://raw.githubusercontent.com/aazaff/paleobiologyDatabase.R/master/partitionDiversity.R")
gamma(OrdovicianMatrix)
[1] 211
gamma(SilurianMatrix)
[1] 423
```

2)
```R
library(vegan)
mean(specnumber(OrdovicianMatrix))
[1] 26.60526
mean(specnumber(SilurianMatrix))
[1] 42.79167
```
alternatively
```R
traditionalAlpha(OrdovicianMatrix)
[1] 26.60526
traditionalAlpha(SilurianMatrix)
[1] 42.79167
```

3)
```R
ncol(OrdovicianMatrix) - mean(specnumber(OrdovicianMatrix))
[1] 184.3947
ncol(SilurianMatrix) - mean(specnumber(SilurianMatrix))
[1] 380.2083

```
alternatively
```R
beta(SilurianMatrix)
[1] 184.3947
beta(SilurianMatrix)
[1] 380.2083
```

