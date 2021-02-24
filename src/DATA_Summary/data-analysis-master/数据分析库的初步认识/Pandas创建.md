
Pandas 体验
===

---

Pandas(panel data & Data Analysis)：最流行的Python数据分析库。

基于Numpy，专用于**数据预处理**和**数据分析**的Python第三方库，最适合处理大型结构化**表格数据**

---

Pandas 的数据类型
---

* Series 一维，带标签数组
* DataFrame 二维，Series容器（最常用）
* Panel 三维，DataFrame容器



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

###  载入pandas 库


```python
import pandas as pd
```

## Series


```python
pd.Series([3,5,8,111,222])
```




    0      3
    1      5
    2      8
    3    111
    4    222
    dtype: int64




```python
pd.Series([3,5,8,11,22],index = ['aa','bb','cc','dd','ee'])
```




    aa     3
    bb     5
    cc     8
    dd    11
    ee    22
    dtype: int64




```python
pd.Series([1,2,3,4,5,6],index = ['66','77','88','99','00','44'])
```




    66    1
    77    2
    88    3
    99    4
    00    5
    44    6
    dtype: int64



## DataFrame


```python
pd.DataFrame([[2,5,6,7],[3,8,4,2]])
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
      <td>2</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>8</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame([[2,5,6,7],[3,8,4,2]],
            index = [1,2],
            columns = ['aa','bb','cc','dd'])
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
      <th>aa</th>
      <th>bb</th>
      <th>cc</th>
      <th>dd</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>8</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame([[1,2,3,4],[5,6,7,8]],
            index = ['a','b'],
            columns = [1,2,3,4])
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>b</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



---

抽象和维度
---

===

12期同学数据


```python
'王灿，18,177.5,75，True'
'刘双丹，28,168.2,45，False'
'翟鹏飞，38,85,180.2，True'
```




    '翟鹏飞，38,85,180.2，True'



# 电子表格

~~~
姓名 | 年龄 | 身高 | 性别
---- | ---- | ---- | ----
王灿 | 18 | 177.5 | True
刘双丹 | 28 | 168.5 | False
翟鹏飞 | 38 | 180.5 | True
~~~

姓名 | 年龄 | 身高 | 性别
---- | ---- | ---- | ----
王灿 | 18 | 177.5 | True
刘双丹 | 28 | 168.5 | False
翟鹏飞 | 38 | 180.5 | True


抽象成python 能处理的数据

0维 ， 标量



```python
# 变量,112 个
name = '王灿'
age = 18
height = 177.6
gender = True

```

1 维，矢量 （向量）


```python
# 列表 ，4 个
name = ['王灿','刘双丹','翟鹏飞']
age = [18,28,38]
height = [177.5,168.6,180.2]
gender = [True,False,True]
```


```python
# 字典 ,3 个。
wangcan = {
    'name':'王灿',
    'age':18,
    'height':170.5,
    'gender':True,
}
```

2维， 矩阵 


```python
# 嵌套 1 个
py12 = {
    'name' : ['王灿','刘双丹','翟鹏飞'],
    'age' : [18,28,38],
    'height' : [177.5,168.6,180.2],
    'gender' : [True,False,True],
}
py12
```




    {'name': ['王灿', '刘双丹', '翟鹏飞'],
     'age': [18, 28, 38],
     'height': [177.5, 168.6, 180.2],
     'gender': [True, False, True]}



3 维， 张量，(tensor:3 维及以上) 


```python
py = {
    'py12':{
         'name' : ['王灿','刘双丹','翟鹏飞'],
        'age' : [18,28,38],
        'height' : [177.5,168.6,180.2],
        'gender' : [True,False,True],
    },
    'py13':{
         'name' : ['白雪原','李尧','，孟宪岳'],
        'age' : [18,28,38],
        'height' : [177.5,168.6,180.2],
        'gender' : [True,False,True],
    }
}
py
```




    {'py12': {'name': ['王灿', '刘双丹', '翟鹏飞'],
      'age': [18, 28, 38],
      'height': [177.5, 168.6, 180.2],
      'gender': [True, False, True]},
     'py13': {'name': ['白雪原', '李尧', '，孟宪岳'],
      'age': [18, 28, 38],
      'height': [177.5, 168.6, 180.2],
      'gender': [True, False, True]}}



例：将图片抽象为二维列表数据
---


```python
# 黑白图像,灰度，1 维
[
    1,2,3,
    4,5,6,
    7,8,9,
]

#彩色图像 ，RGB颜色，2 维

[
    [255,0,0],
    [0,255,0],
    [0,0,255],
    [255,0,0],
    [255,0,0],
    [0,255,0],
    [0,0,255],
    [255,0,0],
]

[[255,0,0],[0,255,0],[0,0,255],[255,0,0],[255,0,0],[0,255,0],[0,0,255],[255,0,0]]

```

# Pandas抽象表格数据


姓名 | 年龄 | 身高 | 性别
---- | ---- | ---- | ----
王灿 | 18 | 177.5 | True
刘双丹 | 28 | 168.5 | False
翟鹏飞 | 38 | 180.5 | True

# Series,1 维


```python

pd.Series(['王灿','刘双丹','翟鹏飞'])
pd.Series(['王灿',18,177,True])
```




    0      王灿
    1      18
    2     177
    3    True
    dtype: object



# 修改Series 索引


```python

pd.Series(['王灿',18,177,True],index=['name','age','height','gender'])
```




    name        王灿
    age         18
    height     177
    gender    True
    dtype: object



# DataFrame, 2 维


```python

pd.DataFrame([
    ['王灿',18,177,True],
    ['刘双丹',16,168,False],
    ['翟鹏飞',28,178,True],
])
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
      <td>王灿</td>
      <td>18</td>
      <td>177</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>刘双丹</td>
      <td>16</td>
      <td>168</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>翟鹏飞</td>
      <td>28</td>
      <td>178</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame, 2 维,修改行索引，列索引。


```python

pd.DataFrame([
    ['王灿',18,177,True],
    ['刘双丹',16,168,False],
    ['翟鹏飞',28,178,True],
],
    index = [1,2,3],
    columns = ['name','age','height','gender'],
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
      <th>name</th>
      <th>age</th>
      <th>height</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>王灿</td>
      <td>18</td>
      <td>177</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>刘双丹</td>
      <td>16</td>
      <td>168</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>翟鹏飞</td>
      <td>28</td>
      <td>178</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>


