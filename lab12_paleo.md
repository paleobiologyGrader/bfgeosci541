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
