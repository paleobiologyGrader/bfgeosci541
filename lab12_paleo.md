#Selectivity patterns of mass extinctions
##Problem set one
1)
```
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
```
length(unique(TriassicDiapsids$genus))
[1] 389
length(unique(TriassicSynapsids$genus))
[1] 116
```

3)
```
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
```
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
```
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
```
Triassic <- downloadPBDB(c("Diapsida", "Synapsida"), "Anisian", "Rhaetian")
Triassic <- cleanRank(Triassic, "genus")
PostTriassic <- downloadPBDB(c("Diapsida", "Synapsida"), "Jurassic", "Neogene")
PostTriassic <- cleanRank(PostTriassic, "genus")
```

2)
```
TriassicLat <- tapply(Triassic[,"paleolat"], Triassic[,"genus"], mean)
```

3)
```
TriassicSurvivors <- subset(Triassic, Triassic[,"genus"]%in%unique(PostTriassic[,"genus"])==TRUE)
TriassicSurvivors <- unique(TriassicSurvivors[,"genus"])
str(TriassicSurvivors)
chr [1:46] "Clevosaurus" "Grallator" "Rhynchosauroides" ...
TriassicVictims <- subset(Triassic, Triassic[,"genus"]%in%unique(PostTriassic[,"genus"])!=TRUE)
TriassicVictims <- unique(TriassicVictims[,"genus"])
str(TriassicVictims)
chr [1:459] "Icarosaurus" "Rutiodon" "Kuehneosuchus" "Kuehneosaurus" ...
```

4)
```
TriassicSyn <- subset(Triassic, Triassic[,"genus"]%in%TriassicSynapsids[,"genus"]==TRUE)
TriassicDi <- subset(Triassic, Triassic[,"genus"]%in%TriassicDiapsids[,"genus"]==TRUE)
```

5) Because the estimate for the slope is 0.0007725, and also because that row does not have a significance code, I conclude that genus survival across the Triassic/Jurassic boundary cannot be predicted by its mean latitude.
```
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

Extra Credit


