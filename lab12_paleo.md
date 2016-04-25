#Selectivity patterns of mass extinctions
##Problem set one
1)
```R
TriassicSynapsids <- downloadPBDB("Synapsida", StartInterval="Anisian", StopInterval="Rhaetian")
TriassicSynapsids <- cleanRank(TriassicSynapsids, "genus")
TriassicDiapsids <- downloadPBDB("Diapsida", StartInterval="Anisian", StopInterval="Rhaetian")
TriassicDiapsids <- cleanRank(TriassicDiapsids, "genus")
PTSynapsids <- downloadPBDB("Synapsida", StartInterval="Jurassic", StopInterval="Neogene")
PTSynapsids <- cleanRank(PTSynapsids, "genus")
PTDiapsids <- downloadPBDB("Diapsida", StartInterval="Jurassic", StopInterval="Neogene")
PTDiapsids <- cleanRank(PTDiapsids, "genus")
```

2) 389 Triassic Diapsid and 116 Synapsid genera are present.
```R
length(unique(TriassicDiapsids$genus))
[1] 389
length(unique(TriassicSynapsids$genus))
[1] 116
```

3)
```R
DiapsidSurvivors <- intersect(unique(TriassicDiapsids[,"genus"]), unique(PTDiapsids[,"genus"]))
length(DiapsidSurvivors)
[1] 37
DiapsidVictims <- setdiff(unique(TriassicDiapsids[,"genus"]), unique(PTDiapsids[,"genus"]))
length(DiapsidVictims)
[1] 352
SynapsidSurvivors <- intersect(unique(TriassicSynapsids[,"genus"]), unique(PTSynapsids[,"genus"]))
length(SynapsidSurvivors)
[1] 9
SynapsidVictims <- setdiff(unique(TriassicSynapsids[,"genus"]), unique(PTSynapsids[,"genus"]))
length(SynapsidVictims)
[1] 107
```

4)
```R
SynapsidGenera <- unique(TriassicSynapsids$genus)
DiapsidGenera <- unique(TriassicDiapsids$genus)
SynapsidOdds <- (length(SynapsidSurvivors)/length(SynapsidGenera))/(length(SynapsidVictims)/length(SynapsidGenera))
DiapsidOdds <- (length(DiapsidSurvivors)/length(DiapsidGenera))/(length(DiapsidVictims)/length(DiapsidGenera))
OddsRatio <- DiapsidOdds/SynapsidOdds
OddsRatio
[1] 1.249684
log(OddsRatio)
[1] 0.222891
```

5) Because the lower limit is negative, we cannot be certain Diapsids had a statistically significant advantage in survival over Synapsids across the Triassic/Jurassic transition.
```R
StandardError <- sqrt(1/length(SynapsidSurvivors) + 1/length(SynapsidVictims) + 1/length(DiapsidSurvivors) + 1/length(DiapsidVictims))
UpperLimit <- log(OddsRatio) + (1.96*StandardError)
UpperLimit
[1] 0.9828172
LowerLimit <- log(OddsRatio) - (1.96*StandardError)
LowerLimit
[1] -0.5370353
```

##Problem set two
1)
```R
Triassic <- downloadPBDB(c("Diapsida", "Synapsida"), "Anisian", "Rhaetian")
Triassic <- cleanRank(Triassic, "genus")
PostTriassic <- downloadPBDB(c("Diapsida", "Synapsida"), "Jurassic", "Neogene")
PostTriassic <- cleanRank(PostTriassic, "genus")
```

2)
```R
TriassicLat <- tapply(Triassic[,"paleolat"], Triassic[,"genus"], mean)
```

3)
```R
TriassicSurvivors <- subset(Triassic, Triassic[,"genus"]%in%unique(PostTriassic[,"genus"])==TRUE)
TriassicSurvivors <- unique(TriassicSurvivors[,"genus"])
str(TriassicSurvivors)
chr [1:46] "Clevosaurus" "Grallator" "Rhynchosauroides" ...
TriassicVictims <- subset(Triassic, Triassic[,"genus"]%in%unique(PostTriassic[,"genus"])!=TRUE)
TriassicVictims <- unique(TriassicVictims[,"genus"])
str(TriassicVictims)
chr [1:459] "Icarosaurus" "Rutiodon" "Kuehneosuchus" "Kuehneosaurus" ...
```

