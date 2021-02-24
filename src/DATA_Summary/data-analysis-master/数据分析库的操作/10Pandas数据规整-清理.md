
数据规整（数据预处理，数据清洗）
---

数据规整的一般分类：

* 清理
* 转换
* 合并
* 重塑

---


Pandas数据规整-清理：
===

对指定数据（如缺失数据、重复数据）进行处理（检查、替换、删除）

* 缺失值的表示：np.nan
* 检查缺失值：isnull(),notnull(),info()
* 删除缺失值： dropna()
* 填充缺失值: fillna()
* 替换值（填充缺失值是替换值的一种情况）：replace().



```python
import pandas as pd
import numpy as np
```

Pandas缺失数据处理
===


缺失值表示


```python

a = np.array([2,4,8,10,12])
a
```




    array([ 2,  4,  8, 10, 12])




```python
a + 10
```




    array([12, 14, 18, 20, 22])



**python  原生缺失值表示：None**

缺失值元素导致计算报错


```python
b = np.array([2,4,None,10,12])
b
```




    array([2, 4, None, 10, 12], dtype=object)




```python
b + 10  #缺失值导致计算报错
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-16-c6d5a276d5e4> in <module>()
    ----> 1 b + 10  #缺失值导致计算报错
    

    TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'


### 使用Numpy的缺失值数据类型 ： np.nan

缺失值运算不会报错，和缺失值运算，结果还是缺失值


```python
c = np.array([2,4,np.nan,10,12])
c
```




    array([ 2.,  4., nan, 10., 12.])




```python
c + 10  #计算时不会报错
```




    array([12., 14., nan, 20., 22.])




```python

c.sum()  #任何数组和缺失值计算，结果还是缺失值
```




    nan




```python
np.sum(c)
```




    nan



nan专有运算方法，会跳过缺失值，直接计算正常值


```python
np.nansum(c)
```




    28.0



### 使用Pandas缺失值 计算
Pandas中，不论缺失值是None 还是np.nan,都会被转化为NaN的形式

NaN：非数字，not a number, Pandas 中它表示缺失或NA值，便于被检测出来。

本质上就是np.nan。

pandas 对象可以跳过缺失值直接进行运算

跳过缺失值直接运算


```python
d = pd.Series([2,4,np.nan,8,None,12])
d
```




    0     2.0
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
d + 10
```




    0    12.0
    1    14.0
    2     NaN
    3    18.0
    4     NaN
    5    22.0
    dtype: float64




```python
d.sum() / 4
```




    6.5




```python
d.mean()
```




    6.5




```python
d[0] = np.nan
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python

c = pd.DataFrame([[1,np.nan,3], [4,5,6], [np.nan, 8,9]])
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.sum()
```




    0     5.0
    1    13.0
    2    18.0
    dtype: float64



### 通过函数检查数据中是否有缺失值


```python
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3 entries, 0 to 2
    Data columns (total 3 columns):
    0    2 non-null float64
    1    2 non-null float64
    2    3 non-null int64
    dtypes: float64(2), int64(1)
    memory usage: 152.0 bytes
    

isnull() 和 notnull()
* isnull():缺失值返回True，正常值返回False
* notnull():正常值返回True，缺失值返回False


```python
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
d.isnull()  #缺失值返回True
```




    0     True
    1    False
    2     True
    3    False
    4     True
    5    False
    dtype: bool




```python
-(d.isnull())  # 非运算
```




    0    False
    1     True
    2    False
    3     True
    4    False
    5     True
    dtype: bool




```python
d.notnull()  #缺失值返回False
```




    0    False
    1     True
    2    False
    3     True
    4    False
    5     True
    dtype: bool



返回所有正常值

手动过滤Series 的缺失值



```python
d[d.notnull()]
```




    1     4.0
    3     8.0
    5    12.0
    dtype: float64




DataFrame 不能通过布尔查询方式过滤缺失值，必须使用Pandas的待定方法过滤

查到缺失值后，Series 可以直接过滤，DataFrame需要进一步处理


```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c[c.notnull()]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c[c.isnull()]  #  是空值的 返回 true  不是空的 是 False，然后 布尔查询以后b ， 是空值的 那么数据就是Nan，而不是空值的返回的是Nan。
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 去除缺失值，只保留有效值

dropna() 函数


```python
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
d.dropna()
```




    1     4.0
    3     8.0
    5    12.0
    dtype: float64




```python
# 等同于
d[d.notnull()]
```




    1     4.0
    3     8.0
    5    12.0
    dtype: float64




