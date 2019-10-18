# 模拟其他随机变量
>R语言中提供了四类有关统计分布的函数（密度函数，累计分布函数，分位函数，随机数函数）。分别在代表该分布的R函数前加上相应前缀获得(d，p，q，r)。如：<br>
> 1）正态分布的函数是norm，命令dnorm(0)就可以获得正态分布的密度函数在0处的值(0.3989)(默认为标准正态分布)。<br>
> 2）pnorm(0)是0.5就是正态分布的累计密度函数在0处的值。<br>
> 3）qnorm(0.5)则得到的是0，即标准正态分布在0.5处的分位数是0（在来个比较常用的：qnorm(0.975)就是那个估计中经常用到的1.96了）。<br>
> 4）rnorm(n)则是按正态分布随机产生n个数据。
## Bernoulli Random Variables

```
> set.seed(23207)
> guesses <- runif(20)
> correct.answers <- (guesses < 0.2)
> correct.answers
 [1] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE
 [9]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
[17] FALSE FALSE FALSE  TRUE
```
```
> table(correct.answers)
correct.answers
FALSE  TRUE 
   14     6 
```
## Binomial Random Variables
### 计算p(X=x)
- dbinom(x, size, prob)
- x 是成功的次数，prob是成功的概率，size是实验的次数
```
> dbinom(x = 4, size = 6, prob = 0.5)
[1] 0.234375
```
### 计算p(X <= x)
- pbinom(x , size, prob)
- x 是成功的次数，prob是成功的概率，size是实验的次数
```
> pbinom(4, 6, 0.5)
[1] 0.890625
```
### 计算binomial分布的分位数
- qbinom(p1, size, p2)
- size是实验的次数，p2是成功的概率，p1是成功x次的概率
- 输出是成功的次数x
```
> qbinom(0.89, 6, 0.5)
[1] 4
```
### 产生随机binomial独立同分布序列
- rbinom(n, size, prob)
```
> rbinom(24, 15, 0.1)
 [1] 1 2 2 2 1 0 1 2 2 1 2 3 1 0 1 0 1 0 3 2 2 1 0 2
```
## Possion Random Variables
- dpois
- ppois
- qpois
- rpois
## Exponential Random Variables
- dexp
- pexp
- qexp
- rexp
