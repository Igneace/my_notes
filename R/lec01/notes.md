# R常用命令
- 观察内置数据：data()
- 设置工作目录：setwd("路径名")
- 罗列会话对象:ls()
- 删除对象：rm(xx)
- 运行源代码:source("xxx")
- 退出：q()  
# R的命名存储:= 与<-
&#10084; 函数传参时用"=",一般赋值运算"<-"与"="均可
# R的向量
## 定义向量
```
x<-c(0,7,8)
y <- 3:10
z = c(x,y)

seq(1, 20, by=3)                  #seq
[1] 1 4 7 10 13 16 19

rep(3,12)                         #rep
[1] 3 3 3 3 3 3 3 3 3 3 3 3

rep(seq(2, 20, by = 2), 2)
[1] 2 4 6 8 10 12 14 16 18 20 2 4 6 8 10 12 14 16 18 20

rep(c(1, 4), c(3, 2))
[1] 1 1 1 4 4

rep(c(1, 4), each = 3)
[1] 1 1 1 4 4 4

rep(1:10, rep(2, 10))
[1] 1 1 2 2 3 3 4 4 5 5 6 6 7 7 8 8 9 9 10 10

sample(1:6, size = 8, replace = TRUE) # 1：6内重复随机抽样8次
[1] 1 5 1 5 3 1 2 1
```  
## 向量中查找数据
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
```
#定义

colors <- c("red", "yellow", "blue")  

#提取字符串中的字符  substr(x, start, stop)

substr(colors, 1, 2)       
[1] "re" "ye" "bl"

#paste将flowers 拼接到字符串向量中的每个字符中

paste(colors, "flowers")     
[1] "red flowers" "yellow flowers" "blue flowers"
```
# Factors
## 创建
```
> grp <- factor(c("control","treatment","control","treatment"))
> grp
[1] control   treatment control   treatment
Levels: control treatment
```
## levels的用法
```
> as.integer(grp)
[1] 1 2 1 2

#标签查询
> levels(grp)
[1] "control"   "treatment"
> levels(grp)[as.integer(grp)]                           
[1] "control"   "treatment" "control"   "treatment"
#更改标签
> levels(grp)[1] <- "placebo"                            
> grp
[1] placebo   treatment placebo   treatment
Levels: placebo treatment
```
## 矩阵与数组
### 矩阵创建
```
> m <- matrix(1:6,nrow =2,ncol =3)
> m
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
```
### 矩阵查询
```
> m[2,3]
[1] 6
> m[1,]
[1] 1 3 5
> m[,2]
[1] 3 4

```
### 数组创建
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
### 数组查询
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