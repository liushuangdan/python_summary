
DataFrame查询1-整体
---

---


```python
import numpy as np
import pandas as pd
```

数据


```python
a = pd.DataFrame([
    ['小明','male',18,170,60,'北京海淀',61],
    ['小华','female',28,160,50,'上海静安',74],
    ['小红','female',22,175,64,'广州天河',59],
    ['小靑','male',31,182,80,'深圳南山',82],
    ['小兰','female',25,165,55,'杭州西湖',98],
],
     index=[1,2,3,4,5],
    columns=['name','sex','age','heigh','weight','address','grade']
)
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



## 查询

### 常用属性

a.shape  # 表格形状 行数 列数

a.dtypes  # 列数据类型

a.index  # 行索引

a.columns  # 列索引

a.values  # 对象值，二维ndarray数组




### 表格形状（几行几列）


```python
a.shape
```




    (5, 7)



### 数据类型


```python
a.dtypes
```




    name        object
    sex         object
    age          int64
    heigh      float64
    weight       int64
    address     object
    grade        int64
    dtype: object




```python
a.shape[0],a.shape[1]
```




    (5, 7)



数据


```python
a_values = [
    ['小明','male',18,170.0,60,'北京海淀',61],  #如果身高这一列 一个数据改为浮点型，那么整列的数据类型都会被影响为浮点型。
    ['小华','female',28,160,50,'上海静安',74],
    ['小红','female',22,175,64,'广州天河',59],
    ['小靑','male',31,182,80,'深圳南山',82],
    ['小兰','female',25,165,55,'杭州西湖',98],
]

a = pd.DataFrame(
    a_values,
    index=[1,2,3,4,5],
    columns=['name','sex','age','heigh','weight','address','grade']
)
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165.0</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



表格值


```python

a.values  #二维数组

```




    array([['小明', 'male', 18, 170.0, 60, '北京海淀', 61],
           ['小华', 'female', 28, 160.0, 50, '上海静安', 74],
           ['小红', 'female', 22, 175.0, 64, '广州天河', 59],
           ['小靑', 'male', 31, 182.0, 80, '深圳南山', 82],
           ['小兰', 'female', 25, 165.0, 55, '杭州西湖', 98]], dtype=object)




```python
a.values[0]
```




    array(['小明', 'male', 18, 170.0, 60, '北京海淀', 61], dtype=object)




```python
a.values[0][0]
```




    '小明'



表格的行索引


```python
a.index
a.index.values
```




    array([1, 2, 3, 4, 5], dtype=int64)




```python
type(a.index),type(a.index.values)
```




    (pandas.core.indexes.numeric.Int64Index, numpy.ndarray)



表格列索引


```python
a.columns
```




    Index(['name', 'sex', 'age', 'heigh', 'weight', 'address', 'grade'], dtype='object')




```python
a.columns.values
```




    array(['name', 'sex', 'age', 'heigh', 'weight', 'address', 'grade'],
          dtype=object)




```python
a.columns.values[0]
```




    'name'



## 整体数据情况

* a.info() 整体信息，查看数据是否异常
* a,describe() 整体统计指标
* a.head()前5行
* a.taill() 后5行



```python
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165.0</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



表格整体信息，一般用于查看表格数据是否有异常
* 是否有缺失值
* 列表数据类型是否正常


```python
a.info()   #可以看出列的数据有没有缺失，根据结果来补全数据。
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 5 entries, 1 to 5
    Data columns (total 7 columns):
    name       5 non-null object
    sex        5 non-null object
    age        5 non-null int64
    heigh      5 non-null float64
    weight     5 non-null int64
    address    5 non-null object
    grade      5 non-null int64
    dtypes: float64(1), int64(3), object(3)
    memory usage: 320.0+ bytes
    

### 表格快速综合统计指标

用来查看数据的整体统计情况

* count，计数

* mean 平均值

* std 标准差

* 四分位数
   四分位数（Quartile）也称四分位点，是指在统计学中把所有数值由小到大排列并分成四等份，处于三个分割点位置的数值
   
    * min 最小值，q1(指处在25%位置上的数值),q2(中位数),q3(指处在75%位置上的数值),max 最大值



```python
a.describe()
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
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>24.800000</td>
      <td>170.400000</td>
      <td>61.800000</td>
      <td>74.800000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.069517</td>
      <td>8.561542</td>
      <td>11.454257</td>
      <td>16.053037</td>
    </tr>
    <tr>
      <th>min</th>
      <td>18.000000</td>
      <td>160.000000</td>
      <td>50.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>22.000000</td>
      <td>165.000000</td>
      <td>55.000000</td>
      <td>61.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>25.000000</td>
      <td>170.000000</td>
      <td>60.000000</td>
      <td>74.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>28.000000</td>
      <td>175.000000</td>
      <td>64.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>31.000000</td>
      <td>182.000000</td>
      <td>80.000000</td>
      <td>98.000000</td>
    </tr>
  </tbody>
</table>
</div>



#### std： 标准差 ： 

    所有数减去其平均值的平方和，所得结果除以该组数之个数（或个数减一，即变异数），再把所得值开根号，所得之数就是这组数据的标准差。
    
    标准差是反映一组数据离散程度最常用的一种量化形式，是表示精确度的重要指标。

输出表格的前5行


```python
a.head()
a.head(3)
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
  </tbody>
</table>
</div>



输出表格的后5行


```python
a.tail()
a.tail(3)
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165.0</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



## 内容查询
 ### 类列表/字典/ndarray数组的查询方式


```python
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165.0</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



 查询单列


```python
a['name']
```




    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object



查询多列


```python
a[['name','address']]
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
      <th>name</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>深圳南山</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>



查询单行


```python
a[0:1]
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
  </tbody>
</table>
</div>



查询多行



```python
a[1:3]
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
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
  </tbody>
</table>
</div>



查询单值


```python
a[0:1]['name']
```




    1    小明
    Name: name, dtype: object




```python
a['name'][0:1]
```




    1    小明
    Name: name, dtype: object


