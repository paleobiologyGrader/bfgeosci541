#Lab Exercise Five
##Problem Set 1

> 18/20

1)
````R
BivalvePresence <- BivalveAbundance
BivalvePresence[BivalvePresence>0] <- 1
sum(BivalvePresence["Miocene",])
[1] 634
````
  
2) 
  
````R
> max(BrachiopodAbundance["Pliocene",])/sum(BrachiopodAbundance["Pliocene",])
> [1] 0.2222222
`````
  
3)

````R  
> gs <- function(x,interval) {
> a <- sum(x[interval,])^2
> b <- x[interval,]^2
> c <- b/a
> d <- 1-sum(c)
> return(d)
> }
> gs(BrachiopodAbundance,"Late Ordovician")
> [1] 0.9784588
````
  
4)

````R
erebus <- function(x,interval) {
a <- x[interval,]
b <- a[a != 0]
c <- sum(b)
d <- b/c
e <- d*log(d)
f <- -sum(e)
return(f)
}
erebus(BivalveAbundance, "Late Cretaceous")
[1] 5.086654
````

5) 

```R
> erebus(BivalveAbundance, "Paleocene")
> [1] 4.511875
````

6) The K-Pg extinction event resulted in a mass extinction of a large portion of the species on Earth some 66 million years ago. This number (0.8870025) does not seem to accurately represent how much biodiversity survived into the Paleocene.

````R
> erebus(BivalveAbundance, "Paleocene")/erebus(BivalveAbundance, "Late Cretaceous")
> [1] 0.8870025
````

> You didn't completely answer the question! -0.5 Points

7) This number seems to be more appropriate for such a large mass extinction as the K-Pg.

````R
> exp(erebus(BivalveAbundance, "Paleocene"))/exp(erebus(BivalveAbundance, "Late Cretaceous"))
> [1] 0.5628292
````

> You didn't compeltely answer the question! 0.5 Points
  
## Problem Set 2

1)

````R
> specnumber(BivalveAbundance["Miocene",])
> [1] 634
````

2)

````R
> diversity(BrachiopodAbundance["Late Ordovician",], index="simpson")
> [1] 0.9784588
````

3)

````R
> diversity(BivalveAbundance["Late Cretaceous",], index="shannon")
> [1] 5.086654
````  

4)

````R
> diversity(BivalveAbundance["Paleocene",], index="shannon")
  
> [1] 4.511875
````
  
## Problem Set 3

1)
````R
> bivalveframe <- data.frame(bivalve_richness=apply(BivalveAbundance, 1, specnumber))
> brachframe <- data.frame(brach_richness=apply(BrachiopodAbundance, 1, specnumber))
> bivalveframe <- mutate(bivalveframe, names=dimnames(bivalveframe)[[1]])
> brachframe <- mutate(brachframe, names=dimnames(bivalveframe)[[1]])

> InOrder <- data.frame(names=c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian" ,"Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene"))
  
> bivalveframe <- bivalveframe[match(InOrder$names, bivalveframe$names),]

> brachframe <- brachframe[match(InOrder$names, brachframe$names),]
  
> corframe <- data.frame(brachframe, bivalveframe)

> cor(corframe$brach_richness, corframe$bivalve_richness)
  
|                    |**brach_richness**|
|:------------------:|:----------------:|
|**bivalve_richness**|         -0.567194|
````

In addition I also found the R squared statistic for the linear regression of the data (bivalve_richness intercept was about 320.2) after plotting it, then created a function to determine the p-value of that R squared value. 

````R
summary(lm(brach_richness~bivalve_richness, data=corframe))$r.squared
[1] 0.321709
lmp <- function(model) {
  if (class(model)!="lm") {
    stop("Not an object of class 'lm'")
    }
  f <- summary(model)$fstatistic
  p <- pf(f[1], f[2], f[3], lower.tail=FALSE)
  attributes(p) <- NULL
  return(p)
  }
  
lmp(lm(brach_richness~bivalve_richness, data=corframe))
[1] 0.001334033
````

> I'm glad you're having fun and experimenting with R. I do feel compelled to point out that you could use the ````summary( )```` and/or ````coefficients( )```` functions to achieve the same results much more efficiently. The most important thing to learn about coding is the same as the tips for scientific writing: accuracy, clarity, and brevity. Simple and straight-forward code is the best code.


2)

