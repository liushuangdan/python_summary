
Pandas数据规整-转换-离散化和面元划分
===

为了便于分析，连续数据常常被离散化或拆分为“面元”(bin)


```python
import numpy as np
import pandas as pd
```

例子：一组年龄数据，将它们划分为不同的年龄组
===

划分为“18到25”，‘26到35’，‘35到60’以及‘60以上’几个面元


```python
# 年龄
ages = [18, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]
#面元区间
bins = [18,25,35,60,100]
```


```python
cats = pd.cut(ages,bins)
cats
```




    [NaN, (18, 25], (18, 25], (25, 35], (18, 25], ..., (25, 35], (60, 100], (35, 60], (35, 60], (25, 35]]
    Length: 12
    Categories (4, interval[int64]): [(18, 25] < (25, 35] < (35, 60] < (60, 100]]



## 返回的是categories对象（划分的面元），可看做一组表示面元名称的字符串

底层含有：

一个codes属性中的年龄数据标签

一个表示不同分类的类型数组



```python
type(cats)
```




    pandas.core.arrays.categorical.Categorical




```python
cats.codes  #分组后的数据
```




    array([-1,  0,  0,  1,  0,  0,  2,  1,  3,  2,  2,  1], dtype=int8)




```python
cats.categories # 类型，分组区间
```




    IntervalIndex([(18, 25], (25, 35], (35, 60], (60, 100]]
                  closed='right',
                  dtype='interval[int64]')




```python
cats[11]  #查询单个值的分类
```




    Interval(25, 35, closed='right')




```python
# pd.cut结果的面元计数
pd.value_counts(cats)  #统计每个分组区间的数据的个数
```




    (18, 25]     4
    (35, 60]     3
    (25, 35]     3
    (60, 100]    0
    dtype: int64



cut方法：默认是左开右闭区间，不包含起始值，包含结束值

right=False后，左闭右开区间，包含起始值，不包含结束值


```python
cats2 = pd.cut(ages,bins,right=False)
cats2
```




    [[18, 25), [18, 25), [25, 35), [25, 35), [18, 25), ..., [25, 35), [60, 100), [35, 60), [35, 60), [25, 35)]
    Length: 12
    Categories (4, interval[int64]): [[18, 25) < [25, 35) < [35, 60) < [60, 100)]




```python
cats.codes
```




    array([-1,  0,  0,  1,  0,  0,  2,  1,  3,  2,  2,  1], dtype=int8)




```python
cats.categories
```




    IntervalIndex([(18, 25], (25, 35], (35, 60], (60, 100]]
                  closed='right',
                  dtype='interval[int64]')



## 修改面元名称


```python
cat3 = pd.cut(ages, bins)
cat3 = pd.cut(ages, bins, labels=False)  # 去掉面元名称
cat3 = pd.cut(ages, bins, labels=['少年', '青年', '中年', '老年'])  # 自定义面元名称
cat3
```




    [NaN, 少年, 少年, 青年, 少年, ..., 青年, 老年, 中年, 中年, 青年]
    Length: 12
    Categories (4, object): [少年 < 青年 < 中年 < 老年]




```python
cat3.codes
```




    array([-1,  0,  0,  1,  0,  0,  2,  1,  3,  2,  2,  1], dtype=int8)




```python
cat3.categories
```




    Index(['少年', '青年', '中年', '老年'], dtype='object')



## 不指定面元切分的起始结束值，而是指定面元切分的个数（切成几份），自动计算面元起始结束值



```python
cat4 = pd.cut(ages, 4, precision=2)  # 将数据分成四组，限定小数位数为2位
cat4
```




    [(17.96, 28.75], (17.96, 28.75], (17.96, 28.75], (17.96, 28.75], (17.96, 28.75], ..., (28.75, 39.5], (50.25, 61.0], (39.5, 50.25], (39.5, 50.25], (28.75, 39.5]]
    Length: 12
    Categories (4, interval[float64]): [(17.96, 28.75] < (28.75, 39.5] < (39.5, 50.25] < (50.25, 61.0]]




```python
28.75-17.96
39.5-28.75
39.5-50.25
61-50.25
```




    10.75



## 18 - 61,等分为四份


```python
# 18 - 61
18+10.75+10.75+10.75+10.75
```




    61.0




```python
cat4.codes
cat4.categories

cat4.value_counts()
pd.value_counts(cat4)
```




    (17.96, 28.75]    6
    (28.75, 39.5]     3
    (39.5, 50.25]     2
    (50.25, 61.0]     1
    dtype: int64



qcut根据样本分位数进行面元划分
===

某些数据分布情况cut可能无法使得各个面元含有相同数量的值

