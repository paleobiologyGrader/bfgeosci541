```
MacStrat <- read.csv("https://macrostrat.org/api/units?format=csv&lith_class=sedimentary")

Periods <- downloadTime(Timescale="international periods")

macroSort <- function(MacStrat, Periods) {
Output <- array(data=NA, dim=nrow(Periods), dimnames=list(Periods[,"name"]))
for (i in 1:nrow(Periods)) {
Output[i] <- nrow(MacStrat %>% filter(t_age>=Periods$t_age[i], b_age<=Periods$b_age[i]))
}
return(Output)
}

macroSort(MacStrat, Periods)
   Quaternary       Neogene     Paleogene    Cretaceous      Jurassic      Triassic       Permian Carboniferous      Devonian  
         3750          3339          3790          4588           998           604           903          3020          2059 
   Silurian    Ordovician     
       1205          2161 
   Cambrian     Ediacaran    Cryogenian        Tonian       Stenian      Ectasian     Calymmian    Statherian     Orosirian    
       1518           154            75            55            46            39           109            38            87 
   Rhyacian      Siderian       
         43             9 

```