```R
  diversityframe <- data.frame(brach_diversity=apply(BrachiopodAbundance, 1, function (x, index="simpson", MARGIN=1, base=exp(1)) 
  {
    x <- drop(as.matrix(x))
    INDICES <- c("shannon", "simpson", "invsimpson")
    index <- match.arg(index, INDICES)
    if (length(dim(x)) > 1) {
         total <- apply(x, MARGIN, sum)
         x <- sweep(x, MARGIN, total, "/")
         }
    else {
        x <- x/sum(x)
       }
     if (index == "shannon") 
        x <- -x * log(x, base)
     else x <- x * x
      if (length(dim(x)) > 1) 
       H <- apply(x, MARGIN, sum, na.rm = TRUE)
     else H <- sum(x, na.rm = TRUE)
     if (index == "simpson") 
         H <- 1 - H
      else if (index == "invsimpson") 
         H <- 1/H
     H
     }),

bivalve_diversity=apply(BivalveAbundance, 1, function(x, index="simpson", MARGIN=1, base=exp(1))
 {
    x <- drop(as.matrix(x))
     INDICES <- c("shannon", "simpson", "invsimpson")
     index <- match.arg(index, INDICES)
     if (length(dim(x)) > 1) {
         total <- apply(x, MARGIN, sum)
         x <- sweep(x, MARGIN, total, "/")
     }
     else {
         x <- x/sum(x)
     }
     if (index == "shannon") 
         x <- -x * log(x, base)
     else x <- x * x
     if (length(dim(x)) > 1) 
         H <- apply(x, MARGIN, sum, na.rm = TRUE)
     else H <- sum(x, na.rm = TRUE)
     if (index == "simpson") 
         H <- 1 - H
     else if (index == "invsimpson") 
         H <- 1/H
     H
 }))

> diversityframe <- mutate(diversityframe, names=dimnames(diversityframe)[[1]])

> diversityframe <- diversityframe[match(InOrder$names, diversityframe$names),]

> rownames(diversityframe) <- NULL

> cor(diversityframe[,"brach_diversity"], diversityframe[,"bivalve_diversity"])

> [1] -0.2624135
```

> You might prefer the ````switch( )```` function to long strings of ````if/else( )```` statements.


3) The biggest drop in brachiopods, purely by richness, occurred between the Lopingian and Early Triassic (loss of 343 species).

##Problem Set 4

1)

````R
> SampleAbundances <- apply(BrachiopodAbundance,1,sum)
> SampleAbundances[which(SampleAbundances==min(SampleAbundances))]
> StandardizedRichness <- apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> StandardizedRichness[1:6]

  **Mississippian**|**Pennsylvanian**|**Early Ordovician**|**Middle Ordovician**|**Late Ordovician**|**Llandovery**
  -----------------|-----------------|--------------------|---------------------|-------------------|--------------
              43.07|            34.72|               37.97|                45.69|              42.35|         41.00 
````

2)

````R
> brach_standard <- StandardizedRichness
> brach_standard <- data.frame(brach_standard, names=names(brach_standard))
> brach_standard <- brach_standard[match(InOrder$names, brach_standard$names),]
> brach_standard$names <- NULL
> brachframe <- data.frame(brachframe, brach_standard)
> cor(brachframe$brach_richness, brachframe$brach_standard)
> [1] 0.8849289
````


3) When plotting unstandardized brachiopod and bivalve richness, an R squared value of 0.321709 was achieved through linear regression. Doing the same with standardized richness, the R squared value was slightly lower at 0.2963702. The two plots are different in their fit, but that doesn't explain the difference between standardized and unstandardized samples. Standardization is equivalent to saying how many standard deviations a dependent variable will change, instead of looking at aggregate number of species.

> No, that is not what standardization means in this case. There are many kinds of standardization. This form of standardizing was like what we discussed in lecture, subsampling, meaning what it would look like if we held the number of individuals constant.

````R
> StandardizedRichness<-apply(BivalveAbundance,1,subsampleIndividuals,Quota=124)
> bivalve_standard <- StandardizedRichness
> bivalve_standard <- data.frame(bivalve_standard, names=names(bivalve_standard))
> bivalve_standard <- bivalve_standard[match(InOrder$names, bivalve_standard$names),]
> bivalve_standard$names <- NULL
> bivalveframe <- data.frame(bivalveframe, bivalve_standard)
> richness <- data.frame(bivalveframe, brachframe)
> plot(richness$bivalve_standard, richness$brach_standard, type="p")
> summary(lm(richness$bivalve_standard~richness$brach_standard))$r.squared
> [1] 0.2963702
> lmp(lm(richness$bivalve_standard~richness$brach_standard))
> [1] 0.002264659
> plot(richness$bivalve_richness, richness$brach_richness, type="p")
> summary(lm(richness$bivalve_richness~richness$brach_richness))$r.squared
> [1] 0.321709
> lmp(lm(richness$bivalve_richness~richness$brach_richness))
> [1] 0.001334033
````

> -1 Points

4) Based purely on the correlation gleaned from question 1 in problem set three, there is evidence to show that as bivalve richness increased there was a corresponding drop in brachiopod richness. Although this could be indicative of competition between the two classes, there could be more subtle underlying factors such as differences in metabolism and available nutrients.
 
 > Hmm.... I do not like think this is a very good answer. What does metabolism have to do with anything? 
 
 > Don't extrapolate beyond the data at hand. All you have here are diversity patterns. Negatively correlated brachiopod and bivalve richness is consistent with one out-competing the other, but is not sufficient evidence to prove competition.
 
 > -1 Points
