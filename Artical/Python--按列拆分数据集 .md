Python ｜利用Groupby拆分数据集 



### 前言

​         最近有点忙，很久没有更新，今天更新一个小Tips。在工作中我们经常会遇到对数据集按列进行拆分的Task，下文展示如何运用Python的Groupby实现。

看到很多资料都是直接介绍Groupby之后进行聚合操作，其实最基本的对Groupy对象进行转换反而总是被忽略。但我觉得其实这个还挺重要的。

### 思路

常用的两种思路：

 <1>  找出需要按的列的Unique值 --> 运用Pandas常规的筛选方式进行取子集

<2>  直接利用Groupby --> 得到Groupby对象 --> 利用list和dict对Groupby对象进行转换

第一种方法过于简单及麻烦，下例直接展示利用Groupby拆分

### 代码及示例

![截屏2021-04-26 下午10.26.54](https://tva1.sinaimg.cn/large/008i3skNly1gpxill79o8j30dq0aljsj.jpg)

原始数据如上所示，现在我们需要按照'Year'进行拆分成多个Dataframe。

一行代码解决

```python
all=dict(list(data.groupby(['Year'],as_index=False)))
```

完整代码

创建示例数据集

```python
import pandas as pd
data={'Team': ['Riders', 'Riders', 'Devils', 'Devils', 'Kings','kings', 'Kings',         'Kings','Riders', 'Royals', 'Royals', 'Riders'],
      'Rank': [1, 2, 2, 3, 3,4 ,1 ,1,2 , 4,1,2],
      'Year': [2014,2015,2014,2015,2014,2015,2016,2017,2016,2014,2015,2017],
      'Points':[876,789,863,673,741,812,756,788,694,701,804,690]}
data= pd.DataFrame(data)
```

将数据按年进行分组，生成Groupby对象

```python
#exp1为Groupby对象
exp1=data.groupby(['Year'],as_index=False)
print(type(exp1))
```

![截屏2021-04-26 下午10.41.52](https://tva1.sinaimg.cn/large/008i3skNly1gpxj0cosolj30fr01n0st.jpg)

利用List和Dict将Groupby对象转换为包含拆分后所有DataFrame的字典对象

```python
exp2=dict(list(exp1))
```

![截屏2021-04-26 下午10.44.21](https://tva1.sinaimg.cn/large/008i3skNly1gpxj2pxnz1j30ou03xaas.jpg)

利用字典取key的方法取2014的数据

```python
#通过字典
year2014=exp2[2014]
```

![截屏2021-04-26 下午10.46.04](https://tva1.sinaimg.cn/large/008i3skNly1gpxj4oujegj30qi051mxn.jpg)