qcut使用样本分位数可以得到大小基本相等的面元


```python
cat5 = pd.qcut(ages, 4)
cat5
```




    [(17.999, 22.75], (17.999, 22.75], (22.75, 29.0], (22.75, 29.0], (17.999, 22.75], ..., (29.0, 38.0], (38.0, 61.0], (38.0, 61.0], (38.0, 61.0], (29.0, 38.0]]
    Length: 12
    Categories (4, interval[float64]): [(17.999, 22.75] < (22.75, 29.0] < (29.0, 38.0] < (38.0, 61.0]]




```python
cat5.value_counts()
```




    (17.999, 22.75]    3
    (22.75, 29.0]      3
    (29.0, 38.0]       3
    (38.0, 61.0]       3
    dtype: int64



### 手输入4分位数，效果一样


```python
cat6 = pd.qcut(ages, [0,0.25,0.5,0.75,1])
cat6
```




    [(17.999, 22.75], (17.999, 22.75], (22.75, 29.0], (22.75, 29.0], (17.999, 22.75], ..., (29.0, 38.0], (38.0, 61.0], (38.0, 61.0], (38.0, 61.0], (29.0, 38.0]]
    Length: 12
    Categories (4, interval[float64]): [(17.999, 22.75] < (22.75, 29.0] < (29.0, 38.0] < (38.0, 61.0]]




```python
cat6.value_counts()
```




    (17.999, 22.75]    3
    (22.75, 29.0]      3
    (29.0, 38.0]       3
    (38.0, 61.0]       3
    dtype: int64




```python
cat6.codes
cat6.categories
```




    IntervalIndex([(17.999, 22.75], (22.75, 29.0], (29.0, 38.0], (38.0, 61.0]]
                  closed='right',
                  dtype='interval[float64]')




-----

分位数和桶分析
===
pandas有一些能根据指定面元或样本分位数将数据拆分成多块的工具（比如cut和qcut）

将这些函数跟groupby结合起来，就能实现对数据集的桶（bucket）或分位数（quantile）分析

以下面这个简单的随机数据集为例，利用cut将其装入长度相等的桶中：



```python
frame = pd.DataFrame({'data1': np.random.randn(1000), 'data2': np.random.randn(1000)})
frame.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.729160</td>
      <td>-0.663376</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.150007</td>
      <td>-1.163234</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.538154</td>
      <td>0.079294</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.682866</td>
      <td>-0.822573</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.835660</td>
      <td>1.303850</td>
    </tr>
  </tbody>
</table>
</div>




```python
q = pd.cut(frame['data1'], 4)
q.head()
```




    0    (-0.849, 1.075]
    1    (-0.849, 1.075]
    2     (1.075, 2.999]
    3    (-0.849, 1.075]
    4    (-0.849, 1.075]
    Name: data1, dtype: category
    Categories (4, interval[float64]): [(-4.704, -2.773] < (-2.773, -0.849] < (-0.849, 1.075] < (1.075, 2.999]]




```python
q.value_counts()
```




    (-0.849, 1.075]     681
    (-2.773, -0.849]    171
    (1.075, 2.999]      145
    (-4.704, -2.773]      3
    Name: data1, dtype: int64



由cut返回的Categorical对象可直接传递到groupby。我们可以像下面这样对data2列做一些统计计算


```python
frame.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1000.000000</td>
      <td>1000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.028416</td>
      <td>-0.022330</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.990060</td>
      <td>0.991433</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-4.696589</td>
      <td>-3.460825</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.608515</td>
      <td>-0.679791</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.002681</td>
      <td>-0.040999</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.665544</td>
      <td>0.625577</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2.998972</td>
      <td>3.163675</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.groupby(q).size()

```




    data1
    (-4.704, -2.773]      3
    (-2.773, -0.849]    171
    (-0.849, 1.075]     681
    (1.075, 2.999]      145
    dtype: int64




```python
frame.groupby(q)['data2'].size()
```




    data1
    (-4.704, -2.773]      3
    (-2.773, -0.849]    171
    (-0.849, 1.075]     681
    (1.075, 2.999]      145
    Name: data2, dtype: int64




```python
frame.groupby(q).sum()
frame.groupby(q)['data2'].sum()
```




    data1
    (-4.704, -2.773]     1.634495
    (-2.773, -0.849]    -2.891152
    (-0.849, 1.075]    -25.292079
    (1.075, 2.999]       4.219041
    Name: data2, dtype: float64



使用自定义函数同时计算多个指标,快速综合统计

自定义函数内构建字典或Series数据返回，会输出DataFrame


```python
def aaa(x):
#     return {
#         'count': x.count(),
#         'mean': x.mean(),
#         'std': x.std(),
#         'min': x.min(),
#         'max': x.max(),
#     }
    return pd.Series([x.count(), x.mean(), x.std(), x.min(), x.max()], index=['count', 'mean', 'std', 'min', 'max'])

