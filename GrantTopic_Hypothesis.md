###Introduction
(899 of 1000)
Explanations of global trilobite biodiversity decine range from active displacement by brachiopod dominated environments to paleocontinental movement and its differing effects on various taxonomic ranks (Harper et al 2015; Westrop and Adrain 2001). These include change in the depth of seas, freshwater circulation, and ocean flux patterns (DeVries and Primeau 2011; Balseiro and Waisfeld 2013). Regardless of these potentially confounding effects, trilobite familial abundance change over the Proteozoic was strongly linked to the rate of contemporaneous brachiopod radiation. Primarily through the use of paleocoordinate data, modeling inward (establishment) or outward (extirpation) familial flux by geoplate between epochs will be possible. A secondary goal will be to adapt Jackson and Sax’s concepts on delayed extinction debts and immigration credits (2010) to the analysis of geoplate flux. 

###Justification
Addresses how rate of overturn of faunal communities leads to long-term/permanent regional biodiversity change
No single model incorporating brachiopod and trilobite biodiversity change over geologic time in the literature
Could provide new method for modeling community interaction dynamics on a geologic timescale by utilizing gradient analysis
Societal: could also provide novel methods for prediction of the effects of biodiversity change on modern habitats/communities

###Research Plan
Construct and clean datasets for brachiopods and trilobites from Cambrian – Permian
Do a soft cull of the cleaned datasets
Match each dataset to internationally recognized epochs/stages
Create family presence/absence data tables for each geoplate in each epoch/stage for both brachiopods and trilobites
Make gradients (vector fields) for each epoch/stage; magnitude=total trilobite richness of geoplate, direction=ratio of brachiopod family geoplate richness/trilobite family geoplate richness (<1=trilobite dominated, >1=brachiopod dominated, 1=no dominance)
Analyze differences between epoch/stage  flux; change in vector direction = change in familial dominance between clades, change in vector magnitude = change in trilobite richness 
Finally, look at the data to see if brachiopods or trilobites are acting to delay or accelerate the others’ extirpation/colonization
Look for relationship between persistence through time of a clade and initial family density of that clade in each geoplate
If both extirpation of trilobites (decrease in magnitude) and immigration of brachiopods (positive change in slope) are slow (small changes), then the incumbents are probably limiting establishment capability of brachiopods
If both are fast (large changes), then the new competitors are likely accelerating extirpation of the incumbents

maybe
```
flux through orientable surfaces defined at each epoch by the planar distributions of brachiopod and trilobite first differences...
  hard to do in R
  MATLAB?
  thickness defined by rock package thickness might be possible but data and time intensive
  or surfaces defined by paleocontinent shape/position relying on paleo maps created for each stage in R
 ```
 ```
Emigration vs immigration effects on biodiversity change
  Tabulate adjacent geoplates by stage; find outward/inward flux for each geoplate between stages
  Could limit to brachiopods/trilobites
  We already know that immigration/emigration is inherently related to biodiversity, but conceivably one is more influential than the   other

 ```
 ```
Does circulation of species in fossil record (simulation Andrew showed us) around continents over geologic time correspond to continental/tectonic circulation rates
 ```
 ```
 Extend Jackson and Sax 2010 to delayed extinction debt and immigration credit to brachiopod geoplate flux by stage, with the strength of the forcing events as amount of introduction/extirpation of trilobites to a specific plate (i.e. nonzero, positive or negative trilobite species flux since previous stage)
 ```



Harper, D.A.T., Zhan, R., and Jin, J. "The Great Ordovician Biodiversification Event: Reviewing two decades of research on diversity's big bang illustrated by mainly brachiopod data." *Palaeoworld* (2015) 24.1-2: 75-85. doi:10.1016/j.palwor.2015.03.003

Westrop, S.R., and Adrain, J.M. "Sampling at the species level: Impact of spatial biases on diversity gradients." *Geology* (2001) 29.10: 903-906. doi:10.1130/0091-7613(2001)​029<0903:SATSLI>​2.0.CO;2

DeVries, T., Primeau, F. "Dynamically and Observationally Constrained Estimates of Water-Mass Distributions and Ages in the Global Ocean." *American Meteorological Society* (2011) 41: 2381-2401. doi:10.1175/JPO-D-10-05011.1

Balseiro, D., Waisfeld, B.G. "Ecological instability in Upper Cambrian-Lower Ordovician trilobite communities from Northwestern Argentina." *Paleogeography, Paleoclimatology, Paleoecology* (2013) 370: 64-76. doi:10.1016/j.palaeo.2012.11.019

Jackson, S.T. and Sax, D.F. “Balancing biodiversity in a changing environment: extinction debt, immigration credit, and species turnover.” *Trends in Ecology & Evolution* (2010) 25.3: 153-160. doi:10.1016/j.tree.2009.10.001

Connolly, S.R. and Miller, A.I. “Global Ordovician faunal transitions in the marine benthos: proximate causes.” *Paleobiology* (2001) 27.4: 779-795. doi:10.1666/0094-8373(2001)027<0779:GOFTIT>2.0.CO;2

Zhang, Z., Robson, S.P., Emig, C., and Shu, D. “Early Cambrian radiation of brachiopods: A perspective from South China.” *Gonwana Research* (2008) 14: 241-254. doi:10.1016/j.gr.2007.08.001

Valentine, J.W. and Moores, E.M. “Plate-tectonic Regulation of Faunal Diversity and Sea Level: a Model.” *Nature* (1970) 228: 657-659. doi:10.1038/228657a0

Zhiyi, Z., Wenwei, Y., and Zhiqiang, Z. “Patterns, processes and likely causes of the Ordovician trilobite radiation in South China.” *Geological Journal* (2007) 42: 297-313. doi:10.1002/gj.1076

Peters, S.E. and Heim, N.A. “Stratigraphic distribution of marine fossils in North America.” *Geology* (2010) 39.3: 259-262. doi:10.1130/G31442.

