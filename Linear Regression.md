Linear Regression
========================================================


Create and Load data  

```r
year  <- rep(2008:2010, each=4)
quarter  <- rep(1:4, 3)
cpi  <- c(162.2, 164.6, 166.5, 166.0,
          166.2, 167.0, 168.6, 169.5,
          171.0, 172.1, 173.3, 174.0)
plot(cpi, xaxt="n", ylab="CPI", xlab="")
# draw x-axis
axis(1, labels=paste(year,quarter,sep="Q"), at=1:12, las=3)
```

![plot of chunk unnamed-chunk-1](figure/unnamed-chunk-1.png) 

Check correlation between CPI and other variable


```r
cor(year, cpi)
```

```
## [1] 0.9096
```



```r
cor(quarter, cpi)
```

```
## [1] 0.3738
```

build linear regression model with `lm()` function on this data, using year and quarter as predicators and CPI as response.


```r
fit  <- lm(cpi ~ year + quarter)
fit
```

```
## 
## Call:
## lm(formula = cpi ~ year + quarter)
## 
## Coefficients:
## (Intercept)         year      quarter  
##    -7644.49         3.89         1.17
```

Predict CPI in 2011


```r
(cpi2011 <- fit$coefficients[[1]] + fit$coefficients[[2]]*2011 +
   fit$coefficients[[3]]*(1:4))
```

```
## [1] 174.4 175.6 176.8 177.9
```

more details about the model .


```r
attributes(fit)
```

```
## $names
##  [1] "coefficients"  "residuals"     "effects"       "rank"         
##  [5] "fitted.values" "assign"        "qr"            "df.residual"  
##  [9] "xlevels"       "call"          "terms"         "model"        
## 
## $class
## [1] "lm"
```


```r
fit$coefficients
```

```
## (Intercept)        year     quarter 
##   -7644.488       3.888       1.167
```

The differences between observed values and fitted values can be obtained with function `residuals()`.


```r
residuals(fit)
```

```
##        1        2        3        4        5        6        7        8 
## -0.57917  0.65417  1.38750 -0.27917 -0.46667 -0.83333 -0.40000 -0.66667 
##        9       10       11       12 
##  0.44583  0.37917  0.41250 -0.05417
```


```r
summary(fit)
```

```
## 
## Call:
## lm(formula = cpi ~ year + quarter)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -0.833 -0.495 -0.167  0.421  1.387 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -7644.488    518.654  -14.74  1.3e-07 ***
## year            3.888      0.258   15.06  1.1e-07 ***
## quarter         1.167      0.189    6.19  0.00016 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.73 on 9 degrees of freedom
## Multiple R-squared:  0.967,	Adjusted R-squared:  0.96 
## F-statistic:  133 on 2 and 9 DF,  p-value: 2.11e-07
```

plot the model 



```r
par(mfrow=c(2,2))
plot(fit)
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10.png) 


pltot the model in 3D
-------


- `scatterplot3d()` creates a 3D scatter plot and `plane3d()` draws the fitted plane.
- Parameter `lab` specifies the number of tickmarks on the x- and y-axes.


```r
par(mfrow=c(1,1))
library(scatterplot3d)
s3d  <- scatterplot3d(year, quarter, cpi, highlight.3d=T, 
                      type="h", lab=c(2,3))

s3d$plane3d(fit)
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11.png) 


Predict cpi in 2011


```r
data2011  <- data.frame(year=2011, quarter = 1:4)
cpi2011  <- predict(fit, newdata = data2011)
style  <- c(rep(1,12), rep(2,4))
plot(c(cpi, cpi2011), xaxt="n", ylab="CPI", xlab="", pch=style, col=style)

axis(1, at=1:16, las=3,
     labels=c(paste(year,quarter,sep="Q"), "2011Q1", "2011Q2", "2011Q3", "2011Q4"))
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12.png) 

