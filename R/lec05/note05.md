# 模拟其他随机变量
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
### dbinom(x, size, prob)