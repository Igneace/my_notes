# 绘图
- 略
# 简单统计
## aggregate
- 分组统计
- aggregate(a~b,dataset,function)<br>按dataset中的b分组，用function对a进行统计
```
> head(iris)
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
5          5.0         3.6          1.4         0.2  setosa
6          5.4         3.9          1.7         0.4  setosa
```
```
> aggregate(Sepal.Width~Species,iris,mean)
     Species Sepal.Width
1     setosa       3.428
2 versicolor       2.770
3  virginica       2.974
```
```
> aggregate(Sepal.Length~Species,iris,mean)
     Species Sepal.Length
1     setosa        5.006
2 versicolor        5.936
3  virginica        6.588
```
- aggregate(cbind(a,b)~c,dataset,function)<br>按dataset中的c列进行分组，用function对a，b两列分别统计
```
> head(iris)
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
5          5.0         3.6          1.4         0.2  setosa
6          5.4         3.9          1.7         0.4  setosa
```
```
> aggregate(cbind(Sepal.Width,Sepal.Length)~Species,iris,mean)
     Species Sepal.Width Sepal.Length
1     setosa       3.428        5.006
2 versicolor       2.770        5.936
3  virginica       2.974        6.588
```
## cov()协方差
- cov(a,b)： a，b两列的协方差
- cov()也可计算协方差矩阵
```
> head(trees)
  Girth Height Volume
1   8.3     70   10.3
2   8.6     65   10.3
3   8.8     63   10.2
4  10.5     72   16.4
5  10.7     81   18.8
6  10.8     83   19.7
```
```
> cov(trees$Height,trees$Volume)
[1] 62.66
```
```
> cov(trees)
           Girth   Height    Volume
Girth   9.847914 10.38333  49.88812
Height 10.383333 40.60000  62.66000
Volume 49.888118 62.66000 270.20280
```
## cor()相关系数
```
> head(trees)
  Girth Height Volume
1   8.3     70   10.3
2   8.6     65   10.3
3   8.8     63   10.2
4  10.5     72   16.4
5  10.7     81   18.8
6  10.8     83   19.7
```
```
> cor(trees$Girth,trees$Volume,method = "spearman")
[1] 0.9547151
```
```
> cor(trees,method = "spearman")
           Girth    Height    Volume
Girth  1.0000000 0.4408387 0.9547151
Height 0.4408387 1.0000000 0.5787101
Volume 0.9547151 0.5787101 1.0000000
```
## cor.test()
- 假设检验补充知识:<br>
&#8195;p值为原假设为真时，样本观察结果出现的概率<br>&#8195;p值越小，拒绝原假设的理由越充分<br>&#8195;p值可以反映决策风险度  
- cor.test()的原假设为cor=0
### p-value < 2.2e-16<br>cor = 0.9671194 
```
> cor.test(trees$Volume,trees$Girth)

	Pearson's product-moment correlation

data:  trees$Volume and trees$Girth
t = 20.478, df = 29, p-value < 2.2e-16
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.9322519 0.9841887
sample estimates:
      cor 
0.9671194 
```
### method = "spearman"
```
> cor.test(trees$Volume,trees$Girth,method = "spearman")

	Spearman's rank correlation rho

data:  trees$Volume and trees$Girth
S = 224.61, p-value < 2.2e-16
alternative hypothesis: true rho is not equal to 0
sample estimates:
      rho 
0.9547151 

Warning message:
In cor.test.default(trees$Volume, trees$Girth, method = "spearman") :
  无法给连结计算精確p值
```
### p-value = 0.002758;cor = 0.5192801 
```
> cor.test(trees$Girth,trees$Height)

	Pearson's product-moment correlation

data:  trees$Girth and trees$Height
t = 3.2722, df = 29, p-value = 0.002758
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.2021327 0.7378538
sample estimates:
      cor 
0.5192801 

```
## Shapiro-Wilk test
- 用于检验数据是否为正态分布
- 原假设是满足正态分布
- 若p > 0.05，在5%显著水平下，不能拒绝原假设
- 若p < 0.05，在5%显著水平下，拒绝原假设
```
> shapiro.test(trees$Height)

	Shapiro-Wilk normality test

data:  trees$Height
W = 0.96545, p-value = 0.4034
```
## Kolmogorov-Smirnov Test
- 单样本ks检验，检验样本是否来自特定分布。原假设是来自该分布
- 双样本ks检验，检验两个样本是否服从同意分布。原假设是来自同一分布
### trees$Height不满足N(100,10)
```
> ks.test(trees$Height,"pnorm",100,10)

	One-sample Kolmogorov-Smirnov test

data:  trees$Height
D = 0.9032, p-value < 2.2e-16
alternative hypothesis: two-sided

Warning message:
In ks.test(trees$Height, "pnorm", 100, 10) :
  Kolmogorov - Smirnov检验里不应该有连结
```
### trees$Height: mean = 76; sd = 6.37
```
> mean(trees$Height)
[1] 76
> sd(trees$Height)
[1] 6.371813
```
### trees$Height ~N(76,6.3)
```
> ks.test(trees$Height,"pnorm",76,6.3)

	One-sample Kolmogorov-Smirnov test

data:  trees$Height
D = 0.12436, p-value = 0.7239
alternative hypothesis: two-sided

Warning message:
In ks.test(trees$Height, "pnorm", 76, 6.3) :
  Kolmogorov - Smirnov检验里不应该有连结
```
## t.test()
```
> t.test(trees$Height)

	One Sample t-test

data:  trees$Height
t = 66.41, df = 30, p-value < 2.2e-16
alternative hypothesis: true mean is not equal to 0
95 percent confidence interval:
 73.6628 78.3372
sample estimates:
mean of x 
       76 
```
## Monte Carlo模拟
## 产生伪随机数(均匀分布)
- runif(n, min = a, max = b) 模拟独立均匀分布随机变量
- 缺省值a = 0，b = 1
```
> runif(5)
[1] 0.1780497 0.5446209 0.6015979 0.8241860 0.3242714
```
```
> runif(10,min=-1,max = 1)
 [1] -0.88299061  0.91140626  0.55537714  0.09843378
 [5] -0.79852980  0.60396286  0.10233457  0.58348982
 [9]  0.78739166  0.68024201
```

