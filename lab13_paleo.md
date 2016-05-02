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

6) Using percentages does mask the disparity between the original numbers, as well as hiding the magnitude of increase (or lack thereof) in the direct comparison. The absolute difference in diversity between the two intervals is also lost.

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
PermianMatrix <- presenceMatrix(LatePermian, SampleDefinition="unit_name", TaxonRank="genus")
TriassicMatrix <- presenceMatrix(EarlyTriassic, SampleDefinition="unit_name", TaxonRank="genus")
CretaceousMatrix <- presenceMatrix(LateCretaceous, SampleDefinition="unit_name", TaxonRank="genus")
PaleogeneMatrix <- presenceMatrix(EarlyPaleogene, SampleDefinition="unit_name", TaxonRank="genus")
PermianMatrix <- cullMatrix(PermianMatrix, 2, 10)
TriassicMatrix <- cullMatrix(TriassicMatrix, 2, 10)
CretaceousMatrix <- cullMatrix(CretaceousMatrix, 2, 10)
PaleogeneMatrix <- cullMatrix(PaleogeneMatrix, 2, 10)
```

2)
```R
traditionalAlpha(PermianMatrix)
[1] 57.63636
traditionalAlpha(TriassicMatrix)
[1] 35.15385
traditionalAlpha(CretaceousMatrix)
[1] 57.96875
traditionalAlpha(PaleogeneMatrix)
[1] 52.85
beta(PermianMatrix)
[1] 253.3636
beta(TriassicMatrix)
[1] 122.8462
beta(CretaceousMatrix)
[1] 717.0312
beta(PaleogeneMatrix)
[1] 978.15
gamma(PermianMatrix)
[1] 311
gamma(TriassicMatrix)
[1] 158
gamma(CretaceousMatrix)
[1] 775
gamma(PaleogeneMatrix)
[1] 1031
```

3)
```R
traditionalAlpha(PermianMatrix)/gamma(PermianMatrix)
[1] 0.1853259
traditionalAlpha(TriassicMatrix)/gamma(TriassicMatrix)
[1] 0.2224927
traditionalAlpha(CretaceousMatrix)/gamma(CretaceousMatrix)
[1] 0.07479839
traditionalAlpha(PaleogeneMatrix)/gamma(PaleogeneMatrix)
[1] 0.05126091
beta(PermianMatrix)/gamma(PermianMatrix)
[1] 0.8146741
beta(TriassicMatrix)/gamma(TriassicMatrix)
[1] 0.7775073
beta(CretaceousMatrix)/gamma(CretaceousMatrix)
[1] 0.9252016
beta(PaleogeneMatrix)/gamma(PaleogeneMatrix)
[1] 0.9487391
```

4) When not measured as a percentage, alpha diversity decreases across both extinction boundaries.

5) When measured as a percentage, alpha diversity increases across the End Permian extinction, but still shows a decrease in the Late Cretaceous extinction event.

##Problem set three
1)
```R
LateOrdovician <- downloadPBDB("Animalia", "Sandbian", "Hirnantian")
EarlySilurian <- downloadPBDB("Animalia", "Llandovery", "Wenlock")
LateOrdovician <- cleanRank(LateOrdovician, "genus")
EarlySilurian <- cleanRank(EarlySilurian, "genus")
LateOrdovician <- constrainAges(LateOrdovician, Epochs)
EarlySilurian <- constrainAges(EarlySilurian, Epochs)
LateOrdovician <- macrostratMatch(LateOrdovician)
EarlySilurian <- macrostratMatch(EarlySilurian)
OrdovicianMatrix <- abundanceMatrix(LateOrdovician, SampleDefinition="unit_name", TaxonRank="genus")
SilurianMatrix <- abundanceMatrix(EarlySilurian, SampleDefinition="unit_name", TaxonRank="genus")
PermianMatrix <- abundanceMatrix(LatePermian, SampleDefinition="unit_name", TaxonRank="genus")
TriassicMatrix <- abundanceMatrix(EarlyTriassic, SampleDefinition="unit_name", TaxonRank="genus")
CretaceousMatrix <- abundanceMatrix(LateCretaceous, SampleDefinition="unit_name", TaxonRank="genus")
PaleogeneMatrix <- abundanceMatrix(EarlyPaleogene, SampleDefinition="unit_name", TaxonRank="genus")
```

2) 
Gamma
```R
exp(diversity(colSums(OrdovicianMatrix), index="shannon"))
[1] 100.5137
exp(diversity(colSums(SilurianMatrix), index="shannon"))
[1] 273.3235
exp(diversity(colSums(PermianMatrix), index="shannon"))
[1] 210.0769
exp(diversity(colSums(TriassicMatrix), index="shannon"))
[1] 204.4873
exp(diversity(colSums(CretaceousMatrix), index="shannon"))
[1] 378.3011
exp(diversity(colSums(PaleogeneMatrix), index="shannon"))
[1] 517.0753
```
Alpha
```R
exp(mean(diversity(OrdovicianMatrix, index="shannon")))
[1] 10.96187
exp(mean(diversity(SilurianMatrix, index="shannon")))
[1] 10.89307
exp(mean(diversity(PermianMatrix, index="shannon")))
[1] 9.318572
exp(mean(diversity(TriassicMatrix, index="shannon")))
[1] 9.198214
exp(mean(diversity(CretaceousMatrix, index="shannon")))
[1] 7.69611
exp(mean(diversity(PaleogeneMatrix, index="shannon")))
[1] 13.97237
```
Beta
```R
exp(diversity(colSums(OrdovicianMatrix), index="shannon"))-exp(mean(diversity(OrdovicianMatrix, index="shannon")))
[1] 89.55187
exp(diversity(colSums(SilurianMatrix), index="shannon"))-exp(mean(diversity(SilurianMatrix, index="shannon")))
[1] 262.4305
exp(diversity(colSums(PermianMatrix), index="shannon"))-exp(mean(diversity(PermianMatrix, index="shannon")))
[1] 200.7583
exp(diversity(colSums(TriassicMatrix), index="shannon"))-exp(mean(diversity(TriassicMatrix, index="shannon")))
[1] 195.2891
exp(diversity(colSums(CretaceousMatrix), index="shannon"))-exp(mean(diversity(CretaceousMatrix, index="shannon")))
[1] 370.605
exp(diversity(colSums(PaleogeneMatrix), index="shannon"))-exp(mean(diversity(PaleogeneMatrix, index="shannon")))
[1] 503.1029
```

3) All values for gamma diversity will be equal to one for the purposes of this question.

Alpha
```R
exp(mean(diversity(OrdovicianMatrix, index="shannon")))/exp(diversity(colSums(OrdovicianMatrix), index="shannon"))
[1] 0.1090584
exp(mean(diversity(SilurianMatrix, index="shannon")))/exp(diversity(colSums(SilurianMatrix), index="shannon"))
[1] 0.03985414
exp(mean(diversity(PermianMatrix, index="shannon")))/exp(diversity(colSums(PermianMatrix), index="shannon"))
[1] 0.04435791
exp(mean(diversity(TriassicMatrix, index="shannon")))/exp(diversity(colSums(TriassicMatrix), index="shannon"))
[1] 0.04498184
exp(mean(diversity(CretaceousMatrix, index="shannon")))/exp(diversity(colSums(CretaceousMatrix), index="shannon"))
[1] 0.02034387
exp(mean(diversity(PaleogeneMatrix, index="shannon")))/exp(diversity(colSums(PaleogeneMatrix), index="shannon"))
[1] 0.02702192
```

Beta
```R
(exp(diversity(colSums(OrdovicianMatrix), index="shannon"))-exp(mean(diversity(OrdovicianMatrix, index="shannon"))))/exp(diversity(colSums(OrdovicianMatrix), index="shannon"))
[1] 0.8909416
(exp(diversity(colSums(SilurianMatrix), index="shannon"))-exp(mean(diversity(SilurianMatrix, index="shannon"))))/exp(diversity(colSums(SilurianMatrix), index="shannon"))
[1] 0.9601459
(exp(diversity(colSums(PermianMatrix), index="shannon"))-exp(mean(diversity(PermianMatrix, index="shannon"))))/exp(diversity(colSums(PermianMatrix), index="shannon"))
[1] 0.9556421
(exp(diversity(colSums(TriassicMatrix), index="shannon"))-exp(mean(diversity(TriassicMatrix, index="shannon"))))/exp(diversity(colSums(TriassicMatrix), index="shannon"))
[1] 0.9550182
(exp(diversity(colSums(CretaceousMatrix), index="shannon"))-exp(mean(diversity(CretaceousMatrix, index="shannon"))))/exp(diversity(colSums(CretaceousMatrix), index="shannon"))
[1] 0.9796561
(exp(diversity(colSums(PaleogeneMatrix), index="shannon"))-exp(mean(diversity(PaleogeneMatrix, index="shannon"))))/exp(diversity(colSums(PaleogeneMatrix), index="shannon"))
[1] 0.9729781
```

4) When not measured as a percentage, alpha diversity decreases after the End Ordovician and End Permian, but increases following the End Cretaceous extinction. I simply looked at the numbers from question 2 in this problem set, no code necessary.

5) Using question 3 for this, alpha diversity increase is seen following the End Permian and End Cretaceous extinctions. However, using this method results in a substantial decrease in alpha diversity after the End Ordovician event.

##Problem four
From the above problem sets, I can find no definitive evidence that would lead to a conclusion of beta diversity increase or decrease following mass extinctions. I therefore have to conclude that beta diversity has other factors through which it is influenced, moreso than mass extinction events.
