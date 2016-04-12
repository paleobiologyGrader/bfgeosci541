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
```
