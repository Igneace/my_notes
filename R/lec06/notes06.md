# 矩阵的创建，性质及运算
## 矩阵创建
- matrix按列填充
```
> matrix(seq(1,12),nrow = 3)
     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12
```
```
> x <- seq(1,3)
> x
[1] 1 2 3
> x2 <- x^2
> x2
[1] 1 4 9
```
- cbind
```
> X <- cbind(x,x2)
> X
     x x2
[1,] 1  1
[2,] 2  4
[3,] 3  9
```
- rbind
```
> Y <- rbind(x,x2)
> Y
   [,1] [,2] [,3]
x     1    2    3
x2    1    4    9
```
## 矩阵访问
```
> X
     x x2
[1,] 1  1
[2,] 2  4
[3,] 3  9
```
- X[3,2]
- X[i,]
- X[,j]
### 访问矩阵三角
```
> H3
          [,1]      [,2]      [,3]
[1,] 1.0000000 0.5000000 0.3333333
[2,] 0.5000000 0.3333333 0.2500000
[3,] 0.3333333 0.2500000 0.2000000
```
#### lower.tri(H3) 
- 下三角return TRUE
```
> lower.tri(H3)
      [,1]  [,2]  [,3]
[1,] FALSE FALSE FALSE
[2,]  TRUE FALSE FALSE
[3,]  TRUE  TRUE FALSE
```
#### upper.tri(H3)
- 上三角return TRUE
```
> upper.tri(H3)
      [,1]  [,2]  [,3]
[1,] FALSE  TRUE  TRUE
[2,] FALSE FALSE  TRUE
[3,] FALSE FALSE FALSE
```
- 令上三角 + diag 值为0
```
> Hnew <- H3
> Hnew[upper.tri(H3, diag = TRUE)] <- 0
> Hnew
          [,1] [,2] [,3]
[1,] 0.0000000 0.00    0
[2,] 0.5000000 0.00    0
[3,] 0.3333333 0.25    0
```