4) These objects (```TriassicSyn``` and ```TriassicDi```) will return lists of the unique Triassic Synapsids and Diapsids, respectively.
```R
TriassicSyn <- subset(Triassic, Triassic[,"genus"]%in%TriassicSynapsids[,"genus"]==TRUE)
TriassicSyn <- unique(TriassicSyn$genus)
str(TriassicSyn)
chr [1:116] "Therioherpeton" "Adelobasileus" "Massetognathus" ...
TriassicDi <- subset(Triassic, Triassic[,"genus"]%in%TriassicDiapsids[,"genus"]==TRUE)
TriassicDi <- unique(TriassicDi$genus)
str(TriassicDi)
chr [1:389] "Icarosaurus" "Rutiodon" "Kuehneosuchus" "Kuehneosaurus" ...
```

5) Because the estimate is 0.0007725, and also because that row does not have a significance code, I conclude that genus survival across the Triassic/Jurassic boundary cannot be predicted by its mean latitude.
```R
TJVictims <- array(0, dim=length(TriassicVictims), dimnames=list(TriassicVictims))
FinalMatrix <- merge(TriassicLat, TJVictims, all=TRUE, by="row.names")
FinalMatrix <- transform(FinalMatrix, row.names=Row.names, Row.names=NULL)
colnames(FinalMatrix) <- c("MeanLatitudes", "Survivor/Victim")
FinalMatrix[is.na(FinalMatrix[,"Survivor/Victim"]),] <- 1
Regression <- glm(FinalMatrix[,"Survivor/Victim"] ~ FinalMatrix[,"MeanLatitudes"], family="binomial")
summary(Regression)

Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[, 
    "MeanLatitudes"], family = "binomial")

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-0.4474  -0.4411  -0.4385  -0.4308   2.1889  

Coefficients:
                                 Estimate Std. Error z value Pr(>|z|)    
(Intercept)                    -2.3009122  0.1547326  -14.87   <2e-16 ***
FinalMatrix[, "MeanLatitudes"]  0.0007725  0.0051555    0.15    0.881    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 308.10  on 504  degrees of freedom
Residual deviance: 308.08  on 503  degrees of freedom
AIC: 312.08

Number of Fisher Scoring iterations: 5
```

Extra Credit: Again the result is not significant. Whether the genus was a Synapsid or a Diapsid held no sway over survival across the T/J boundary. And looking at the AIC difference between the two, I would hypothesize that the simpler linear regression explains more of the data. 
```R
Di <- array(0, dim=length(TriassicDi), dimnames=list(TriassicDi)
FinalMatrix1 <- merge(TriassicLat, TJVictims, all=TRUE, by="row.names")
FinalMatrix2 <- merge(TriassicLat, Di, all=TRUE, by="row.names")
FinalMatrix1 <- transform(FinalMatrix1, row.names=Row.names, Row.names=NULL)
FinalMatrix2 <- transform(FinalMatrix2, row.names=Row.names, Row.names=NULL)
colnames(FinalMatrix1) <- c("MeanLatitudes", "Survivor/Victim")
colnames(FinalMatrix2) <- c("MeanLatitudes", "Synapsid/Diapsid")
FinalMatrix1[is.na(FinalMatrix1[,"Survivor/Victim"]),] <- 1
FinalMatrix2[is.na(FinalMatrix2[,"Synapsid/Diapsid"]),] <- 1
FinalMatrix <- merge(FinalMatrix1, FinalMatrix2, all=TRUE, by="row.names")
FinalMatrix <- transform(FinalMatrix, row.names=Row.names, Row.names=NULL)
colnames(FinalMatrix) <- c("MeanLatitudes", "Survivor/Victim", "Synapsid/Diapsid")
MRegression <- glm(FinalMatrix[,"Survivor/Victim"] ~ FinalMatrix[,"MeanLatitudes"] + FinalMatrix[,"Synapsid/Diapsid"], family="binomial")
summary(MRegression)

Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[, 
    "MeanLatitudes"] + FinalMatrix[, "Synapsid/Diapsid"], family = "binomial")

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-0.4492  -0.4477  -0.4466  -0.4029   2.2603  

Coefficients:
                                    Estimate Std. Error z value Pr(>|z|)    
(Intercept)                       -2.2533359  0.1740487 -12.947   <2e-16 ***
FinalMatrix[, "MeanLatitudes"]     0.0001619  0.0052887   0.031    0.976    
FinalMatrix[, "Synapsid/Diapsid"] -0.2204787  0.3956189  -0.557    0.577    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 308.10  on 504  degrees of freedom
Residual deviance: 307.76  on 502  degrees of freedom
AIC: 313.76

Number of Fisher Scoring iterations: 5
```

