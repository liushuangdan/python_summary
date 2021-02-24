
Pandas数据操作：其他操作
===

---

* Pandas对象的命名：name
* Pandas对象的遍历

Pandas对象的命名：name
---

Series 和 DataFrame 对象本身，索引都可以命名


```python
import numpy as np
import pandas as pd
```

Series 的name命名
===


```python
a = pd.Series([3,5,8,12,14])
a
```




    0     3
    1     5
    2     8
    3    12
    4    14
    dtype: int64




```python
a.name  # 默认没有name 属性
a.name = '张三'   # 列索引命名
a.name
```




    '张三'




```python
a
```




    0     3
    1     5
    2     8
    3    12
    4    14
    Name: 张三, dtype: int64



## Series的命名


```python
# Series 索引命名


a.index.name 
a.index.name = 'aaa'   #行索引命名
a.index
```




    RangeIndex(start=0, stop=5, step=1, name='aaa')




```python
a
```




    aaa
    0     3
    1     5
    2     8
    3    12
    4    14
    Name: 张三, dtype: int64



Series 命名的用处


```python
a2 = pd.Series([2,3,4,5,6])
a2
```




    0    2
    1    3
    2    4
    3    5
    4    6
    dtype: int64




```python
pd.DataFrame(a2)    # Series 变成 DataFrame 的一列，行索引就是s的索引，列索引就是D的自增索引
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
a
```




    aaa
    0     3
    1     5
    2     8
    3    12
    4    14
    Name: 张三, dtype: int64




```python
pd.DataFrame(a)
#列索引是Series 的命名

# 行索引也有名字：Serise 的index 命名

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
      <th>张三</th>
    </tr>
    <tr>
      <th>aaa</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



DataFrame的命名
===

层次化索引


```python
av = [
    ['小明','male',18,170,60,'北京海淀',61],
    ['小华','female',28,160,50,'上海静安',74],
    ['小红','female',22,175,64,'广州天河',59],
    ['小靑','male',31,182,80,'深圳南山',82],
    ['小兰','female',25,165,55,'杭州西湖',98],
]
b = pd.DataFrame(
    av,
    index=[1,2,3,4,5],
    columns=['name','sex','age','heigh','weight','address','grade']
)
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
# 行索引命名 

b.index.name 
b.index.name = '学号'
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
      <th>属性</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
    <tr>
      <th>学号</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
# 列索引命名
b.columns.name
b.columns.name = '属性'
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
      <th>属性</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
    <tr>
      <th>学号</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
b.index

```




    Int64Index([1, 2, 3, 4, 5], dtype='int64', name='学号')




```python
b.columns
```




    Index(['name', 'sex', 'age', 'heigh', 'weight', 'address', 'grade'], dtype='object', name='属性')



-----------------------

Pandas 对象的遍历
---

---

Pandas的对象一般不需要遍历,偶尔有需求


```python
a
```




    aaa
    0     3
    1     5
    2     8
    3    12
    4    14
    Name: 张三, dtype: int64



### Series遍历



```python
for i in a:
    print(i)
```

    3
    5
    8
    12
    14
    


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
      <th>属性</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
    <tr>
      <th>学号</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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



### DataFrame遍历


```python
for i in b:
    print(i)  #列索引
    
```

    name
    sex
    age
    heigh
    weight
    address
    grade
    


```python
for i in b:
    print(b[i])  #列值
```

    学号
    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object
    学号
    1      male
    2    female
    3    female
    4      male
    5    female
    Name: sex, dtype: object
    学号
    1    18
    2    28
    3    22
    4    31
    5    25
    Name: age, dtype: int64
    学号
    1    170
    2    160
    3    175
    4    182
    5    165
    Name: heigh, dtype: int64
    学号
    1    60
    2    50
    3    64
    4    80
    5    55
    Name: weight, dtype: int64
    学号
    1    北京海淀
    2    上海静安
    3    广州天河
    4    深圳南山
    5    杭州西湖
    Name: address, dtype: object
    学号
    1    61
    2    74
    3    59
    4    82
    5    98
    Name: grade, dtype: int64
    


```python
for i in b:
    print(type(b[i]))  #列值为Series类型
```

    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.series.Series'>
    


```python
for i in b:
    for j in b[i]:
        print(j)  #单元格值
        print(type(j))  #单值
```

    小明
    <class 'str'>
    小华
    <class 'str'>
    小红
    <class 'str'>
    小靑
    <class 'str'>
    小兰
    <class 'str'>
    male
    <class 'str'>
    female
    <class 'str'>
    female
    <class 'str'>
    male
    <class 'str'>
    female
    <class 'str'>
    18
    <class 'int'>
    28
    <class 'int'>
    22
    <class 'int'>
    31
    <class 'int'>
    25
    <class 'int'>
    170
    <class 'int'>
    160
    <class 'int'>
    175
    <class 'int'>
    182
    <class 'int'>
    165
    <class 'int'>
    60
    <class 'int'>
    50
    <class 'int'>
    64
    <class 'int'>
    80
    <class 'int'>
    55
    <class 'int'>
    北京海淀
    <class 'str'>
    上海静安
    <class 'str'>
    广州天河
    <class 'str'>
    深圳南山
    <class 'str'>
    杭州西湖
    <class 'str'>
    61
    <class 'int'>
    74
    <class 'int'>
    59
    <class 'int'>
    82
    <class 'int'>
    98
    <class 'int'>
    

### 用Pandas专有函数遍历


```python
for index,rows in b.iterrows():
    #print(index)   #行索引
    #print(rows)  #列
   #print(type(rows))
   # print(rows['name'])  #查询指定列的单元格值
    for i in rows:
        print(i)  #遍历所有单元格值
        #print(type(i))
```

    小明
    male
    18
    170
    60
    北京海淀
    61
    小华
    female
    28
    160
    50
    上海静安
    74
    小红
    female
    22
    175
    64
    广州天河
    59
    小靑
    male
    31
    182
    80
    深圳南山
    82
    小兰
    female
    25
    165
    55
    杭州西湖
    98
    
