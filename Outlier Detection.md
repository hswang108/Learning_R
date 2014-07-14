Outlier Detection
========================================================

Outlier detection with the LOF (Local Outlier Factor) algorithm.


The LOF algorithm
-----------------
LOF (Local Outlier Factor) is an algorithm for identifying density-based local outliers [Breunig et al., 2000]. With LOF, the local density of a point is compared with that of its neighbors. If the former is significantly lower than the latter (with an LOF value greater than one), the point is in a sparser region than its neighbors, which suggests it be an outlier.



```r
summary(cars)
```

```
##      speed           dist    
##  Min.   : 4.0   Min.   :  2  
##  1st Qu.:12.0   1st Qu.: 26  
##  Median :15.0   Median : 36  
##  Mean   :15.4   Mean   : 43  
##  3rd Qu.:19.0   3rd Qu.: 56  
##  Max.   :25.0   Max.   :120
```
Function `lofactor(data, k)` in packages `DMwR` and `dprep` calculates local outlier factors using the `LOF algorithm`, where `k` is the `number of neighbors` used in the calculation of the local outlier factors.

Calculate Outlier scores.
----------

DMwR: Functions and data for the book "Data Mining with R"


```r
library(DMwR)
```

```
## Loading required package: lattice
## Loading required package: grid
## KernSmooth 2.23 loaded
## Copyright M. P. Wand 1997-2009
```


remove "Species", which is a categorical variable. 


```r
iris2  <- iris[,1:4]
outlier.scores  <- lofactor(iris2, k = 5)
plot(density(outlier.scores))
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 
?lofactor: An implementation of the LOF algorithm

pick top 5 as outliers.

```r
outliers  <- order(outlier.scores, decreasing=T)[1:5]
```

who are the outliers. 

```r
print(outliers)
```

```
## [1]  42 107  23 110  63
```


Visualize outliers with plots
---------

show outliers with a biplot of the first two principal components
TODO: what is biplot and how to interpret this graph.

```r
n  <- nrow(iris2)
labels  <- 1:n
labels[-outliers]  <- "."
biplot(prcomp(iris2), cex=0.8, xlabs=labels)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

show outliers with a pairs plot. The outliers are labeled with + in red.


```r
pch <- rep(".",n)
pch[outliers]  <- "+"
col  <- rep("black", n)
col[outliers]  <- "red"
pairs(iris2, pch = pch, col=col)
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 

