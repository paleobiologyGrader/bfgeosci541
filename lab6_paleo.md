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

4) A hollow curve.
> We are the hollow men
<br />
> We are the stuffed men
<br />
> Leaning together
<br />
> Headpiece filled with straw. Alas!
<br />
> Our dried voices, when
<br />
> We whisper together
<br />
> Are quiet and meaningless
<br />
> As wind in dry grass
<br />
> Or rats' feet over broken glass
<br />
> In our dry cellar

> Shape without form, shade without colour,
<br />
> Paralysed force, gesture without motion;

> Those who have crossed
<br />
> With direct eyes, to death's other Kingdom
<br />
> Remember us—if at all—not as lost
<br />
> Violent souls, but only
<br />
> As the hollow men
<br />
> The stuffed men.

> -T.S. Eliot

5) 
> RareGenera <- subset(GenusFrequencies, genus_frequencies<=median(genus_frequencies))

##Problem Set 3
1)
> CandidateMatrix <- GenusMatrix[c(CandidateUnits),]

2) Due to the fact I saved GenusFrequencies as a data frame (therefore RareGenera is a data frame) I had to alter the function to look for names of the CandidateMatrix in **rownames** of the RareGenera, instead of **names**. The four stratigraphic units I included below as most likely to qualify as Lagerstätten contain the highest percentages of rare genera (at least according to the list I made), one of the qualities of Lagerstätten.

```
PercentShared<- apply(CandidateMatrix,1,percentRare,RareGenera)
PercentShared
Chancellor  Marjum Limestone   Weymouth Fm  Harkless Fm 
0.5714286        0.3559322      0.6764706     0.4137931
```

3) The Marjum formation in the House Range of Utah contains exceptional trilobite and echinoderm fossils as well as worms and other soft bodied organisms in certain shale beds, reminiscent of the level of preservation at the Burgess Shale. 
