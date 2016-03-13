#Learning R

##Beginner Concepts
1.	mtcars is a dataframe, I used the class() function to find out
2.	precip is a 70 element vector with only $names as an attribute, to figure this out I initially tried using is.vector(precip) and str(precip), but then realized that it returns TRUE for list(). I then created a primitive function to test three things. 

 > is2 <- function(x)
 
 > {
 
 > c(is.vector(x), is.atomic(x), is.array(x))
 
 > }
 
 > is2(precip)
 
 > [1] “TRUE”     “TRUE”     “FALSE”

The function of the first two elements is to determine through logic whether precip is a vector, and if so, is it an atomic vector and not a list? Another way to go about that might be to use is.recursive(x) to directly query if it is a list. The third element double checks that precip is not, in fact, a one dimensional array.
3.	as.matrix(trees)
4.	Atlanta (print(precip[14]))
5.	> all <- list(“a”=precip, “b”=trees, “c”=mtcars)
6.	Yes it does, specifically it is a double-precision floating point vector which all numeric data is stored as in R.

> typeof(precip)

> [1] “double”

7.	mtcars[2,7]; mtcars[2,][[7]]; mtcars[,7][[2]]; mtcars$qsec[[2]]
8.	precip[c(“Juneau”, “Phoenix”, “Sacramento”)] <- c(23, 46, 12)
9.	No. I used a nested ifelse function with logical operators to compare Girth and Volume, if there were any Girth values greater than its corresponding Volume it would return a 1 in the vector, and if not a 0.

> ifelse(trees$Girth>trees$Volume, 1, ifelse(trees$Girth<trees$Volume, 0, NA))

> [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

10.	2356.633





##Intermediate Concepts

###Section 1
1.	The replace= argument of the sample() function indicate to R whether to sample with replacement (TRUE) or without (FALSE)
2.	ifelse(MyMatrix==FALSE, 0, ifelse(MyMatrix==TRUE, 1, NA))
3.	I formed a function, utilizing the previous ifelse statement. This works especially well because MyMatrix is already logical and need not be coerced.

> test <- function(x) {

> MyMatrix=ifelse(MyMatrix==TRUE,1,ifelse(MyMatrix==FALSE,0,NA))

> augMatrix=rowSums(MyMatrix)

> matrix(data=ifelse(augMatrix==12,TRUE,ifelse(augMatrix!=12,FALSE,NA)))

> }

> test(MyMatrix)

>		[,1]

> [1,]	FALSE

> [2,]	FALSE

> [3,]	FALSE

> [4,]	FALSE

> [5,]	FALSE

> [6,]	FALSE

> [7,]	FALSE

> [8,]	FALSE

###Section 2
1.

> length(which(MyMatrix==7))

> [1]  16
2.	
> colSums(MyMatrix)

> [1]  51   37   45   58   47   54   51   46   53   42   59   42
3.	
> apply(MyMatrix, 2, prod)

> [1]   290304     46656     123480     3402000     340200     1080000     1975680     79380     987840

> [10]   134400     4838400     72000

4.	ifelse(MyMatrix==10, 12, MyMatrix)
5.	length(which(MyMatrix>3 & MyMatrix<8))
6.	MyMatrix[,12] <- as.character(MyMatrix[,12])

7.
> newMatrix <- data.frame(MyMatrix, RowTest = ifelse(rowSums(MyMatrix)>70, TRUE,

> ifelse(rowSums(MyMatrix)<70, FALSE, NA)))


##Advanced Concepts

###Section 1
1.
> test <- function(x) {

> return(“Hello world.”)

> }

###Section 2
1.	Abbreviated sepal length with SL, sepal width with SW, etc.

> subiris <- function(x) {

> df1 <- data.frame(subset(x, Species=="setosa"))

> colnames(df1) <- c("setosa.SL", "setosa.SW", "setosa.PL", "setosa.PW", "Species")

> df2 <- data.frame(subset(x, Species=="versicolor"))

> colnames(df2) <- c("versicolor.SL", "versicolor.SW", "versicolor.PL", "versicolor.PW", "Species")

> df3 <- data.frame(subset(x, Species=="virginica"))

> colnames(df3) <- c("virginica.SL", "virginica.SW", "virginica.PL", "virginica.PW", "Species")

> df1$Species <- NULL; df2$Species <- NULL; df3$Species <- NULL

> d <- data.frame(df1, df2, df3)

> return(d)

> }

2.
> attach(iris) 

> sortiris <- function(x) {

> s <- ifelse(Sepal.Width>3.1, Sepal.Length+Petal.Length, ifelse(Sepal.Width<3.1, 

> Sepal.Length-Petal.Length, NA))

> return(s)

> }

3.
> library(dplyr)

> library(magrittr)

> avgbycyl <- function(x) {

> car_data <- mtcars %>% subset(cyl==x)

> return(mean(car_data$mpg))

> }




4.
> library(foreach) 

> powersim <- function(num) {

> a <- c(1:num)

> b <- foreach(a=1:num, .combine=rbind) %do% sample(1:69, 5, replace=F)

> c <- matrix(foreach(a=1:num) %do% sample(1:26, 1), ncol=1)

> cbind(b,c)

> }

Or

> powersim <- function(x) {

> foreach(1:x, .combine=rbind) %do% sample(1:69, 5, replace=FALSE) %>%

> data.frame(pow=matrix(foreach(1:x) %do% sample(1:26, 1)))

> }

5.
> powersimtest <- function(r1,r2,r3,r4,r5,p) {

> a <- powersim(1000000)

> b <- ifelse(a[1:1000000,]==c(r1,r2,r3,r4,r5,p), TRUE, 

> ifelse(a[1:1000000,]!=c(r1,r2,r3,r4,r5,p), FALSE, NA))

> b <- ifelse(b==TRUE, 1, ifelse(b==FALSE, 0, NA))

> b1 <- rowSums(b)

> b <- matrix(data=ifelse(b1==6, TRUE, ifelse(b1!=6, FALSE, NA)), ncol=1)

> return(which(b))

> }


##Expert Concepts
1.
> summary(precip)

> Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 

> 7.00   29.38   36.60   34.89   42.77   67.00 

> sd(precip)

> [1] 13.70665

2.	In this particular case the precip data is best visualized with a histogram, because there are too many cities to effectively convey the relevant information (i.e. distributions of rainfall amount).
3.	RandomNormal <- rnorm(70, mean=34.89, sd=13.70665)


4.	The actual function in answer to this problem is the second one (distcompavg), but I created the first to use within the second.

> compareDists <- function(x,y,iterations) {

> Barrel<-c(x,y)

> ReplicatedMeans<-array(data=NA, dim=iterations)

> for (counter in 1:iterations) {

> newx <- sample(Barrel[x],70,replace=T)

> newy <- sample(Barrel[y],70,replace=T)

> xmean <- mean(newx)

> ymean <- mean(newy)

> ReplicatedMeans[counter]<-xmean-ymean

> }

> return(abs(ReplicatedMeans))

> }



> distcompavg <- function(iterations) {

> d1 <- array(data=NA,dim=iterations)

> for (counter in 1:iterations) {

> d1[counter]<-length(which(compareDists(precip,RandomNormal,100)>2.326))

> }

> return(mean(d1))

> }

5.	The density distribution for the precip data is not abnormal, but it is skewed toward larger and smaller values, with a local density minimum around 25 inches. The distribution I created assumes a shape closer to that of the classic bell curve. Thus the test I ran was not a good measure of similarity between the two data sets. 