```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.dropna()  #默认删除缺失值所在行

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.dropna(axis=0)  #默认删除缺失值所在行
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.dropna(axis=1)  #按列删除
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
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
#增加一列 全部为缺失值的数据
c[3] = np.nan
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 行或 列， 有1 个缺失值即删除
c.dropna(axis=1)
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
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
#等同
c.dropna(axis=1, how='any')
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
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.dropna(axis=1, how='all')  # 行或列必须全部都是缺失值才删
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



### 根据行或列的非缺失值数量衡量删除与否


```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.dropna()
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
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
c.dropna(thresh=3)  # 行非缺失值数量大于等于3个，保留
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 填充缺失值¶

缺失值问题除了删除所在行列以外，还可以通过填充值解决

fillna()函数参数


```python
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
d.fillna(0)   # 缺失值填充0
```




    0     0.0
    1     4.0
    2     0.0
    3     8.0
    4     0.0
    5    12.0
    dtype: float64




```python
d.fillna(d.mean())  #填充均值

```




    0     8.0
    1     4.0
    2     8.0
    3     8.0
    4     8.0
    5    12.0
    dtype: float64



### 前向填充和后向填充¶

method='ffill'

method='bfill'


```python
d
```




    0     NaN
    1     4.0
    2     NaN
    3     8.0
    4     NaN
    5    12.0
    dtype: float64




```python
d.fillna(0)
```




    0     0.0
    1     4.0
    2     0.0
    3     8.0
    4     0.0
    5    12.0
    dtype: float64



### 前向填充：使用缺失值的前一个值填充


```python
d.fillna(method='ffill')
```




    0     NaN
    1     4.0
    2     4.0
    3     8.0
    4     8.0
    5    12.0
    dtype: float64



### 后向填充，使用缺失值的后一个值填充


```python
d.fillna(method='bfill')
```




    0     4.0
    1     4.0
    2     8.0
    3     8.0
    4    12.0
    5    12.0
    dtype: float64




```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(method='ffill')  # 前向填充，按行
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.0</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(axis=1, method='ffill')  # 前向填充，按列
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(axis=1, method='ffill')  # 前向填充，按列
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>



给各列分布填充不同值


```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna({0:100, 1:200,3:300})
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>200.0</td>
      <td>3</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100.0</td>
      <td>8.0</td>
      <td>9</td>
      <td>300.0</td>
    </tr>
  </tbody>
</table>
</div>



上面一切删除，填充操作都没有修改原变量

修改原变量：inplace = True


```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(100,inplace=True)

```


```python
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>100.0</td>
      <td>3</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>5.0</td>
      <td>6</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100.0</td>
      <td>8.0</td>
      <td>9</td>
      <td>100.0</td>
    </tr>
  </tbody>
</table>
</div>



连续填充数量


```python
c.loc[3] = np.nan
c.loc[0,1] = np.nan
c.loc[1:3,0] = np.nan
c[3] = np.nan
c
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(method='ffill')  #默认全部填充
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.fillna(method='ffill', limit=2)  # 设置填充多少行或列
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



替换值
===

利用fillna方法填充缺失数据是值替换的一种特殊情况， replace方法用作替换值更简单、更灵活


```python
data = pd.Series([1,-999,2,-999,-1000,3])
data
```




    0       1
    1    -999
    2       2
    3    -999
    4   -1000
    5       3
    dtype: int64




```python
# 替换单值
data.replace(-999, np.nan)
```




    0       1.0
    1       NaN
    2       2.0
    3       NaN
    4   -1000.0
    5       3.0
    dtype: float64




```python
# 替换多值
data.replace([-999, -1000], np.nan)
```




    0    1.0
    1    NaN
    2    2.0
    3    NaN
    4    NaN
    5    3.0
    dtype: float64




```python
# 多个值替换为不同数值
data.replace([-999, -1000], [0, 1])
data.replace({-999: 0, -1000: 1})
```




    0    1
    1    0
    2    2
    3    0
    4    1
    5    3
    dtype: int64



### 映射数据替换

map除了自定义函数运算，还是一种映射转换元素以及其他数据清理工作的便捷方式


```python
a = pd.DataFrame([['鬃刷','皮带','煎蛋','观赏'], [10,20,30,40]]).T
a
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>鬃刷</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>皮带</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>煎蛋</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>观赏</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>




```python
y = {'鬃刷': '猪', '皮带': '牛', '观赏': '鱼', '衣服': '棉花'}
```


```python
a[0].map(y)
```




    0      猪
    1      牛
    2    NaN
    3      鱼
    Name: 0, dtype: object


