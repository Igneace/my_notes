> &#9730;Author: chenshuo
# R常用命令(没咋用过)
- 观察内置数据：data()
- 设置工作目录：setwd("路径名")
- 罗列会话对象:ls()
- 删除对象：rm(xx)
- 运行源代码:source("xxx")
- 退出：q()  
# R的命名存储:= 与<-
 函数传参时用"=",一般赋值运算"<-"与"="均可
# 向量
## 向量创建
```
x<-c(0,7,8)
y <- 3:10
z = c(x,y)
```
 ### seq
```
seq(1, 20, by=3)                 
[1] 1 4 7 10 13 16 19
```
### **rep(x,sth,len,times)**
> 1. x是要重复的vector/number
> 2. sth（只是便于理解用，不能写“sth = ”）可以是<br> 1)number: 1,2,3...<br>2)vector: c( ) & 1:n<br>3)each
> 3. times是将前面的整体重复n次
> 4. rep()与replicate()区别见后
- x是要重复的vector/number
```
> rep(4,2)
[1] 4 4
> rep(1:4,2)
[1] 1 2 3 4 1 2 3 4
> rep(seq(1,8,by = 2),2)
[1] 1 3 5 7 1 3 5 7
```
- sth可以是数字和向量
```
> rep(1:4,c(1,2,1,2))
[1] 1 2 2 3 4 4
> rep(1:8,rep(1:4,2))
 [1] 1 2 2 3 3 3 4 4 4 4 5 6 6 7 7 7 8 8 8 8
> rep(1:4,1:4)
 [1] 1 2 2 3 3 3 4 4 4 4
 ```
 - sth可以是each
 ```
> rep(1:4,each = 2)
[1] 1 1 2 2 3 3 4 4
```
- len与times
```
> rep(1:4,each = 2,len =4)
[1] 1 1 2 2
> rep(1:4, each = 2, len = 10)
 [1] 1 1 2 2 3 3 4 4 1 1
> rep(1:4, each = 2, times = 3)
 [1] 1 1 2 2 3 3 4 4 1 1 2 2 3 3 4 4 1 1 2 2 3 3 4 4
 ```
### **sample(x, size, replace = FALSE, prob = NULL)**
- x = n 等价于 x = 1:n
```
> sample(x = 5, size = 5)
[1] 2 4 3 5 1
> sample(x = 1:5, size = 5)
[1] 2 1 4 5 3
```
- x 也可以是字符向量
```
> sample(x = c('a','b','c','d','e'),size = 5)
[1] "d" "a" "c" "b" "e"
```
- replace = T放回抽样。缺省值FALSE
```
> sample(x = 1:5, size = 5, replace = T)
[1] 4 3 5 2 3
```
- prob代表x中对应元素被抽取的概率，相互是独立的，概率之和不需要为1
```
> a <- sample(x = 1:5, size = 5000, replace = T, prob = c(0.4, 0.4, 0.7, 0.1, 0.1))
> table(a)
a
   1    2    3    4    5 
1203 1167 2027  310  293 
```  
## 向量查询
```
z[2]
z[c(1, 4, 5)]
z[2 : 4]
z[-c(1, 3, 4)]  #去掉第1，3，4位置剩下的
```
## 向量的数学运算
```
y <- z^ 2  #z向量中每个元素求平方  

a<-c(1,2,3)
b<-c(3,2,1)
y <- a^ b   #  向量对应元素进行计算
y
[1] 1 4 3
```  
- 向量长度不对等的运算，短的向量循环运算  
## 字符向量
### 创建
```
colors <- c("red", "yellow", "blue")  
```
### 提取字符串中的字符  substr(x, start, stop)
```
substr(colors, 1, 2)       
[1] "re" "ye" "bl"
```
### paste将flowers 拼接到字符串向量中的每个字符中
```
paste(colors, "flowers")     
[1] "red flowers" "yellow flowers" "blue flowers"
```
# Factors
## 创建 factor(x = character(), levels)
```
> grp <- factor(c("control","treatment","control","treatment"))
> grp
[1] control   treatment control   treatment
Levels: control treatment
```
## levels的用法
### 标签查询

```
> levels(grp)
[1] "control"   "treatment"
```
- as.integer查询factor对象内部整数编码
```
> levels(grp)[as.integer(grp)]                           
[1] "control"   "treatment" "control"   "treatment"
```
### 标签更改
```
> levels(grp)[1] <- "placebo"                            
> grp
[1] placebo   treatment placebo   treatment
Levels: placebo treatment
```
# 矩阵(详见lec6)与数组
## 矩阵创建
```
> m <- matrix(1:6,nrow =2,ncol =3)
> m
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
```
##  矩阵查询
```
> m[2,3]
[1] 6
> m[1,]
[1] 1 3 5
> m[,2]
[1] 3 4

```
##  数组创建
```
> a <- array(1:24, c(3,4,2))
> a
, , 1

     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12

, , 2

     [,1] [,2] [,3] [,4]
[1,]   13   16   19   22
[2,]   14   17   20   23
[3,]   15   18   21   24
```
##  数组查询
```
> a[1,2,2]
[1] 16
> a[1,1,]
[1]  1 13
> a[1,,]
     [,1] [,2]
[1,]    1   13
[2,]    4   16
[3,]    7   19
[4,]   10   22
```