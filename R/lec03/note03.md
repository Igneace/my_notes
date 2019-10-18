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

##求小于n的质数
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