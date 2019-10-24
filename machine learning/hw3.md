# 抽取60天数据
## 1. 设置index，loc
- 抽取数据后df为空
![date](../img/python/19class/20191023/date01.png)
- 源文件时间降序
### 1）改为升序
```
df_concat.sort_index(inplace = True) 
```
### 2）start_date与end_date对调
```
df_concat.loc[e_date:s_date,:] 
```
## 2. Date column 索引
```
df_concat[(df_concat['Date'] >= '2016-04-01') & (df_concat['Date'] <= '2016-05-30')]
```
# 数据标准化
## ERROR：(n,)与(n,1)
- 调用standardscaler(score)函数报错

```
score = df_new['Compound_multiplied'].values
```

![error01](../img/python/19class/20191023/error01.png)
![01](../img/python/19class/20191023/01.png)

- reshape(-1,1)
```
score = df_new['Compound_multiplied'].values.reshape(-1,1)
```

![02](../img/python/19class/20191023/02.png)

- df[['column']]
```
score = df_new[['Compound_multiplied']].values
```

![03](../img/python/19class/20191023/03.png)
## 数据标准化的作用
- 无量纲化，便于不同评价指标的比较
- 弱化奇异值对模型的影响
- 加快梯度下降求最优解的速度  

| 未归一化 | 归一化 |
| :-: | :-: |
|$J = (3\theta_{1} + 600\theta_{2} - y_{correct})^{2}$|$(0.5\theta_{1}+0.55\theta_{2}-y_{correct})^{2}$
| ![gradient](../img/python/19class/20191023/梯度更新.png)|![gradient2](../img/python/19class/20191023/梯度更新2.png)
> 来源：https://zhuanlan.zhihu.com/p/27627299
## 几种不同的标准化方法
### StandardScale
- 原理  
  
  $z=\frac{x-mean(x)}{std(x)}$
  
- 调用
```
def standard_scaler(score):                 
    scaler = StandardScaler().fit(score)   #保存标准化参数
    scaled_data = scaler.transform(score)
    #scaled_data = StandardScaler().fit_transform(x)
    return scaled_data
```
- 实现
```
def standard_scaler_1(x):          #实现StandardScaler
    x = (x - np.mean(x,axis = 0)) / np.std(x, axis = 0)
    return x
```
### MinMaxScaler
- 原理
  
  $z=\frac{x-min(x)}{max(x)-min(x)}$

- 调用
```
def min_max_scaler(x):               #MinMaxScaler
#     scaler = MinMaxScaler.fit(x)
#     scaled_data = scaler.transform(x)
    scaled_data = MinMaxScaler().fit_transform(x)
    return scaled_data             #实现MinMaxScaler
```
- 实现
```
def min_max_scaler_1(x):
    x = (x - np.min(x, axis = 0)) /(np.max(x, axis = 0) - np.min(x, axis = 0))
    return x
```
### MaxAbsScaler
- 原理  
  
  $z=\frac{x}{max(x)}$
- 调用
```
def max_abs_scaler(x):          #MaxAbsScaler 
    
    scaled_data = MaxAbsScaler().fit_transform(x)

#     scaler = preprocessing.MaxAbsScaler()
#     scaled_data = scaler.fit_transform(x)
  
    return scaled_data
```
- 实现
```
def max_abs_scaler_1(x):         #实现MaxAbsScaler      
    x = x / np.max(x,axis = 0)
    return x
```
### 更多方法
![sklearn](../img/python/19class/20191023/preprocessing.png)