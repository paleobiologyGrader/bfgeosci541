Part one questions
1. 704 collections are associated with this reference. 
2. 24429

Collection 72438
1. The significance of this citation is that Conrad was the person who named it. 
2. Class: Strophomenata
	Order: Strophomenida
	Family: Strophomenidae
	Genus: Strophomena
	Species: Strophomena planumbona
3. Union County, Indiana
4. The Upper Ordovician (Katian period).
5. Liberty Formation in Indiana

Part two questions
1. The different colors signify different levels of temporal resolution for the different occurrences.
2. Belgium, the United States, and the United Kingdom
3. Cinncinati
4. The finest resolved timeframe was the Ordovician period, but most can be generalized to the Paleozoic era.

1. Most occurrences of Ambonychia were arrayed parallel to the equator.
2. Ambonychia belongs to the Myalinida order.

Part three questions
1. https://paleobiodb.org/data1.2/occs/list.json?base_name=Ambonychia&strat=Lexington Limestone
2. https://paleobiodb.org/data1.2/occs/list.csv?base_name=Mammalia&interval=Paleocene,Oligocene
3. https://paleobiodb.org/data1.2/taxa/opinions.csv?base_name=Testudines&interval=Mesozoic&op_type=all
4. https://paleobiodb.org/data1.2/colls/list.csv?base_name=Aves, Marsupialia, Sirenia&cc=US
5. https://paleobiodb.org/data1.2/occs/list.csv?base_name=Ficus&taxon_reso=genus&show=refattr








API function

downloadPBDB <- function(taxon,interval) {
	URL <- paste("https://paleobiodb.org/data1.2/occs/list.csv?base_name=",taxon,"&interval=",interval,sep="")
	tempPBDB <- read.csv(URL)
	return(tempPBDB)
}
