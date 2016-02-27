#Lab Exercise Five
##Problem set 1
1)
  > BivalvePresence <- BivalveAbundance
  
  > BivalvePresence[BivalvePresence>0] <- 1
  
  > sum(BivalvePresence["Miocene",])
  
  > [1] 634
  
2) 
  > max(BrachiopodAbundance["Pliocene",])/sum(BrachiopodAbundance["Pliocene",])
  
  > [1] 0.2222222
  
3)
  > gsOrdo <- function(x,interval) {

  > a <- sum(x[interval,])^2

  > b <- x[interval,]^2

  > c <- b/a

  > d <- 1-sum(c)

  > return(d)

  > }
  
  > gsOrdo(BrachiopodAbundance,"Late Ordovician")
  
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

5) 
  > erebus(BivalveAbundance, "Paleocene")

6) The K-Pg extinction event resulted in a mass extinction of a large portion of the species on Earth some 66 million years ago. This number (0.8870025) does not seem to accurately represent how much biodiversity survived into the Paleocene.
  > erebus(BivalveAbundance, "Paleocene")/erebus(BivalveAbundance, "Late Cretaceous")
  
  > [1] 0.8870025

7) This number seems to be more appropriate for such a large mass extinction as the K-Pg.
  > exp(erebus(BivalveAbundance, "Paleocene"))/exp(erebus(BivalveAbundance, "Late Cretaceous"))

  > [1] 0.5628292
  
##Problem Set 2
1) 
