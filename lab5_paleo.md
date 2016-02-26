Problem set 1
1)
  > BivalvePresence <- BivalveAbundance
  
  > BivalvePresence[BivalvePresence>0] <- 1
  
  > sum(BivalvePresence["Miocene",])
  
2) 
  > max(BrachiopodAbundance["Pliocene",])/sum(BrachiopodAbundance["Pliocene",])
  
3)
  > gsOrdo <- function(x,interval) {

  > a <- sum(x[interval,])^2

  > b <- x[interval,]^2

  > c <- b/a

  > d <- 1-sum(c)

  > return(d)

  > }
  
  > gsOrdo(BrachiopodAbundance,"Late Ordovician")
  
4.
  > shanentropy <- function(x,interval) {
  
  > a <- x[interval,]

  > b <- a[a != 0]
  
  > c <- sum(b)

  > d <- b/c

  > e <- d*log(d)

  > f <- -sum(e)

  > return(f)

  > }
  
  > shanentropy(BivalveAbundance, "Late Cretaceous")

5. 
  > shanentropy(BivalveAbundance, "Paleocene")

6. 
