#Lab Exercise Four

##Section one
1. Miocene=603, Early Jurassic=169, Late Cretaceous=375, Pennsylvanian=133
  > sum(PresencePBDB["Miocene",])

2. There are 29 epochs in this data set. 
  > str(PresencePBDB)

3. *Mytilus* is present in the Pridoli, Early Devonian, Cisuralian, Late Jurassic, Eocene, Late Cretaceous, Early Cretaceous, Middle Jurassic, Paleocene, Oligocene, Miocene, Early Jurassic, Pleistocene, Middle Triassic, Pliocene, and Early Triassic epochs. 
  > which(PresencePBDB[,"Mytilus"]==1)

4. We can infer from 3 that *Mytilus* was present in the Mississippian, Middle Devonian, Late Devonian, Guadalupian, and Lopingian epochs.

##Section two
1. jacsim(PresencePBDB) = 0.8279221
  > library(dplyr)

  > jacsim <- function(x) {

  > jac1 <- data.frame(Pleistocene=x["Pleistocene",],Miocene=x["Miocene",])
  
  > jac2 <- mutate(.data=jac1, sums=rowSums(jac1))
  
  > a <- ifelse(jac2[,"sums"]==2,TRUE,ifelse(jac2[,"sums"]==1,FALSE,ifelse(jac2[,"sums"]==0,NA,NA)))
  
  > b <- length(which(a))
  
  > c <- length(which(a==FALSE))
  
  > d <- b/(b+c)
  
  > return(d)
  
  > }
  
2. 1.0-0.8279221=0.1720779

3. 
  > vegdist(PresencePBDB[c("Pleistocene","Miocene"),], method="jaccard")

4. 
  > vegdist(PresencePBDB[c("Pleistocene","Pliocene","Miocene","Oligocene","Eocene",

  > "Paleocene"),], method="jaccard")
  
##Section three

##Section four
1.
  > Ordovician <- downloadPBDB(Taxa="animalia",StartInterval="Ordovician",StopInterval="")

2.
  > Ordovician <- cleanGenus(Ordovician)

3.
  > Ordovician <- cullMatrix(PresencePBDB,minOccurrences=2,minDiversity=25)

4. I looked at the summaries of samples drawn (without replacement) from both the "paleolat" and "paleolng" categories in the Ordovician data set. Because the latitude distribution is constrained more due to latitudinal tolerances of organisms, it would seem to make sense that the DCA2 axis would relate to the latitude, and the DCA1 axis with its relatively random distribution density would relate to longitude in the downloaded data.
  > distlng <- sample(Ordovician[,"paleolng"],replace=FALSE)
  
  > distlat <- sample(Ordovician[,"paleolat"],replace=FALSE)

  > summary(distlng)
  
  > summary(distlat)


  
