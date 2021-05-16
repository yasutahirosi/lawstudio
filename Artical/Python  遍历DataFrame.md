## Python | 遍历DataFrame

​        最近有一个需求就是遍历一个数据框后取得相应的数据，想要得到的格式是 [row_name,column_name,value]，研究了一下，现将实现方法描述如下。

​        首先我们创建一个演示数据集，男生女生在中文韩文及日文的分数表格。

```python
import pandas as pd

Chinese=[90,80]
Korean=[80,70]
Japanese=[70,60]

data=pd.DataFrame([Chinese,Korean,Japanese]).transpose()
data.columns=['Chinese','Korean','Japanese']
data.index=['Male','Female']
```

 ![截屏2021-05-16 下午5.25.44](https://tva1.sinaimg.cn/large/008i3skNgy1gqke999bt5j307d02ot8m.jpg)

​            按照本文开头的想法，我要实现的输出是['Male','Chinese',90]...

​            首先我们使用dataframe的遍历行的方法来，遍历行，并且存储迭代的变量，看看我们到底获取到了什么信息。

```python
x,y=[],[]
for i,j in data.iterrows():
    x.append(i)
    y.append(j)
```

![截屏2021-05-16 下午5.29.24](https://tva1.sinaimg.cn/large/008i3skNgy1gqked1b9qgj30h207bmxh.jpg)

我们可以清晰的看到x保存到了行的索引，y保存到了每一行对应的各列信息。因此我们下一步目标即是对y部分进行迭代解析，分离出列名及值，就完成了我们的目标。我们用y里面的一个元素进行测试，如下：

```python
c,u=[],[]
for col,col_value in y[0].iteritems():
    c.append(col)
    u.append(col_value)
    
```

![截屏2021-05-16 下午5.34.10](https://tva1.sinaimg.cn/large/008i3skNgy1gqkehzkpmhj30h4058749.jpg)

可以成功的分离出了，列名及值，因此迭代整个数据框的完整代码如下:

```python
iterdata=[]
for row,row_details in data.iterrows():
    for col,value in row_details.iteritems():
        iterdata.append(row+"'s "+col+' mean score is '+str(value))
        
```

![截屏2021-05-16 下午5.40.47](https://tva1.sinaimg.cn/large/008i3skNgy1gqkeovfhzqj30h6046wet.jpg)

