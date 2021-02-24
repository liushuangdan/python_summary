
Pandas 对象的数据操作：增删改查
===

---


#### 数据操作

* 创建：C,Create
* 查询：R,Read
* 增加：I,Insert
* 修改：U,Update
* 删除：D,Delete


```python
import numpy as np
import pandas as pd
```


```python
# 创建对象
a_values = [
    ['小明','male',18,170,60,'北京海淀',61],
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



DadaFrame 对象 的修改的视图和副本问题
===

* 视图模式
    * 讲一个对象整体赋值给另一个变量
    * 修改一个变量，另一个变量值也会变
    * 对个变量数据指向同一个内存数据
    
* 副本模式
    * 将一个对象查询的一部分值赋值给另一个变量
    * 修改一个变量，另一个变量值不会变
     

 当将一个对象整体赋值给另一个变量时，**视图模式**，两个变量对应的内存地址相同，修改一个变量，另一个变量也会改变。
 
 或者使用查询赋值，查询数据的一部分并赋值给其他变量
 
 * 当赋值为原数据查询的一部分时，是**副本模式**，修改一个变量不会影响另一个 变量


```python
a.loc[1,'name']#查询
```




    '小明'




```python
a.loc[1,'name'] = '小明明'
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
      <td>小明明</td>
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



#### 视图模式



```python
b = a #将a 赋值给b
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
      <td>小明明</td>
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
b.loc[1,'name']
```




    '小明明'




```python
b.loc[1,'name'] = '大明明xxx'
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
      <td>大明明xxx</td>
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
      <td>大明明xxx</td>
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



### 使用.copy()函数实现对象的内存副本


```python
c = a.copy()
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
      <td>大明明xxx</td>
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
c.loc[1,'name'] = 'xxxx' #副本模式，完全复制
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
      <td>xxxx</td>
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
      <td>大明明xxx</td>
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



### 副本模式


```python
c = a.loc[:, ['name','sex','address']]
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
      <th>name</th>
      <th>sex</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>male</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>深圳南山</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.loc[1,'name'] = '小明yyy'
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
      <th>name</th>
      <th>sex</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明yyy</td>
      <td>male</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>female</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>深圳南山</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>




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
      <td>大明明xxx</td>
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



---

Series数据操作
===


创建


```python
d = pd.Series([3,5,8,12,14])
d
```




    0     3
    1     5
    2     8
    3    12
    4    14
    dtype: int64



查询


```python
d[2] #索引查询
```




    8




```python
d[1:3]  #切片查询
```




    1    5
    2    8
    dtype: int64




```python
# 布尔查询
d[d>10]
```




    3    12
    4    14
    dtype: int64




```python
#查询索引和值
d.index
```




    RangeIndex(start=0, stop=5, step=1)




```python
d.values
```




    array([ 3,  5,  8, 12, 14], dtype=int64)



增加


```python
d[5] = 100
d
```




    0      3
    1      5
    2      8
    3     12
    4     14
    5    100
    dtype: int64




```python
d['aaa']='bbb'
d
```




    0        3
    1        5
    2        8
    3       12
    4       14
    5      100
    aaa    bbb
    dtype: object



不同数据类型强制统一时候，只能保存为占用内存最大的数据类型


```python
[True, 18, 175.1, '小明']
```




    [True, 18, 175.1, '小明']



修改


```python
d[0] = 30
d
```




    0       30
    1        5
    2        8
    3       12
    4       14
    5      100
    aaa    bbb
    dtype: object



删除

删除功能等同于查询数据时跳过被删除数据


```python
d.drop(0)  # 删除视图,没有真的删除原数据
```




    1        5
    2        8
    3       12
    4       14
    5      100
    aaa    bbb
    dtype: object




```python
d  # 原数据不变
```




    0       30
    1        5
    2        8
    3       12
    4       14
    5      100
    aaa    bbb
    dtype: object



DataFrame数据操作
---

创建（略）


```python
e = a.copy()  # 副本
e
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
      <td>大明明xxx</td>
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



查询


```python
# 整体查询
e.index
e.columns
e.values

e.info()
e.describe()
e.head()
e.tail(3)
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 5 entries, 1 to 5
    Data columns (total 7 columns):
    name       5 non-null object
    sex        5 non-null object
    age        5 non-null int64
    heigh      5 non-null int64
    weight     5 non-null int64
    address    5 non-null object
    grade      5 non-null int64
    dtypes: int64(4), object(3)
    memory usage: 320.0+ bytes
    




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
e.loc[[3, 5], ['name', 'address']]  # 索引查询

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
      <th>3</th>
      <td>小红</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>




```python
e.loc[3:5, 'name':'address']  # 切片查询

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
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>




