# R中的数据存储
二进制，0.8无法精确表示  

0.8*2=1.6  取1<br>0.6*2=1.2  取1<br>0.2*2=0.4 取0<br>0.4*2=0.8 取0 <br>0.8表示成 0.1100<br>
# 逻辑向量做索引
```
> a <- c(TRUE,FALSE,FALSE,FALSE,TRUE)
> b <- c(13,7,8,2)
> b[a]
[1] 13 NA
```
```
> a <- c(3,6,9)
> a[a>6]
[1] 9
> b <- c(-1,8,3)
> b[b>a]
[1] 8
```
# DataFrame
## 常用操作
```
> head(women,3)             #head
  height weight
1     58    115
2     59    117
3     60    120
> tail(women,3)            #tail
   height weight
13     70    154
14     71    159
15     72    164
> nrow(women)              #nrow
[1] 15
> ncol(women)              #ncol
[1] 2
> dim(women)               #dim
[1] 15  2
> str(women)
'data.frame':	15 obs. of  2 variables:
 $ height: num  58 59 60 61 62 63 64 65 66 67 ...
 $ weight: num  115 117 120 123 126 129 132 135 139 142 ...
```
## 查询
```
> women[2,2]
[1] 117
> women[2,]
  height weight
2     59    117
> women[1:3,1]
[1] 58 59 60
> women$weight
[1] 115 117 120 123 126 129 132 135 139 142 146 150 154 159 164
> women$height[women$weight>140]        ##
[1] 67 68 69 70 71 72
```
# List
>&#10052;list可以存放长度不同的列<br>
>&#10052;dataframe只能存放长度相同的列  
```
> x <- c(3,2,3)
> y <- c("a","bc")
> z <- list(x,y)
> z
[[1]]
[1] 3 2 3

[[2]]
[1] "a"  "bc"

```
# apply家族函数
> <font face = '楷体' color = 'red' size = 4>apply家族函数详见附录</font>
## lapply
>&#10052;lapply将函数应用到list的每个元素中
```
> x <- c(3,2,3)
> y <- c(7,7)
> z <- list(x,y)
> lapply(z, mean)
[[1]]
[1] 2.666667

[[2]]
[1] 7
```
## vapply
```
> vapply(z, summary, FUN.VALUE = numeric(6))
            [,1] [,2]
Min.    2.000000    7
1st Qu. 2.500000    7
Median  3.000000    7
Mean    2.666667    7
3rd Qu. 3.000000    7
Max.    3.000000    7
```
## sapply
```
> head(iris)
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
5          5.0         3.6          1.4         0.2  setosa
6          5.4         3.9          1.7         0.4  setosa
> sapply(iris[,1:4], mean)
Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    5.843333     3.057333     3.758000     1.199333 
```
## tapply
> &#10084;tapply(vector, index, function)<br>
> &#10084;分组统计；function作用于vector，group by index

```
> head(iris)
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
5          5.0         3.6          1.4         0.2  setosa
6          5.4         3.9          1.7         0.4  setosa
> tapply(iris$Sepal.Width, iris$Species, mean)
    setosa versicolor  virginica 
     3.428      2.770      2.974 
```
```
> head(warpbreaks)
  breaks wool tension
1     26    A       L
2     30    A       L
3     54    A       L
4     25    A       L
5     70    A       L
6     52    A       L
> tapply(warpbreaks$breaks,list(warpbreaks$wool,warpbreaks$tension),median)
   L  M  H
A 51 21 24
B 29 28 17
```

