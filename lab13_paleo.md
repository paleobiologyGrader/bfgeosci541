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

5) When expressed as a percentage of gamma diversity, beta diversity still increases. However, it is a significantly smaller increase than the direct comparison. The higher beta diversity in the Silurian can be equated to higher faunal turnover between communities, therefore implying that Silurian faunal communities were less cosmopolitan than those from the Ordovician. There may be a tradeoff between alpha and beta diversity across such large landscapes, as alpha diversity decreased by a similar percentage (more in terms of proportion, however, than beta diversity). 
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

6) Using percentages does mask the disparity between the original numbers, as well as hiding the magnitude of increase (or lack thereof) in the direct comparison. While ratios and other statistics have their usefulness, sometimes simple numbers work just as well.....????????

##Problem set two
1)
```R
LatePermian <- downloadPBDB("Animalia", StartInterval="Guadalupian", StopInterval="Lopingian")
EarlyTriassic <- downloadPBDB("Animalia", StartInterval="Induan", StopInterval="Ladinian")
LateCretaceous <- downloadPBDB("Animalia", StartInterval="Santonian", StopInterval="Maastrichtian")
EarlyPaleogene <- downloadPBDB("Animalia", StartInterval="Danian", StopInterval="Lutetian")
LatePermian <- cleanRank(LatePermian, "genus")
EarlyTriassic <- cleanRank(EarlyTriassic, "genus")
LateCretaceous <- cleanRank(LateCretaceous, "genus")
EarlyPaleogene <- cleanRank(EarlyPaleogene, "genus")
LatePermian <- constrainAges(LatePermian, Epochs)
EarlyTriassic <- constrainAges(EarlyTriassic, Epochs)
LateCretaceous <- constrainAges(LateCretaceous, Epochs)
EarlyPaleogene <- constrainAges(EarlyPaleogene, Epochs)
LatePermian <- macrostratMatch(LatePermian)
EarlyTriassic <- macrostratMatch(EarlyTriassic)
LateCretaceous <- macrostratMatch(LateCretaceous)
EarlyPaleogene <- macrostratMatch(EarlyPaleogene)
PermianMatrix <- abundanceMatrix(LatePermian, SampleDefinition="unit_name", TaxonRank="genus")
TriassicMatrix <- abundanceMatrix(EarlyTriassic, SampleDefinition="unit_name", TaxonRank="genus")
CretaceousMatrix <- abundanceMatrix(LateCretaceous, SampleDefinition="unit_name", TaxonRank="genus")
PaleogeneMatrix <- abundanceMatrix(EarlyPaleogene, SampleDefinition="unit_name", TaxonRank="genus")
PermianMatrix <- cullMatrix(PermianMatrix, 2, 10)
TriassicMatrix <- cullMatrix(TriassicMatrix, 2, 10)
CretaceousMatrix <- cullMatrix(CretaceousMatrix, 2, 10)
PaleogeneMatrix <- cullMatrix(PaleogeneMatrix, 2, 10)
```

2)
```R

```
