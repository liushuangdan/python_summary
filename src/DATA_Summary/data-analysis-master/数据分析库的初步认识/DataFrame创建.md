
# DataFrame对象-创建


---

DataFrame对象是Pandas最常用的数据类型

 DataFrame 对象是由多个Sries增加一个索引后组成的一种表格类型数据结构

### DataFrame 对象既有行索引，又有列索引

* 行索引，表明不同行，横向索引，叫index，0轴，axis=0
* 列索引，表名不同列，纵向索引，叫columns，1轴，axis=1

---

%%HTML

<script>
code_show=true;
function code_toggle() {
 if (code_show){
 $('div.input').hide();
 } else {
 $('div.input').show();
 }
 code_show = !code_show
}
$( document ).ready(code_toggle);
</script>
<form action="javascript:code_toggle()"><input type="submit" value="点击按钮显示/隐藏文档代码！"></form>


```python
import numpy as np
import pandas as pd
```

# 创建

* 列表创建
    *ndarray 数组创建
    
* 字典创建
    * 字典内嵌套列表：要求列表等长
    * 字典内嵌套字典：内壁字典不需要等长
        * 字典内嵌套Series：等同嵌套字典


## 列表创建


```python
pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]])
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
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame(
    [[1,2,3],[4,5,6],[7,8,9]],
    index = [1,2,3],
    columns = ['a','b','c']
)
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
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
a = pd.DataFrame([
    ['刘双丹',18,177.6,66,True],
    ['丁洁',28,166.4,45,False],
],
    index = [0,1],
    columns = ['name','age','height','weight','gender'],
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
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>刘双丹</td>
      <td>18</td>
      <td>177.6</td>
      <td>66</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>丁洁</td>
      <td>28</td>
      <td>166.4</td>
      <td>45</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#ndarray 数组创建，类似列表
np.arange(10)
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
x = np.arange(10).reshape(2,5)
x
```




    array([[0, 1, 2, 3, 4],
           [5, 6, 7, 8, 9]])




```python
pd.DataFrame(x)
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
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame(x,index = [5,10],columns=['a','b','c','d','e'])
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
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



## 字典创建

####  字典内嵌套列表


```python
b = pd.DataFrame({
    'name': ['刘双丹','李尧','袁鹏飞'],
    'age': [18,26,28],
    'height': [177.4,165.4,180.1],
    'weight': [45,66,54],
    'gender': [True,False,True],
})
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
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>刘双丹</td>
      <td>18</td>
      <td>177.4</td>
      <td>45</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李尧</td>
      <td>26</td>
      <td>165.4</td>
      <td>66</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>袁鹏飞</td>
      <td>28</td>
      <td>180.1</td>
      <td>54</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



###  自定义行索引，和列索引


```python
b = pd.DataFrame({
    'name': ['刘双丹','李尧','袁鹏飞'],
    'age': [18,26,28],
    'height': [177.4,165.4,180.1],
    'weight': [45,66,54],
    'gender': [True,False,True],
},
    index = [1,2,3],
    columns = ['name','age','height','sex']
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
      <th>age</th>
      <th>height</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>刘双丹</td>
      <td>18</td>
      <td>177.4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李尧</td>
      <td>26</td>
      <td>165.4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>袁鹏飞</td>
      <td>28</td>
      <td>180.1</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 字典嵌套字典

字典不要求等长



```python
c = pd.DataFrame({
    'name': {2: '刘双丹',5: '李尧',8: '袁鹏飞'},
    'age': {2: 18,5: 26,8: 28},
    'height': {2: 177.4,5: 165.4,8: 180.1},
    'weight': {2: 45,5: 66}, # 少一个值
    'gender': {2: True,5: False,8: True},
})
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
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>刘双丹</td>
      <td>18</td>
      <td>177.4</td>
      <td>45.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>李尧</td>
      <td>26</td>
      <td>165.4</td>
      <td>66.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>袁鹏飞</td>
      <td>28</td>
      <td>180.1</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Series组成的字典 创建DataFrame，同嵌套字典

# 外层键是列索引，内层键是行索引
h_values = {
    'name':pd.Series(['小明', '小华', '小红', '小靑', '小兰'],index=[1, 2, 3, 4, 5]),
    'sex':pd.Series([1, 0, 0, 1, 0],index=[1, 2, 3, 4, 5]),
    'age':pd.Series([28, 38, 48, 8],index=[2, 3, 4, 5])  # 少一个值自动填充为NaN
}
h = pd.DataFrame(h_values)

h
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>0</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>0</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>1</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小兰</td>
      <td>0</td>
      <td>8.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 指定内层字典键（行索引），没有的值会填充NaN
i = pd.DataFrame(h_values, index=[3, 4, 2, 6])
i
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>小红</td>
      <td>0.0</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小靑</td>
      <td>1.0</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小华</td>
      <td>0.0</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


