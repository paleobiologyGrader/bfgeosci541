##Introduction
Explanations of global trilobite biodiversity decline range from active displacement by brachiopod dominated environments to paleocontinental movement and its differing effects on various taxonomic ranks (Harper et al 2015; Westrop and Adrain 2001). These include change in the depth of seas, freshwater circulation, and ocean flux patterns (DeVries and Primeau 2011; Balseiro and Waisfeld 2013). All of them are documented to some extent. Yet their individual effects on biodiversity are inherently difficult to determine due to convolution. **Trilobite familial abundance change was strongly linked to brachiopod radiation across the Proteozoic. By using geoplate and paleocoordinate data, deconvolution of trilobite and brachiopod familial richness can be performed and subsequent correspondence analysis on geoplate presence/absence matrices for both deconvoluted phyla can be run. The main goal is to minimize objective paleocontinental movement when analyzing correspondence.**

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


