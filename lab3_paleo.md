#Lab Three

> 16/20... you forgot a whole section!

###Exercise one questions
1. 704 collections are associated with this reference. 
2. 24429

###Collection 72438
1. The significance of this citation is that Conrad was the person who named it. 
2. Class: Strophomenata
	Order: Strophomenida
	Family: Strophomenidae
	Genus: Strophomena
	Species: Strophomena planumbona
3. Union County, Indiana
4. The Upper Ordovician (Katian period).
5. Liberty Formation in Indiana

###Exercise two questions
1. The different colors signify different levels of temporal resolution for the different occurrences.
2. Belgium, the United States, and the United Kingdom
3. Cinncinati
4. The finest resolved timeframe was the Ordovician period, but most can be generalized to the Paleozoic era.

1. Most occurrences of Ambonychia were arrayed parallel to the equator.
2. Ambonychia belongs to the Myalinida order.

###Exercise three questions
1. https://paleobiodb.org/data1.2/occs/list.json?base_name=Ambonychia&strat=Lexington%20Limestone
2. https://paleobiodb.org/data1.2/occs/list.csv?base_name=Mammalia&interval=Paleocene,Oligocene
3. https://paleobiodb.org/data1.2/taxa/opinions.csv?base_name=Testudines&interval=Mesozoic&op_type=all
4. https://paleobiodb.org/data1.2/colls/list.csv?base_name=Aves,Marsupialia,Sirenia&cc=US
5. https://paleobiodb.org/data1.2/occs/list.csv?base_name=Ficus&taxon_reso=genus&show=refattr

> Close, you need to use Gastropoda:Ficus to prevent getting speciemsn of the plant Ficus. -1 points

###Exercise four questions
1. Gastrocoptidae is the family of the Gastrocopta genus.
2. The occurence of Isoetes in portugal is from the Aptian age, in the range of 125-113 Ma.
3. The oldest occurrence of Gastrocopta is from the Bridgerian North American Stage, approximately 46.2-50.3 Mya.
4. The only documented occurrence of Tiktaalik in the fossil record was located in the tropics when it was alive.
5. The occurrences of Namacalathus in Siberia come from two distinct formations, Raiga and Kotodzha.

###Exercise five questions
1. > URL <- "https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Pliocene"
   > MammutData <- read.csv(URL)
2. 39x13
3. The above call used the collections route. 
4. The genus being called for is Mammut, the colloquial name is Mastodon, and the query was limited to the Pliocene epoch.
5. URL <- "https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Miocene,Pleistocene"
6. URL <- "https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Miocene,Pleistocene&show=paleoloc"



###Sixth question
API function

> downloadPBDB <- function(taxon,interval) {

>	URL <- paste("https://paleobiodb.org/data1.2/occs/list.csv?base_name=",taxon,"&interval=",interval,sep="")

>	tempPBDB <- read.csv(URL)

>	return(tempPBDB)

>	}

> You didn't do the ammonoid section!? - 6 points
