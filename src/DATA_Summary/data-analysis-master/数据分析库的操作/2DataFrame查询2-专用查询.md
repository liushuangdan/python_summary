
DataFrame查询2-专用查询
---

---


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



Pandas专用查询方式
---

经过优化，推荐

三种查询方式：

索引

切片

过滤

---


## 索引查询

    用于连续或不连续(行列有间隔)行列区块查询

    解决了DataFrame进行行标签查询的问题
    

#### 两种查询方式：

    a.loc[行,列]，标签索引，自定义索引

    a.iloc[行,列]，位置索引，默认索引
    

参数书写顺序都是都是先行后列


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



查询单行


```python
#自定义索引
a.loc[1,:]    #自定义索引查询单行
a.loc[1]   #省略列，简便写法

#默认索引
a.iloc[0]
```




    name         小明
    sex        male
    age          18
    heigh       170
    weight       60
    address    北京海淀
    grade        61
    Name: 1, dtype: object




```python
# Series 类型
type(a.loc[1])
```




    pandas.core.series.Series



查询多行



```python
a.loc[[1, 3],:]
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
a.iloc[[0,2]]
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




查询单列


```python
a.loc[:,'name']
```




    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object




```python
a.iloc[:,0]
```




    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object



查询多列


```python
a.loc[:,['name','address']]
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




```python
a.iloc[:, [0,5]]
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



查询单元格，某一个具体的值  单行单列交叉



```python
a.loc[3,'address']   #行列交叉处
```




    '广州天河'




```python
a.iloc[2,5]
```




    '广州天河'




```python
#针对单元格的特殊写法
a.at[3,'address']

```




    '广州天河'




```python
a.iat[2,5]
```




    '广州天河'



查询一行多列


```python
a.loc[3,['name','address']]
```




    name         小红
    address    广州天河
    Name: 3, dtype: object




```python
a.iloc[2,[0,5]]
```




    name         小红
    address    广州天河
    Name: 3, dtype: object



查询多行一列


```python
a.loc[[2,4],'name']
```




    2    小华
    4    小靑
    Name: name, dtype: object




```python
a.iloc[[1,3],0]
```




    2    小华
    4    小靑
    Name: name, dtype: object



查询多行多列


```python
a.loc[[2,4],['name','address']]
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
      <th>2</th>
      <td>小华</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>深圳南山</td>
    </tr>
  </tbody>
</table>
</div>




```python
a.iloc[[1,3],[0,5]]
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
      <th>2</th>
      <td>小华</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>深圳南山</td>
    </tr>
  </tbody>
</table>
</div>



---

### 切片查询


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



查询单行，单列


```python
a.loc[1,:]   # 单行 同 a.loc[1]
```




    name         小明
    sex        male
    age          18
    heigh       170
    weight       60
    address    北京海淀
    grade        61
    Name: 1, dtype: object




```python
a.iloc[0,:]
```




    name         小明
    sex        male
    age          18
    heigh       170
    weight       60
    address    北京海淀
    grade        61
    Name: 1, dtype: object




```python
a.loc[:,'name']  # 单列

```




    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object




```python
a.iloc[:,0]
```




    1    小明
    2    小华
    3    小红
    4    小靑
    5    小兰
    Name: name, dtype: object



查询多行多列


```python
a.loc[2:4,'heigh':'address']  #自定义索引切片，包含结束值
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
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>3</th>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>4</th>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
    </tr>
  </tbody>
</table>
</div>




```python
a.iloc[1:4,3:6] #默认索引切片，不包含结束值
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
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
    </tr>
    <tr>
      <th>3</th>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
    </tr>
    <tr>
      <th>4</th>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
    </tr>
  </tbody>
</table>
</div>



#### 索引查询和切片查询的区别


* 索引查询更适合查询不连续的数据
* 切片查询适合查询连续数据

索引查询可以实现切片查询的所有功能，只是有一个书写效率问题
* 用索引查询查连续数据，需要将每个索引都写上，效率低。
* 切片查询查连续数据，只要写上起始和结束索引即可。
    * 切片不能查询不连续数据

优先使用切片查询
