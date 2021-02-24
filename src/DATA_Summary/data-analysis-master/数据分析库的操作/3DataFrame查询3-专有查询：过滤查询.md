
DataFrame查询3-专有查询：过滤查询
===

---

索引查询和切片查询，都是通过索引来查询值

## 过滤查询（布尔查询）

通过值查询索引

通过列布尔值过滤、筛选查询


* 过滤查询不通过索引，而是通过值查询

* 用于结果索引不确定的查询

* 通过运算所得布尔值对查询结果进行过滤




```python
import numpy as np
import pandas as pd

```


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



类 列表/字典  查询方式


```python
a[['name','age']]
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
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 布尔查询应用到行
a[[True,False,True,True,False]]
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
  </tbody>
</table>
</div>



专有查询方式的布尔查询

过滤查询（布尔查询） 的原理

真正布尔查询时，布尔条件应该是自动生成的

查询多行多列


```python
a.loc[[1,3],['name','sex','address']]
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
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>广州天河</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 专有的布尔查询
a.loc[[True,False,True]]
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
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
  </tbody>
</table>
</div>




```python
a.loc[[True,False,True],[True,True,False,False,False,True]]
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
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>male</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>广州天河</td>
    </tr>
  </tbody>
</table>
</div>



# 自动生成布尔查询条件


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



# 栗子：输出所有考试不合格的同学的信息


```python
#查询所有同学的成绩列
a['grade']
```




    1    61
    2    74
    3    59
    4    82
    5    98
    Name: grade, dtype: int64




```python
a.loc[:,'grade']
```




    1    61
    2    74
    3    59
    4    82
    5    98
    Name: grade, dtype: int64




```python
# 向量化运算，生成布尔条件
a['grade'] < 60
```




    1    False
    2    False
    3     True
    4    False
    5    False
    Name: grade, dtype: bool




```python
a[a['grade']<60]  #等同于 a.loc[[True,False,True],[True,True,False,False,False,True]]
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
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
  </tbody>
</table>
</div>




```python
a.loc[a['grade']<60]
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
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
  </tbody>
</table>
</div>



### 将布尔查询和索引、切片查询结合


```python
a.loc[a['grade']<60, ['name','sex','grade','address']] 
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
      <th>grade</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>59</td>
      <td>广州天河</td>
    </tr>
  </tbody>
</table>
</div>



### isin 函数

判断某列是否存在某值


```python
a['address']
```




    1    北京海淀
    2    上海静安
    3    广州天河
    4    深圳南山
    5    杭州西湖
    Name: address, dtype: object




```python
x = a['address'].isin(['北京海淀','杭州西湖','加州硅谷'])
x
```




    1     True
    2    False
    3    False
    4    False
    5     True
    Name: address, dtype: bool




```python
a[x]
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



不用isin 原生布尔查询实现

### 逻辑运算

    & 且

    | 或

    - 非(或用 != 判断)


```python
a['address'] == '北京海淀'
a['address'] == '杭州西湖'
a['address'] == '加州硅谷'
```




    1    False
    2    False
    3    False
    4    False
    5    False
    Name: address, dtype: bool




```python
x2 = (a['address'] == '北京海淀') | (a['address'] == '杭州西湖') | (a['address'] == '加州硅谷')
x2
```




    1     True
    2    False
    3    False
    4    False
    5     True
    Name: address, dtype: bool




```python
a[x2]
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



### 栗子： 查询所有考试及格的女同学 



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




```python
a['sex'] == 'female'  #所有女同学
```




    1    False
    2     True
    3     True
    4    False
    5     True
    Name: sex, dtype: bool




```python
a['grade'] >= 60  # 所有考试及格的同学
```




    1     True
    2     True
    3    False
    4     True
    5     True
    Name: grade, dtype: bool




```python
x3 = (a['sex'] == 'female') & (a['grade'] >= 60)
a[x3]
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
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
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




```python
a.loc[x3,['name','heigh','address']]
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
      <th>heigh</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>160</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>165</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>



