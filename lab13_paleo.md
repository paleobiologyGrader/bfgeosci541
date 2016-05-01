#Diversity Partioning Across Mass Extinction Boundaries
##Problem set one
1) These generic richness numbers represent gamma diversity for the Ordovician and Silurian, respectively.
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

2) These average biodiversities across stratigraphic units represent alpha diversities for the Ordovician and Silurian in the additive diversity partioning scheme. 
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

3) The differences between the above results gives the beta diversity for the Ordovician and Silurian. 
```R
ncol(OrdovicianMatrix) - mean(specnumber(OrdovicianMatrix))
[1] 184.3947
ncol(SilurianMatrix) - mean(specnumber(SilurianMatrix))
[1] 380.2083

```
alternatively
```R
beta(OrdovicianMatrix)
[1] 184.3947
beta(SilurianMatrix)
[1] 380.2083
```

4) All diversity measures (alpha, beta, and gamma) increase from the Ordovician to the Silurian. Alpha increases from 26.6 to 42.7, beta from 184.3 to 380.2, and gamma from 211 to 423.

5) When expressed as a percentage of gamma diversity, beta diversity still increases. However, it is a significantly smaller increase than the direct comparison. The higher beta diversity in the Silurian can be equated to higher faunal turnover between communities, therefore implying that Silurian faunal communities were less cosmopolitan than those from the Ordovician.
```R
traditionalAlpha(OrdovicianMatrix)/gamma(OrdovicianMatrix)
[1] 0.1260913
traditionalAlpha(SilurianMatrix)/gamma(SilurianMatrix)
[1] 0.1011623
beta(OrdovicianMatrix)/gamma(OrdovicianMatrix)
[1] 0.8739087
beta(SilurianMatrix)/gamma(SilurianMatrix)
[1] 0.8988377
```

6)
