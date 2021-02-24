
Pandas数据运算
===

---


```python
import numpy as np
import pandas as pd
```


```python
# 数据
a = pd.Series([9,8,7,6],index=['a','b','c','d'])
a
```




    a    9
    b    8
    c    7
    d    6
    dtype: int64




```python
b = pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



python科学计算的基本方式是：向量化运算（矢量化运算），并行运算

自定义运算
===
* Series
    * map()
* DataFrame
    * apply()
    * applymap()
    
    
* 如果Pandas库自带的运算和函数不满足需求，可以自定义函数，并同时将函数应用到Pandas的每行／列或值上
* 应用函数主要用于替代传统的for循环

针对Series的map函数，会将自定义函数应用到Series对象的每个值



## Series 的map函数


```python
a
```




    a    9
    b    8
    c    7
    d    6
    dtype: int64




```python
# 自定义运算函数
def xxx(x):
    return x + 1 - 2 * 3 / 4

#向量化运算
a.map(xxx)
```




    a    8.5
    b    7.5
    c    6.5
    d    5.5
    dtype: float64




```python
9 + 1 - 2 * 3 / 4
```




    8.5




DataFrame的自定义函数操作
---


apply:操作 行、列

applymap：操作单元格


```python
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 自定义运算函数
# def yyy(x):
#     return x + 1 - 2 * 3 / 4

#lambda 表达式(匿名函数)
yyy = lambda x:x + 1 - 2 * 3 / 4

b.apply(yyy)
b.applymap(yyy)
#直接应用于单元格的算法，两个函数效果一样
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>-0.5</td>
      <td>0.5</td>
      <td>1.5</td>
      <td>2.5</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>a</th>
      <td>4.5</td>
      <td>5.5</td>
      <td>6.5</td>
      <td>7.5</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>9.5</td>
      <td>10.5</td>
      <td>11.5</td>
      <td>12.5</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>14.5</td>
      <td>15.5</td>
      <td>16.5</td>
      <td>17.5</td>
      <td>18.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
15 + 1 - 2 * 3 / 4
```




    14.5



不直接应用于单元格的算法



```python
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



## 关于行和列的思路

* axis = 0 按行操作
    * 给这一列的所有行，进行计算  （说白了就是axis代表的是列，但是计算里计算的是这一行。）
* axis =1 按列操作
    * 给这一行的所有列，进行运算


** DataFrame的apply自定义函数应用，复杂，重要**


```python
def zzz(x):
    
    return x.min()  #返回行、列的最小值

b.apply(zzz) # 默认按行操作，就是每一列的所有行上的数字。
b.apply(zzz,axis = 0)  #上面行的完整写法
```




    0    0
    1    1
    2    2
    3    3
    4    4
    dtype: int64




```python
b.apply(zzz,axis = 1) #按列操作  就是每一行的所有列。
```




    c     0
    a     5
    d    10
    b    15
    dtype: int64




```python
def zzz(x):
    return x.min(),x.max()

b.apply(zzz,axis=1)
```




    c      (0, 4)
    a      (5, 9)
    d    (10, 14)
    b    (15, 19)
    dtype: object




```python
def zzz(x):
#     return x.min(),x.max()

#输出DataFrame ******************************************

    return pd.Series([x.min(), x.max()], index = ['最小值', '最大值'])

b.apply(zzz,axis=1)
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
      <th>最小值</th>
      <th>最大值</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



----

基本统计函数
===

Pandas的统计运算方法，和Numpy基本一致

默认针对0轴（行）做运算，大部分函数可加参数 axis=1 改为对列运算


函数	| 解释
----- | -----
.describe()	| 针对0轴的统计汇总，计数/平均值/标准差/最小值/四分位数/最大值
.sum()	| 计算数据的总和,按0轴计算(各行计算),下同,要按列计算参数1
.count()	| 非NaN值数量
.mean() .median() .mode()	| 计算数据的算数平均值/中位数/众数
.var() .std()	| 计算数据的方差/标准差
.min() .max()	| 计算数据的最小值/最大值
.idxmin() .idxmax()	| 计算数据第一个最大值/最小值所在位置的索引，给索引或切片使用(自定义索引，排除null/NA等空值)


```python
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 求和
b.sum()  #按行求和
b.sum(axis = 0)  #这一列的所有行，求和
```




    0    30
    1    34
    2    38
    3    42
    4    46
    dtype: int64




```python
0 + 5 + 10 + 15
```




    30




```python
b.sum(axis=1)  #按列求和： 0 1 2 3 4 

#这一行的所有列，求和
```




    c    10
    a    35
    d    60
    b    85
    dtype: int64



求最小值，最大值的索引


```python
a
```




    a    9
    b    8
    c    7
    d    6
    dtype: int64




```python
a.argmin()  #即将被废弃，建议改用idxmin(),inxmax()
```

    D:\Anaconda\anaconda\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: 'argmin' is deprecated, use 'idxmin' instead. The behavior of 'argmin'
    will be corrected to return the positional minimum in the future.
    Use 'series.values.argmin' to get the position of the minimum now.
      """Entry point for launching an IPython kernel.
    




    'd'




```python
a.idxmax()
```




    'a'




```python
# dataframe
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
b.idxmin()  #求最小值的索引是啥
```




    0    c
    1    c
    2    c
    3    c
    4    c
    dtype: object




```python
b.idxmax(axis=1)  #求最大值的索引是啥
```




    c    4
    a    4
    d    4
    b    4
    dtype: int64



##### 快速综合统计指标


```python
a
```




    a    9
    b    8
    c    7
    d    6
    dtype: int64




```python
a.describe()
```




    count    4.000000
    mean     7.500000
    std      1.290994
    min      6.000000
    25%      6.750000
    50%      7.500000
    75%      8.250000
    max      9.000000
    dtype: float64




```python
type(a.describe())
```




    pandas.core.series.Series




```python
a.describe()['min']
```




    6.0




```python
b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
b.describe()
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.500000</td>
      <td>8.500000</td>
      <td>9.500000</td>
      <td>10.500000</td>
      <td>11.500000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.454972</td>
      <td>6.454972</td>
      <td>6.454972</td>
      <td>6.454972</td>
      <td>6.454972</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.750000</td>
      <td>4.750000</td>
      <td>5.750000</td>
      <td>6.750000</td>
      <td>7.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.500000</td>
      <td>8.500000</td>
      <td>9.500000</td>
      <td>10.500000</td>
      <td>11.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>11.250000</td>
      <td>12.250000</td>
      <td>13.250000</td>
      <td>14.250000</td>
      <td>15.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15.000000</td>
      <td>16.000000</td>
      <td>17.000000</td>
      <td>18.000000</td>
      <td>19.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(b.describe())  # df类型
```




    pandas.core.frame.DataFrame




```python
b.describe()[4]
```




    count     4.000000
    mean     11.500000
    std       6.454972
    min       4.000000
    25%       7.750000
    50%      11.500000
    75%      15.250000
    max      19.000000
    Name: 4, dtype: float64




```python
b.describe().loc[['min', 'max'],[0, 2, 4]]
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
      <th>0</th>
      <th>2</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>min</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15.0</td>
      <td>17.0</td>
      <td>19.0</td>
    </tr>
  </tbody>
</table>
</div>