where 过滤
---


```python
a_values = [
    ['小明',True,18,170.7,60,'北京海淀',61],
    ['小华',True,28,160,50,'上海静安',74],
    ['小红',False,22,175,64,'广州天河',59],
    ['小靑',False,31,182,80,'深圳南山',35],
    ['小兰',False,25,165,55,'杭州西湖',98],
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
      <td>True</td>
      <td>18</td>
      <td>170.7</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>True</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>False</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>False</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>35</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>False</td>
      <td>25</td>
      <td>165.0</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



#### 原生布尔查询方式


```python
a[(a['sex'] == False) & (a['weight'] >= 60) & (a['grade'] >= 60)]  #没有符合条件的数据
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
  </tbody>
</table>
</div>




```python
a.loc[5,'weight'] = 65  #修改值
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
      <td>True</td>
      <td>18</td>
      <td>170.7</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>True</td>
      <td>28</td>
      <td>160.0</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>False</td>
      <td>22</td>
      <td>175.0</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>False</td>
      <td>31</td>
      <td>182.0</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>35</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>False</td>
      <td>25</td>
      <td>165.0</td>
      <td>65</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
a[(a['sex'] == False) & (a['weight'] >= 60) & (a['grade'] >= 60)]

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
      <th>5</th>
      <td>小兰</td>
      <td>False</td>
      <td>25</td>
      <td>165.0</td>
      <td>65</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



### where 过滤方式


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
      <td>65</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
a >= 60
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
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
a[a>=60]
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
      <td>NaN</td>
      <td>170</td>
      <td>60.0</td>
      <td>北京海淀</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>NaN</td>
      <td>160</td>
      <td>NaN</td>
      <td>上海静安</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>NaN</td>
      <td>175</td>
      <td>64.0</td>
      <td>广州天河</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>NaN</td>
      <td>182</td>
      <td>80.0</td>
      <td>深圳南山</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>NaN</td>
      <td>165</td>
      <td>NaN</td>
      <td>杭州西湖</td>
      <td>98.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
a[a>=60].info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 5 entries, 1 to 5
    Data columns (total 7 columns):
    name       5 non-null object
    sex        5 non-null object
    age        0 non-null float64
    heigh      5 non-null int64
    weight     3 non-null float64
    address    5 non-null object
    grade      4 non-null float64
    dtypes: float64(3), int64(1), object(3)
    memory usage: 480.0+ bytes
    


```python
b = a.loc[:, ['heigh','weight','grade']]
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
      <th>heigh</th>
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>170.7</td>
      <td>60</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>160.0</td>
      <td>50</td>
      <td>74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>175.0</td>
      <td>64</td>
      <td>59</td>
    </tr>
    <tr>
      <th>4</th>
      <td>182.0</td>
      <td>80</td>
      <td>35</td>
    </tr>
    <tr>
      <th>5</th>
      <td>165.0</td>
      <td>65</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
b >= 60
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
      <th>heigh</th>
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
b[b>= 60]
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
      <th>heigh</th>
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>170.7</td>
      <td>60.0</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>160.0</td>
      <td>NaN</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>175.0</td>
      <td>64.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>182.0</td>
      <td>80.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>165.0</td>
      <td>65.0</td>
      <td>98.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
b[b>=60].dropna()  #删除所有含有空值的行
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
      <th>heigh</th>
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>170.7</td>
      <td>60.0</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>165.0</td>
      <td>65.0</td>
      <td>98.0</td>
    </tr>
  </tbody>
</table>
</div>



---

总结：
---


* 原生的布尔查询，需要每列单独判断条件，然后用逻辑运算符组合条件，得出最终结果
* where 过滤：现将所有需要判断条件的列抽出来，整体判断，得出最终结果
    * where过滤所有列的判断条件，只能有一个，使用受限。
    * 书写简洁
    
优先使用where过滤，实现不了再用原生布尔查询。
