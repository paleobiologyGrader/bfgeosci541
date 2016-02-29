#Lab Exercise Five
##Problem Set 1
1)
  > BivalvePresence <- BivalveAbundance
  
  > BivalvePresence[BivalvePresence>0] <- 1
  
  > sum(BivalvePresence["Miocene",])
  
  > [1] 634
  
2) 
  > max(BrachiopodAbundance["Pliocene",])/sum(BrachiopodAbundance["Pliocene",])
  
  > [1] 0.2222222
  
3)
  > gs <- function(x,interval) {

  > a <- sum(x[interval,])^2

  > b <- x[interval,]^2

  > c <- b/a

  > d <- 1-sum(c)

  > return(d)

  > }
  
  > gs(BrachiopodAbundance,"Late Ordovician")
  
  > [1] 0.9784588
  
4)
  > erebus <- function(x,interval) {
  
  > a <- x[interval,]

  > b <- a[a != 0]
  
  > c <- sum(b)

  > d <- b/c

  > e <- d*log(d)

  > f <- -sum(e)

  > return(f)

  > }
  
  > erebus(BivalveAbundance, "Late Cretaceous")
  
  > [1] 5.086654

5) 
  > erebus(BivalveAbundance, "Paleocene")
  
  > [1] 4.511875

6) The K-Pg extinction event resulted in a mass extinction of a large portion of the species on Earth some 66 million years ago. This number (0.8870025) does not seem to accurately represent how much biodiversity survived into the Paleocene.
  > erebus(BivalveAbundance, "Paleocene")/erebus(BivalveAbundance, "Late Cretaceous")
  
  > [1] 0.8870025

7) This number seems to be more appropriate for such a large mass extinction as the K-Pg.
  > exp(erebus(BivalveAbundance, "Paleocene"))/exp(erebus(BivalveAbundance, "Late Cretaceous"))

  > [1] 0.5628292
  
##Problem Set 2
1)
  > specnumber(BivalveAbundance["Miocene",])
  
  > [1] 634
  
2)
  > diversity(BrachiopodAbundance["Late Ordovician",], index="simpson")
  
  > [1] 0.9784588

3)
  > diversity(BivalveAbundance["Late Cretaceous",], index="shannon")
  
  > [1] 5.086654
  
4)
  > diversity(BivalveAbundance["Paleocene",], index="shannon")
  
  > [1] 4.511875
  
##Problem Set 3
1)
  > bivalveframe <- data.frame(bivalve_richness=apply(BivalveAbundance, 1, specnumber))

  > brachframe <- data.frame(brach_richness=apply(BrachiopodAbundance, 1, specnumber))
  
  > bivalveframe <- mutate(bivalveframe, names=dimnames(bivalveframe)[[1]])
  
  > brachframe <- mutate(brachframe, names=dimnames(bivalveframe)[[1]])
  
  > InOrder <- data.frame(names=c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian" ,"Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene"))
  
  > bivalveframe <- bivalveframe[match(InOrder$names, bivalveframe$names),]
  
  > brachframe <- brachframe[match(InOrder$names, brachframe$names),]
  
  > corframe <- data.frame(brachframe, bivalveframe)

  > cor(corframe$brach_richness, corframe$bivalve_richness)
  
|                    |brach_richness |
|:------------------:|:-------------:|
|**bivalve_richness**|      -0.567194|

In addition I also found the R squared statistic for the linear regression of the data (bivalve_richness intercept was about 320.2) after plotting it, then created a function to determine the p-value of that R squared value. 

  > summary(lm(brach_richness~bivalve_richness, data=corframe))$r.squared
  
  > [1] 0.321709
  
  > lmp <- function(model) {
  
  > if (class(model)!="lm")
  
  > stop("Not an object of class 'lm'")
  
  > f <- summary(model)$fstatistic
  
  > p <- pf(f[1], f[2], f[3], lower.tail=FALSE)
  
  > attributes(p) <- NULL
  
  > return(p)
  
  > }
  
  > lmp(lm(brach_richness~bivalve_richness, data=corframe))
  
  > [1] 0.001334033

2)
> diversityframe <- data.frame(brach_diversity=apply(BrachiopodAbundance, 1, function (x, index="simpson", MARGIN=1, base=exp(1))

> {

>     x <- drop(as.matrix(x))

>     INDICES <- c("shannon", "simpson", "invsimpson")

>     index <- match.arg(index, INDICES)

>     if (length(dim(x)) > 1) {

>         total <- apply(x, MARGIN, sum)

>         x <- sweep(x, MARGIN, total, "/")

>     }

>     else {

>         x <- x/sum(x)

>     }

>     if (index == "shannon") 

>         x <- -x * log(x, base)

>     else x <- x * x

>     if (length(dim(x)) > 1) 

>         H <- apply(x, MARGIN, sum, na.rm = TRUE)

>     else H <- sum(x, na.rm = TRUE)

>     if (index == "simpson") 

>         H <- 1 - H

>     else if (index == "invsimpson") 

>         H <- 1/H

>     H

> }),

> bivalve_diversity=apply(BivalveAbundance, 1, function(x, index="simpson", MARGIN=1, base=exp(1))

> {

>     x <- drop(as.matrix(x))

>     INDICES <- c("shannon", "simpson", "invsimpson")

>     index <- match.arg(index, INDICES)

>     if (length(dim(x)) > 1) {

>         total <- apply(x, MARGIN, sum)

>         x <- sweep(x, MARGIN, total, "/")

>     }

>     else {

>         x <- x/sum(x)

>     }

>     if (index == "shannon") 

>         x <- -x * log(x, base)

>     else x <- x * x

>     if (length(dim(x)) > 1) 

>         H <- apply(x, MARGIN, sum, na.rm = TRUE)

>     else H <- sum(x, na.rm = TRUE)

>     if (index == "simpson") 

>         H <- 1 - H

>     else if (index == "invsimpson") 

>         H <- 1/H

>     H

> }))

> diversityframe <- mutate(diversityframe, names=dimnames(diversityframe)[[1]])

> diversityframe <- diversityframe[match(InOrder$names, diversityframe$names),]

> rownames(diversityframe) <- NULL

> cor(diversityframe[,"brach_diversity"], diversityframe[,"bivalve_diversity"])

> [1] -0.2624135

3) The biggest drop in brachiopods, purely by richness, occurred between the Lopingian and Early Triassic (loss of 343 species).

##Problem Set 4
1)
> SampleAbundances <- apply(BrachiopodAbundance,1,sum)

> SampleAbundances[which(SampleAbundances==min(SampleAbundances))]

> StandardizedRichness <- apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
  
> StandardizedRichness[1:6]


  |**Mississippian**|**Pennsylvanian**|**Early Ordovician**|**Middle Ordovician**|**Late Ordovician**|**Llandovery**|
  |:---------------:|:---------------:|:------------------:|:-------------------:|:-----------------:|:------------:|
  |            43.07|            34.72|               37.97|                45.69|              42.35|         41.00| 


2)
> brach_standard <- StandardizedRichness

> brach_standard <- data.frame(brach_standard, names=names(brach_standard))

> brach_standard <- brach_standard[match(InOrder$names, brach_standard$names),]

> brach_standard$names <- NULL

> brachframe <- data.frame(brachframe, brach_standard)

> cor(brachframe$brach_richness, brachframe$brach_standard)

> [1] 0.8849289
3)
4)
