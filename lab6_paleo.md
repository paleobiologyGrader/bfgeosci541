#Lab Exercise Six

##Problem Set 1
1) 
> length(DataPBDB$occurrence_no)-length(MacroPBDB$occurrence_no)

> [1] 25153

2) By default, because Macrostrat is only in North America currently, any occurrence outside of North America is dropped in the matching procedure. 

##Problem Set 2
1) using arrange{dplyr}
> order_rich <- data.frame(richness=apply(OrderMatrix, 1, specnumber))

> CandidateUnits <- c(as.character(arrange(order_rich, desc(richness))[1:10,]$names))

> CandidateUnits

> [1] "Chancellor"       "Kinzers Fm"       "Stephen Fm"       "Marjum Limestone"

> [5] "Wheeler Shale"    "Langston Fm"      "Parker Slate"     "Snowy Range Fm"  

> [9] "Weymouth Fm"      "Harkless Fm"

2)
> GenusFrequencies <- data.frame(genus_frequencies=apply(GenusMatrix, 2, sum))

3) 
> hist(GenusFrequencies)

4) Hollow curves!
> We are the hollow men

> We are the stuffed men

> Leaning together

> Headpiece filled with straw. Alas!

> Our dried voices, when

> We whisper together

> Are quiet and meaningless

> As wind in dry grass

> Or rats' feet over broken glass

> In our dry cellar
<br />
> Shape without form, shade without colour,

> Paralysed force, gesture without motion;
<br />
> Those who have crossed

> With direct eyes, to death's other Kingdom

> Remember us—if at all—not as lost

> Violent souls, but only

> As the hollow men

> The stuffed men.

5) 
> RareGenera <- subset(GenusFrequencies, genus_frequencies<=median(genus_frequencies))