frame.groupby(q)['data2'].apply(aaa)
frame.groupby(q)['data2'].apply(aaa).unstack()
frame.groupby(q)['data2'].apply(aaa).unstack().T
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>data1</th>
      <th>(-4.704, -2.773]</th>
      <th>(-2.773, -0.849]</th>
      <th>(-0.849, 1.075]</th>
      <th>(1.075, 2.999]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.000000</td>
      <td>171.000000</td>
      <td>681.000000</td>
      <td>145.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.544832</td>
      <td>-0.016907</td>
      <td>-0.037140</td>
      <td>0.029097</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.204511</td>
      <td>0.892292</td>
      <td>1.016679</td>
      <td>0.993543</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.422128</td>
      <td>-3.014230</td>
      <td>-3.460825</td>
      <td>-2.698864</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.780919</td>
      <td>2.251479</td>
      <td>3.163675</td>
      <td>2.439298</td>
    </tr>
  </tbody>
</table>
</div>



-------

计算指标/哑变量
===

一种常用于统计建模或机器学习的转换方式是：将分类变量（categorical variable）转换为 哑变量、指标矩阵（虚拟变量，独热（one-hot）编码变量）

如果DataFrame的某一列含有k个不同的值，则可以派生出一个k列矩阵或DataFrame（其值全为1和0）

pandas有一个get_dummies函数可以实现该功能

## 独热编码的作用：将不能计算的字符串转为可以计算的数值（表格，或矩阵）
字符串：'一个对统计应用有用的方法：结合get_dummies和如cut之类的离散化函数'

[统计,应用,有用,方法,结合,离散化,函数]
[1,1,1,1,1,1,1]

统计：[1,0,0,0,0,0,0]
方法：[0,0,0,1,0,0,0]


```python
df = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'b'], 'data1': range(6)})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>data1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>a</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['key']
```




    0    b
    1    b
    2    a
    3    c
    4    a
    5    b
    Name: key, dtype: object



### 手动转为独热编码

    [a,b,c]
    [1,1,1]

    a: [1,0,0]
    b: [0,1,0]
    c: [0,0,1]



```python
pd.get_dummies(df['key'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



合并两个表格


```python
dummies = pd.get_dummies(df['key'], prefix='key')
dummies
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key_a</th>
      <th>key_b</th>
      <th>key_c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>data1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>a</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
dummies
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key_a</th>
      <th>key_b</th>
      <th>key_c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.join(dummies)  #合并
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>data1</th>
      <th>key_a</th>
      <th>key_b</th>
      <th>key_c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>a</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b</td>
      <td>5</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



例子：将一组数据转为哑变量
===

一个对统计应用有用的方法：结合get_dummies 和如 cut 之类的离散化函数


```python
# 生成随机数据
np.random.seed(12345)
values = np.random.rand(10)
values
```




    array([0.92961609, 0.31637555, 0.18391881, 0.20456028, 0.56772503,
           0.5955447 , 0.96451452, 0.6531771 , 0.74890664, 0.65356987])



面元划分


```python
bins = [0, 0.2, 0.4, 0.6, 0.8, 1]
x = pd.cut(values, bins)
x
```




    [(0.8, 1.0], (0.2, 0.4], (0.0, 0.2], (0.2, 0.4], (0.4, 0.6], (0.4, 0.6], (0.8, 1.0], (0.6, 0.8], (0.6, 0.8], (0.6, 0.8]]
    Categories (5, interval[float64]): [(0.0, 0.2] < (0.2, 0.4] < (0.4, 0.6] < (0.6, 0.8] < (0.8, 1.0]]




```python
x.categories
```




    IntervalIndex([(0.0, 0.2], (0.2, 0.4], (0.4, 0.6], (0.6, 0.8], (0.8, 1.0]]
                  closed='right',
                  dtype='interval[float64]')




```python
x.codes
```




    array([4, 1, 0, 1, 2, 2, 4, 3, 3, 3], dtype=int8)



将面元划分结构进行独热编码(哑变量)


```python
pd.get_dummies(x)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>(0.0, 0.2]</th>
      <th>(0.2, 0.4]</th>
      <th>(0.4, 0.6]</th>
      <th>(0.6, 0.8]</th>
      <th>(0.8, 1.0]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
values
```




    array([0.92961609, 0.31637555, 0.18391881, 0.20456028, 0.56772503,
           0.5955447 , 0.96451452, 0.6531771 , 0.74890664, 0.65356987])


