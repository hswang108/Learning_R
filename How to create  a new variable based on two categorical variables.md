How to create a new variable based on two categorical variables
========================================================

I have two categorical variables a & b.


```r
a = sample(0:1, size = 10, replace = T)
b = sample(0:1, size = 10, replace = T)
```



I want to create a new variable c, whose values depend on a & b in such a way:



```r
c = vector(length = 10)
c[a == 1 & b == 1] = 1
c[a == 1 & b == 0] = 2
c[a == 0 & b == 1] = 3
c[a == 0 & b == 0] = 4
```