```python
e.loc[e['grade'] > 60, ['name', 'age', 'weight', 'grade']]  # 行，布尔查询；列，索引查询
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
      <th>weight</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>18</td>
      <td>60</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>28</td>
      <td>50</td>
      <td>74</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>31</td>
      <td>80</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>25</td>
      <td>55</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



增加




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
      <td>大明明xxx</td>
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



增加行、列的代码不能反复执行，因为加了后表格行列长度会变


```python
# 增加行
e.loc['6'] = 0
e
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
      <th>phone</th>
      <th>qq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
      <td>818414</td>
      <td>111</td>
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
      <td>818414</td>
      <td>22</td>
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
      <td>818414</td>
      <td>333</td>
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
      <td>818414</td>
      <td>444</td>
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
      <td>818414</td>
      <td>555</td>
    </tr>
    <tr>
      <th>xxx</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>818414</td>
      <td>666</td>
    </tr>
    <tr>
      <th>yyy</th>
      <td>张三</td>
      <td>female</td>
      <td>35</td>
      <td>155.5</td>
      <td>60</td>
      <td>加州硅谷</td>
      <td>100</td>
      <td>818414</td>
      <td>888888</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
e.loc['7'] = ['张三', 'female', 35, 155.5, 60, '加州硅谷', 100, 818414,6666]
e
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
      <th>phone</th>
      <th>qq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
      <td>818414</td>
      <td>111</td>
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
      <td>818414</td>
      <td>22</td>
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
      <td>818414</td>
      <td>333</td>
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
      <td>818414</td>
      <td>444</td>
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
      <td>818414</td>
      <td>555</td>
    </tr>
    <tr>
      <th>xxx</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>818414</td>
      <td>666</td>
    </tr>
    <tr>
      <th>yyy</th>
      <td>张三</td>
      <td>female</td>
      <td>35</td>
      <td>155.5</td>
      <td>60</td>
      <td>加州硅谷</td>
      <td>100</td>
      <td>818414</td>
      <td>888888</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>张三</td>
      <td>female</td>
      <td>35</td>
      <td>155.5</td>
      <td>60</td>
      <td>加州硅谷</td>
      <td>100</td>
      <td>818414</td>
      <td>6666</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 增加列
e['phone'] = 818414
e

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
      <th>phone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
      <td>818414</td>
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
      <td>818414</td>
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
      <td>818414</td>
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
      <td>818414</td>
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
      <td>818414</td>
    </tr>
    <tr>
      <th>xxx</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>818414</td>
    </tr>
    <tr>
      <th>yyy</th>
      <td>张三</td>
      <td>female</td>
      <td>35</td>
      <td>155.5</td>
      <td>60</td>
      <td>加州硅谷</td>
      <td>100</td>
      <td>818414</td>
    </tr>
  </tbody>
</table>
</div>




```python
e['qq'] = [111,22,333,444,555,666,888888]
e
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
      <th>phone</th>
      <th>qq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>大明明xxx</td>
      <td>male</td>
      <td>18</td>
      <td>170.0</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
      <td>818414</td>
      <td>111</td>
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
      <td>818414</td>
      <td>22</td>
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
      <td>818414</td>
      <td>333</td>
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
      <td>818414</td>
      <td>444</td>
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
      <td>818414</td>
      <td>555</td>
    </tr>
    <tr>
      <th>xxx</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>818414</td>
      <td>666</td>
    </tr>
    <tr>
      <th>yyy</th>
      <td>张三</td>
      <td>female</td>
      <td>35</td>
      <td>155.5</td>
      <td>60</td>
      <td>加州硅谷</td>
      <td>100</td>
      <td>818414</td>
      <td>888888</td>
    </tr>
  </tbody>
</table>
</div>



修改


```python
f = a.copy()
f
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
      <td>大明明xxx</td>
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
f.loc[[1,3,5],['name','address']]
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
      <td>大明明xxx</td>
      <td>北京海淀</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>杭州西湖</td>
    </tr>
  </tbody>
</table>
</div>




```python
f.loc[[1,3,5],['name','address']] = 0
f
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
      <td>0</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>0</td>
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
      <td>0</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>0</td>
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
      <td>0</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>0</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
f.loc[[1,3,5],['name','address']]
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
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame([[1,2],[3,4],[5,6]])
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
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
# f.loc[[1,3,5],['name','address']] = [[1,2,3],[4,5]]  # 错误修改，值应该和查询数据形状相同
f.loc[[1,3,5],['name','address']] = [[1,2],[3,4],[5,6]]  # 3行两列
f
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
      <td>1</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>2</td>
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
      <td>3</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>4</td>
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
      <td>5</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>6</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>



删除
* 删除基本等同于简单版的查询
* 默认不修改原值，值输出删除后的数据，真删除加参数

inplace = True

* 默认的参数： axis = 0 删除行，改为 axis = 1 删除列


```python
# 删除行
f.drop(2)  # 假删除
f.drop(2, axis=0)  # 完整写法
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
      <td>1</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>2</td>
      <td>61</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>4</td>
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
      <td>5</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>6</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
f  # 原值不变
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
      <td>1</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>2</td>
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
      <td>3</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>4</td>
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
      <td>5</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>6</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 真删
f.drop(3, inplace=True)  # 删除原值
```


```python
f
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
      <td>1</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>2</td>
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
      <td>5</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>55</td>
      <td>6</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 删除列
f.drop(['weight'], axis=1)
f.drop(['weight', 'grade'], axis=1)
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
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182</td>
      <td>深圳南山</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>female</td>
      <td>25</td>
      <td>165</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>


