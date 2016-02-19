#Lab Exercise Four

##Section one
1. Miocene=603, Early Jurassic=169, Late Cretaceous=375, Pennsylvanian=133
  > sum(PresencePBDB["Miocene",])

2. There are 29 epochs in this data set. 
  > str(PresencePBDB)

3. *Mytilus* is present in the Pridoli, Early Devonian, Cisuralian, Late Jurassic, Eocene, Late Cretaceous, Early Cretaceous, Middle Jurassic, Paleocene, Oligocene, Miocene, Early Jurassic, Pleistocene, Middle Triassic, Pliocene, and Early Triassic epochs. 
  > which(PresencePBDB[,"Mytilus"]==1)

4.
