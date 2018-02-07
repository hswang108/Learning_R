How to convert or transform the list
=====

Input List 

```r
L <- list(A = 25, B = 22, C = 25, D = 26)
L
```

```
## $A
## [1] 25
## 
## $B
## [1] 22
## 
## $C
## [1] 25
## 
## $D
## [1] 26
```


Expected Output 

```
$25
[1] "A" "C"

$22
[1] "B"

$26
[1] "D"
```




```r
split(names(L), unlist(L))
```

```
## $`22`
## [1] "B"
## 
## $`25`
## [1] "A" "C"
## 
## $`26`
## [1] "D"
```



Split - Divide into groups and re-assemble



```r
names(L)
```

```
## [1] "A" "B" "C" "D"
```



unlist - flatten lists 
Given a list structure x, unlist simplifies it to produce a vector which contains all the atomic components which occur in x.


```r
unlist(L)
```

```
##  A  B  C  D 
## 25 22 25 26
```




```r
str(unlist(L))
```

```
##  Named num [1:4] 25 22 25 26
##  - attr(*, "names")= chr [1:4] "A" "B" "C" "D"
```



TODO
You could also try with(stack(L), split(as.character(ind), values)).

```r
with(stack(L), split(as.character(ind), values))
```

```
## $`22`
## [1] "B"
## 
## $`25`
## [1] "A" "C"
## 
## $`26`
## [1] "D"
```
