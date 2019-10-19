> &#10084;Author: chenshuo
# loop&if&function
## for 
```
for (name in vector) {commands}
```
## while
```
wihle (condition) {statements}
```
## repeat
```
repeat {
    if (condition)
        break
}
```
## if
```
if (condition){
    commands
}else {
    commands
}
```
## function
```
fuc <- function(a,b){
    statements
}
```
# 应用案例

## 求小于n的质数
```
prime_fc <- function(n){
  sieve <- seq(2,n)
  primes <- c()
  for (i in seq(2,n)) {
    if (any(sieve == i)){
      primes <- c(primes, i)
      sieve <- sieve[(sieve%%i)!= 0]
    }
    
  }
  return(primes)                          #return后加()
}

```
## Newton寻根迭代
- 求$f(x)=x^{3} + 2*x^{2} - 7$的根
```
f <- x^3 + 2*x^2 -7
tolerance <- 0.0001
while (abs(f) > tolerance){
  f.prime <- 3*x^2 + 4*x
  x <- x - f/f.prime
  f <- x^3 + 2*x^2 -7
}
x
```

