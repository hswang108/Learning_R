Random Forest
========================================================

Package randomForest: There are two limitations with function randomForest(). First, it cannot handle data with missing values, and users have to impute data before feeding them into the function. Second, there is a limit of 32 to the maximum number of levels of each categorical attribute. Attributes with more than 32 levels have to be transformed first before using randomForest().


An alternative way to build a random forest is to use function cforest() from package party, which is not limited to the above maximum levels. However, generally speaking, categorical variables with more levels will make it require more memory and take longer time to build a random forest.

split the `iris` dataset into training and testing datasets.


```r
ind  <- sample(2, nrow(iris), replace=T, prob=c(0.7,0.3))
trainData  <- iris[ind ==1, ] 
testData  <- iris[ind ==2, ]
```

Load `randomForest` package to train a forest.


```r
library(randomForest)
```

```
## randomForest 4.6-7
## Type rfNews() to see new features/changes/bug fixes.
```

```r
rf  <- randomForest(Species ~ ., data = trainData, ntree=100,
                    proximity=TRUE)
table(predict(rf), trainData$Species)
```

```
##             
##              setosa versicolor virginica
##   setosa         35          0         0
##   versicolor      0         32         2
##   virginica       0          1        35
```

```r
print(rf)
```

```
## 
## Call:
##  randomForest(formula = Species ~ ., data = trainData, ntree = 100,      proximity = TRUE) 
##                Type of random forest: classification
##                      Number of trees: 100
## No. of variables tried at each split: 2
## 
##         OOB estimate of  error rate: 2.86%
## Confusion matrix:
##            setosa versicolor virginica class.error
## setosa         35          0         0     0.00000
## versicolor      0         32         1     0.03030
## virginica       0          2        35     0.05405
```



```r
attributes(rf)
```

```
## $names
##  [1] "call"            "type"            "predicted"      
##  [4] "err.rate"        "confusion"       "votes"          
##  [7] "oob.times"       "classes"         "importance"     
## [10] "importanceSD"    "localImportance" "proximity"      
## [13] "ntree"           "mtry"            "forest"         
## [16] "y"               "test"            "inbag"          
## [19] "terms"          
## 
## $class
## [1] "randomForest.formula" "randomForest"
```

plot the error rates with number of trees


```r
plot(rf)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

importance of variables can be obtained form the funcitons `importance()` and `varImpPlot()`.




```r
importance(rf)
```

```
##              MeanDecreaseGini
## Sepal.Length            5.623
## Sepal.Width             2.485
## Petal.Length           30.211
## Petal.Width            30.899
```




```r
varImpPlot(rf)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

predit the data in test dataset


```r
irisPred  <- predict(rf, newdata=testData)
table(irisPred, testData$Species)
```

```
##             
## irisPred     setosa versicolor virginica
##   setosa         15          0         0
##   versicolor      0         16         2
##   virginica       0          1        11
```




```r
plot(margin(rf, testData$Species))
```

```
## Loading required package: RColorBrewer
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8.png) 

























