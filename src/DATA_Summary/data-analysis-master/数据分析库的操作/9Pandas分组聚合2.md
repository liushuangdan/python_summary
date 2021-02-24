
### 根据层次化索引的级别分组¶
要根据层次化索引的级别分组，使用level关键字传递级别序号或名字


```python
import numpy as np
import pandas as pd
```


```python
columns = pd.MultiIndex.from_arrays([['US', 'US', 'US', 'JP', 'JP'], [1, 3, 5, 1, 3]],  names=['cty', 'tenor'])
hier_df = pd.DataFrame(np.random.randn(4, 5), columns=columns)
hier_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>cty</th>
      <th colspan="3" halign="left">US</th>
      <th colspan="2" halign="left">JP</th>
    </tr>
    <tr>
      <th>tenor</th>
      <th>1</th>
      <th>3</th>
      <th>5</th>
      <th>1</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.092580</td>
      <td>1.353454</td>
      <td>0.659464</td>
      <td>-0.146829</td>
      <td>-0.488205</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.361819</td>
      <td>-1.735350</td>
      <td>-0.027743</td>
      <td>1.138146</td>
      <td>-0.130812</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.270425</td>
      <td>0.524885</td>
      <td>-0.238268</td>
      <td>0.008854</td>
      <td>1.397235</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.238916</td>
      <td>-0.441246</td>
      <td>0.609524</td>
      <td>-0.644583</td>
      <td>1.427737</td>
    </tr>
  </tbody>
</table>
</div>




```python
hier_df.index
hier_df.columns
```




    MultiIndex(levels=[['JP', 'US'], [1, 3, 5]],
               labels=[[1, 1, 1, 0, 0], [0, 1, 2, 0, 1]],
               names=['cty', 'tenor'])




```python
hier_df.groupby(level='cty', axis=1).sum()
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
      <th>cty</th>
      <th>JP</th>
      <th>US</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.635034</td>
      <td>0.920338</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.007334</td>
      <td>-1.401274</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.406088</td>
      <td>0.557042</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.783153</td>
      <td>-0.070638</td>
    </tr>
  </tbody>
</table>
</div>




```python
-0.146829 + -0.488205
```




    -0.635034




```python
hier_df.groupby(level='tenor', axis=1).sum()
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
      <th>tenor</th>
      <th>1</th>
      <th>3</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.239409</td>
      <td>0.865249</td>
      <td>0.659464</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.499966</td>
      <td>-1.866162</td>
      <td>-0.027743</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.279278</td>
      <td>1.922120</td>
      <td>-0.238268</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.883499</td>
      <td>0.986491</td>
      <td>0.609524</td>
    </tr>
  </tbody>
</table>
</div>




```python
-1.092580 + -0.146829
```




    -1.2394090000000002



### 根据列表分组


```python
df = pd.DataFrame({
    'name': ['张三','李四','王五','李四','王五','王五','赵六'],
    'chinese':np.random.randint(35,100,7),
    'math':np.random.randint(35,100,7),
    'english':np.random.randint(35,100,7),
    'test': ['一','一','一','二','二','三','一']
})

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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['name']
```




    0    张三
    1    李四
    2    王五
    3    李四
    4    王五
    5    王五
    6    赵六
    Name: name, dtype: object




```python
df.groupby('name').sum()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>254</td>
      <td>182</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(df['name']).sum()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>254</td>
      <td>182</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
xxx = ['张三','李四','王五','李四','王五','王五','张三']  # 赵六变成张三
df.groupby(xxx).sum()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>129</td>
      <td>135</td>
      <td>167</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>254</td>
      <td>182</td>
    </tr>
  </tbody>
</table>
</div>




```python
47 + 82
```




    129



根据字典对象分组


```python
df2 = df.set_index('name')
df2
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 行索引，张三、赵六合并为“一个人”，李四改为‘李四new’,王五不在字典中，过滤掉
mapping2 = {'张三': '一个人', '赵六': '一个人', '李四': '李四new'}
df2.groupby(mapping2).sum()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>一个人</th>
      <td>129</td>
      <td>135</td>
      <td>167</td>
    </tr>
    <tr>
      <th>李四new</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.groupby(['name', mapping2]).sum()
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
      <th></th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <th>一个人</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <th>李四new</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>一个人</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



----

## 练习： 输出每个学生在每次考试次数中的数字平均分

从一个原始大表中抽取一个符合需求的小表



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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#每个学生，所有考试，所有成绩平均分。
df.groupby('name').mean()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80.666667</td>
      <td>84.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#每个学生，所有考试，数学成绩平均分
df.groupby('name')['math'].mean()
```




    name
    张三    89.000000
    李四    77.000000
    王五    84.666667
    赵六    46.000000
    Name: math, dtype: float64




```python
df.groupby('name').mean()['math']
```




    name
    张三    89.000000
    李四    77.000000
    王五    84.666667
    赵六    46.000000
    Name: math, dtype: float64




```python
df.groupby(['name','test']).mean()  # 每个学生，每次考试，所有科目平均分，2维
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
      <th></th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th>test</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <th>一</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>一</th>
      <td>99</td>
      <td>98</td>
      <td>84</td>
    </tr>
    <tr>
      <th>二</th>
      <td>46</td>
      <td>56</td>
      <td>95</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">王五</th>
      <th>一</th>
      <td>99</td>
      <td>96</td>
      <td>47</td>
    </tr>
    <tr>
      <th>三</th>
      <td>89</td>
      <td>82</td>
      <td>64</td>
    </tr>
    <tr>
      <th>二</th>
      <td>54</td>
      <td>76</td>
      <td>71</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>一</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['name','test'])['math'].mean()    # 每个学生，每次考试，数学科目平均分，2维
```




    name  test
    张三    一       89
    李四    一       98
          二       56
    王五    一       96
          三       82
          二       76
    赵六    一       46
    Name: math, dtype: int32



每个学生在每次考试次数中的数学平均分

最终版，二维表格形式


```python
# 转为3维
df.groupby(['name','test'])['math'].mean().unstack().fillna(0)  # 将内层索引旋转为列索引，缺失值填充为0
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
      <th>test</th>
      <th>一</th>
      <th>三</th>
      <th>二</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>89.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>98.0</td>
      <td>0.0</td>
      <td>56.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>96.0</td>
      <td>82.0</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>46.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



------

自定义聚合方式
===

自定义聚合方式：aggregate()，或agg()

之前的聚合方式，所有列只能应用一个相同的聚合函数

### agg()自定义聚合方式的优势：

* 聚合参数是列表
    * 对数据每列应用多个相同的聚合函数
* 聚合参数是字典
    * 对数据的每列应用一个或多个不同的聚合函数
* 聚合参数是自定义函数
    * 对数据进行一些复杂的操作
自定义聚合方式可以：

* 每个列应用不同的聚合方式
* 一个列应用多个聚合方式


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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#普通分组聚合
df.groupby('name').sum()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>254</td>
      <td>182</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
#上面代码使用自定义函数聚合的写法
df.groupby('name').agg('sum')
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>154</td>
      <td>179</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>254</td>
      <td>182</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



#### 聚合参数是列表
给每一列同时应用对个聚合函数


```python
df.groupby('name').agg([sum,'mean',np.min])  #列表参数函数可以有多种不同写法
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">chinese</th>
      <th colspan="3" halign="left">math</th>
      <th colspan="3" halign="left">english</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>amin</th>
      <th>sum</th>
      <th>mean</th>
      <th>amin</th>
      <th>sum</th>
      <th>mean</th>
      <th>amin</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
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
      <th>张三</th>
      <td>47</td>
      <td>47.000000</td>
      <td>47</td>
      <td>89</td>
      <td>89.000000</td>
      <td>89</td>
      <td>82</td>
      <td>82.000000</td>
      <td>82</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>72.500000</td>
      <td>46</td>
      <td>154</td>
      <td>77.000000</td>
      <td>56</td>
      <td>179</td>
      <td>89.500000</td>
      <td>84</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>80.666667</td>
      <td>54</td>
      <td>254</td>
      <td>84.666667</td>
      <td>76</td>
      <td>182</td>
      <td>60.666667</td>
      <td>47</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>82.000000</td>
      <td>82</td>
      <td>46</td>
      <td>46.000000</td>
      <td>46</td>
      <td>85</td>
      <td>85.000000</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
#将聚合列索引改为自定义方式，元组实现
df.groupby('name')['chinese','math'].agg([('求和',sum),('平均值','mean'),('最小值','min')])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">chinese</th>
      <th colspan="3" halign="left">math</th>
    </tr>
    <tr>
      <th></th>
      <th>求和</th>
      <th>平均值</th>
      <th>最小值</th>
      <th>求和</th>
      <th>平均值</th>
      <th>最小值</th>
    </tr>
    <tr>
      <th>name</th>
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
      <th>张三</th>
      <td>47</td>
      <td>47.000000</td>
      <td>47</td>
      <td>89</td>
      <td>89.000000</td>
      <td>89</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>72.500000</td>
      <td>46</td>
      <td>154</td>
      <td>77.000000</td>
      <td>56</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>80.666667</td>
      <td>54</td>
      <td>254</td>
      <td>84.666667</td>
      <td>76</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>82.000000</td>
      <td>82</td>
      <td>46</td>
      <td>46.000000</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
</div>



### 聚合参数是字典
每列应用一个不同聚合函数，或者每列应用多个不同的聚合函数


```python
# 语文列聚合函数，求和
df.groupby('name').agg({'chinese':sum})
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
      <th>chinese</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
#语文列聚合函数：求和，平均值
df.groupby('name').agg({'chinese':[sum,'mean']})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">chinese</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>47.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>72.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>80.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>82.000000</td>
    </tr>
  </tbody>
</table>
</div>



选中的多个列，每列都应用不同的多个聚合函数


```python
df.groupby('name').agg({'chinese':[sum,'mean'],'math': [sum,'mean', max]})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">chinese</th>
      <th colspan="3" halign="left">math</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>sum</th>
      <th>mean</th>
      <th>max</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47</td>
      <td>47.000000</td>
      <td>89</td>
      <td>89.000000</td>
      <td>89</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>145</td>
      <td>72.500000</td>
      <td>154</td>
      <td>77.000000</td>
      <td>98</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>242</td>
      <td>80.666667</td>
      <td>254</td>
      <td>84.666667</td>
      <td>96</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82</td>
      <td>82.000000</td>
      <td>46</td>
      <td>46.000000</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
</div>



### 聚合参数是自定义函数

用于一些较为复杂的聚合工作

* 自定义聚合函数要比系统自带的、经过优化的函数慢得多。
* 因为在构造中间分组数据块时存在非常大的开销（函数调用、数据重排等）


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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
def aaa(x):
    return x.max() - x.min()

df.groupby('name').agg(aaa)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>53</td>
      <td>42</td>
      <td>11</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>45</td>
      <td>20</td>
      <td>24</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



----

### 其他分组运算
运用groupby 函数进行分组后，我们能做的事情还有很多，并不局限于聚合汇总



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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>



过滤数据

栗子： 输出所有数学考试平均分及格的学生



```python
def bbb(x):
    return x['math'].mean() >= 60

df.groupby('name').agg(bbb)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
e = df.groupby('name').filter(bbb)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').filter(bbb).groupby('name').mean()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80.666667</td>
      <td>84.666667</td>
      <td>60.666667</td>
    </tr>
  </tbody>
</table>
</div>



使用transform 函数对所有的数据元素进行转换计算


```python
def fff(x):
    return x + 10

df.groupby('name').transform(fff)

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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>57</td>
      <td>99</td>
      <td>92</td>
    </tr>
    <tr>
      <th>1</th>
      <td>109</td>
      <td>108</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>109</td>
      <td>106</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>56</td>
      <td>66</td>
      <td>105</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>86</td>
      <td>81</td>
    </tr>
    <tr>
      <th>5</th>
      <td>99</td>
      <td>92</td>
      <td>74</td>
    </tr>
    <tr>
      <th>6</th>
      <td>92</td>
      <td>56</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>




```python
#使用向量化运算方式实现
df.loc[:,['chinese','math','english']] + 10
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>57</td>
      <td>99</td>
      <td>92</td>
    </tr>
    <tr>
      <th>1</th>
      <td>109</td>
      <td>108</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>109</td>
      <td>106</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>56</td>
      <td>66</td>
      <td>105</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>86</td>
      <td>81</td>
    </tr>
    <tr>
      <th>5</th>
      <td>99</td>
      <td>92</td>
      <td>74</td>
    </tr>
    <tr>
      <th>6</th>
      <td>92</td>
      <td>56</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>



apply是更底层的函数



```python
#使用自定义函数方式实现
def fff(x):
    return x + 10
df.loc[:,['chinese','math','english']].apply(fff)   #效果同上，底层写法，较为繁琐
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>57</td>
      <td>99</td>
      <td>92</td>
    </tr>
    <tr>
      <th>1</th>
      <td>109</td>
      <td>108</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>109</td>
      <td>106</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>56</td>
      <td>66</td>
      <td>105</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>86</td>
      <td>81</td>
    </tr>
    <tr>
      <th>5</th>
      <td>99</td>
      <td>92</td>
      <td>74</td>
    </tr>
    <tr>
      <th>6</th>
      <td>92</td>
      <td>56</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>



## 例子 ： 每个学生，每科成绩的平均值


```python
#正常分组聚合
df.groupby('name').mean()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80.666667</td>
      <td>84.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#apply 自定义函数，底层写法，聚合的原理
def ggg(x):
    return x.mean()
df.groupby('name').apply(ggg)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80.666667</td>
      <td>84.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>



### 练习：分组后进行复杂计算，使用apply自定义函数

* 语文成绩全部加10
* 数学成绩全部减10
* 求每位同学，每科成绩，平均分


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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#普通写法
df3 = df.copy()
df3
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#语文加10 分
df3['chinese'] = df3['chinese'] + 10
df3
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>57</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>109</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>109</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>56</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>64</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>99</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>92</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#数学减10 分
df3['math'] -= 10
df3
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>57</td>
      <td>79</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>109</td>
      <td>88</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>109</td>
      <td>86</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>56</td>
      <td>46</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>64</td>
      <td>66</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>99</td>
      <td>72</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>92</td>
      <td>36</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#分组聚合
df3.groupby('name').mean()
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>57.000000</td>
      <td>79.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>82.500000</td>
      <td>67.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90.666667</td>
      <td>74.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>92.000000</td>
      <td>36.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>




-----

------



```python

# apply 实现

def hh(x):
    x['chinese'] += 10
    x['math'] -= 10
    return x.mean()
df.groupby('name').apply(hh)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>67.000000</td>
      <td>69.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>82.500000</td>
      <td>67.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90.666667</td>
      <td>74.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>92.000000</td>
      <td>36.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>



------

### 例子：将学生某科成绩按由低到高排序，并返回需要的个数

* 返回语文成绩最低的前三条数据
* 返回所有同学语文成绩最低的1次考试成绩
* 返回所有同学数学成绩最低的2次考试成绩



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
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>



**排序知识**

a.sort_values()  **正序**

a.sort_values(ascending=False)   **倒序**


```python
#排序知识
a = pd.Series([3,5,1,9,2,4])
a
```




    0    3
    1    5
    2    1
    3    9
    4    2
    5    4
    dtype: int64




```python
a.sort_values()  #正序
```




    2    1
    4    2
    0    3
    5    4
    1    5
    3    9
    dtype: int64




```python
a.sort_values(ascending=False)   #倒序
```




    3    9
    1    5
    5    4
    0    3
    4    2
    2    1
    dtype: int64



DataFrame 按列排序


```python
df.sort_values(by='chinese')
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values(by='chinese',ascending = False)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 返回语文成绩最低的前三条数据
df.sort_values(by='chinese')[:3]
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 返回所有同学语文成绩最低的1次考试成绩
df.sort_values(by='chinese')[:1]
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 返回所有同学数学成绩最低的2次考试成绩
df.sort_values(by='math')[:2]
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 自定义函数实现上面功能
def top(x, p='chinese', n=3):
    """
    自定义函数实现DataFram对象排序输出功能.
    
    x：传入的DataFrame对象
    n：获取前几个值
    p：按df对象的哪一列排序
    """
    return x.sort_values(by=p)[:n]

```


```python
# 返回语文成绩最低的前三条数据
top(df)

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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 返回所有同学语文成绩最低的1次考试成绩
top(df, n=1)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 返回所有同学数学成绩最低的2次考试成绩
top(df, p='math', n=2)
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
  </tbody>
</table>
</div>



使用apply方式调用函数实现


```python
df.groupby('name').apply(top)
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
      <th></th>
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
    <tr>
      <th>name</th>
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
      <th>张三</th>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">王五</th>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').apply(top, p='math', n=2)  # apply通过这种方式传参数
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
      <th></th>
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
    <tr>
      <th>name</th>
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
      <th>张三</th>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">王五</th>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>



### 禁止分组键

分组键会跟原始对象的索引共同构成结果对象中的层次化索引

将group_keys=False传入groupby即可禁止该效果

group_key 删除最外层的行索引


```python
df.groupby(['name','test']).sum()
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
      <th></th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th>test</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <th>一</th>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>一</th>
      <td>99</td>
      <td>98</td>
      <td>84</td>
    </tr>
    <tr>
      <th>二</th>
      <td>46</td>
      <td>56</td>
      <td>95</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">王五</th>
      <th>一</th>
      <td>99</td>
      <td>96</td>
      <td>47</td>
    </tr>
    <tr>
      <th>三</th>
      <td>89</td>
      <td>82</td>
      <td>64</td>
    </tr>
    <tr>
      <th>二</th>
      <td>54</td>
      <td>76</td>
      <td>71</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>一</th>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['name','test'], as_index=False).sum()
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
      <th>test</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>一</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>一</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李四</td>
      <td>二</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>王五</td>
      <td>一</td>
      <td>99</td>
      <td>96</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>三</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>二</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>一</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
#删除，删除分组带来的外层索引
df.groupby('name').apply(top,n=2,p='math')
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
      <th></th>
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
    <tr>
      <th>name</th>
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
      <th>张三</th>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">王五</th>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name',group_keys = False).apply(top,n=2,p='math')
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
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name',as_index=False).apply(top,n=2,p='math')

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
      <th></th>
      <th>name</th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>0</th>
      <td>张三</td>
      <td>47</td>
      <td>89</td>
      <td>82</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1</th>
      <th>3</th>
      <td>李四</td>
      <td>46</td>
      <td>56</td>
      <td>95</td>
      <td>二</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>99</td>
      <td>98</td>
      <td>84</td>
      <td>一</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>4</th>
      <td>王五</td>
      <td>54</td>
      <td>76</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>89</td>
      <td>82</td>
      <td>64</td>
      <td>三</td>
    </tr>
    <tr>
      <th>3</th>
      <th>6</th>
      <td>赵六</td>
      <td>82</td>
      <td>46</td>
      <td>85</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>



### groupby调用describe()方法


```python
df.groupby('name')['chinese'].mean()
```




    name
    张三    47.000000
    李四    72.500000
    王五    80.666667
    赵六    82.000000
    Name: chinese, dtype: float64




```python
df.groupby('name')['chinese'].describe()
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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
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
      <th>张三</th>
      <td>1.0</td>
      <td>47.000000</td>
      <td>NaN</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2.0</td>
      <td>72.500000</td>
      <td>37.476659</td>
      <td>46.0</td>
      <td>59.25</td>
      <td>72.5</td>
      <td>85.75</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3.0</td>
      <td>80.666667</td>
      <td>23.629078</td>
      <td>54.0</td>
      <td>71.50</td>
      <td>89.0</td>
      <td>94.00</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1.0</td>
      <td>82.000000</td>
      <td>NaN</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name')['chinese'].describe().stack()  # 列索引转为行索引
```




    name       
    张三    count     1.000000
          mean     47.000000
          min      47.000000
          25%      47.000000
          50%      47.000000
          75%      47.000000
          max      47.000000
    李四    count     2.000000
          mean     72.500000
          std      37.476659
          min      46.000000
          25%      59.250000
          50%      72.500000
          75%      85.750000
          max      99.000000
    王五    count     3.000000
          mean     80.666667
          std      23.629078
          min      54.000000
          25%      71.500000
          50%      89.000000
          75%      94.000000
          max      99.000000
    赵六    count     1.000000
          mean     82.000000
          min      82.000000
          25%      82.000000
          50%      82.000000
          75%      82.000000
          max      82.000000
    dtype: float64




```python
df.groupby('name')['chinese'].describe().unstack()  # 行索引转为列索引
```




           name
    count  张三       1.000000
           李四       2.000000
           王五       3.000000
           赵六       1.000000
    mean   张三      47.000000
           李四      72.500000
           王五      80.666667
           赵六      82.000000
    std    张三            NaN
           李四      37.476659
           王五      23.629078
           赵六            NaN
    min    张三      47.000000
           李四      46.000000
           王五      54.000000
           赵六      82.000000
    25%    张三      47.000000
           李四      59.250000
           王五      71.500000
           赵六      82.000000
    50%    张三      47.000000
           李四      72.500000
           王五      89.000000
           赵六      82.000000
    75%    张三      47.000000
           李四      85.750000
           王五      94.000000
           赵六      82.000000
    max    张三      47.000000
           李四      99.000000
           王五      99.000000
           赵六      82.000000
    dtype: float64



DataFrame分组后能应用describe的原因:

转化后的表格式层次化索引，可以模拟三维数据


```python
df.groupby('name').describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">chinese</th>
      <th colspan="5" halign="left">english</th>
      <th colspan="8" halign="left">math</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>...</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>张三</th>
      <td>1.0</td>
      <td>47.000000</td>
      <td>NaN</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
      <td>1.0</td>
      <td>82.000000</td>
      <td>...</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>1.0</td>
      <td>89.000000</td>
      <td>NaN</td>
      <td>89.0</td>
      <td>89.0</td>
      <td>89.0</td>
      <td>89.0</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2.0</td>
      <td>72.500000</td>
      <td>37.476659</td>
      <td>46.0</td>
      <td>59.25</td>
      <td>72.5</td>
      <td>85.75</td>
      <td>99.0</td>
      <td>2.0</td>
      <td>89.500000</td>
      <td>...</td>
      <td>92.25</td>
      <td>95.0</td>
      <td>2.0</td>
      <td>77.000000</td>
      <td>29.698485</td>
      <td>56.0</td>
      <td>66.5</td>
      <td>77.0</td>
      <td>87.5</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3.0</td>
      <td>80.666667</td>
      <td>23.629078</td>
      <td>54.0</td>
      <td>71.50</td>
      <td>89.0</td>
      <td>94.00</td>
      <td>99.0</td>
      <td>3.0</td>
      <td>60.666667</td>
      <td>...</td>
      <td>67.50</td>
      <td>71.0</td>
      <td>3.0</td>
      <td>84.666667</td>
      <td>10.263203</td>
      <td>76.0</td>
      <td>79.0</td>
      <td>82.0</td>
      <td>89.0</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1.0</td>
      <td>82.000000</td>
      <td>NaN</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>1.0</td>
      <td>85.000000</td>
      <td>...</td>
      <td>85.00</td>
      <td>85.0</td>
      <td>1.0</td>
      <td>46.000000</td>
      <td>NaN</td>
      <td>46.0</td>
      <td>46.0</td>
      <td>46.0</td>
      <td>46.0</td>
      <td>46.0</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 24 columns</p>
</div>



apply是聚合操作的底层操作


```python
xxx = lambda x:x.describe()

df.groupby('name').apply(xxx)
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
      <th></th>
      <th>chinese</th>
      <th>math</th>
      <th>english</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">张三</th>
      <th>count</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>47.000000</td>
      <td>89.000000</td>
      <td>82.000000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">李四</th>
      <th>count</th>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>37.476659</td>
      <td>29.698485</td>
      <td>7.778175</td>
    </tr>
    <tr>
      <th>min</th>
      <td>46.000000</td>
      <td>56.000000</td>
      <td>84.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>59.250000</td>
      <td>66.500000</td>
      <td>86.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>72.500000</td>
      <td>77.000000</td>
      <td>89.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>85.750000</td>
      <td>87.500000</td>
      <td>92.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>99.000000</td>
      <td>98.000000</td>
      <td>95.000000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">王五</th>
      <th>count</th>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>80.666667</td>
      <td>84.666667</td>
      <td>60.666667</td>
    </tr>
    <tr>
      <th>std</th>
      <td>23.629078</td>
      <td>10.263203</td>
      <td>12.342339</td>
    </tr>
    <tr>
      <th>min</th>
      <td>54.000000</td>
      <td>76.000000</td>
      <td>47.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>71.500000</td>
      <td>79.000000</td>
      <td>55.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>89.000000</td>
      <td>82.000000</td>
      <td>64.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>94.000000</td>
      <td>89.000000</td>
      <td>67.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>99.000000</td>
      <td>96.000000</td>
      <td>71.000000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">赵六</th>
      <th>count</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>82.000000</td>
      <td>46.000000</td>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').apply(xxx).unstack()  # 将内层行索引旋转为内层列索引
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">chinese</th>
      <th colspan="5" halign="left">math</th>
      <th colspan="8" halign="left">english</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>...</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>张三</th>
      <td>1.0</td>
      <td>47.000000</td>
      <td>NaN</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
      <td>47.00</td>
      <td>47.0</td>
      <td>1.0</td>
      <td>89.000000</td>
      <td>...</td>
      <td>89.0</td>
      <td>89.0</td>
      <td>1.0</td>
      <td>82.000000</td>
      <td>NaN</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2.0</td>
      <td>72.500000</td>
      <td>37.476659</td>
      <td>46.0</td>
      <td>59.25</td>
      <td>72.5</td>
      <td>85.75</td>
      <td>99.0</td>
      <td>2.0</td>
      <td>77.000000</td>
      <td>...</td>
      <td>87.5</td>
      <td>98.0</td>
      <td>2.0</td>
      <td>89.500000</td>
      <td>7.778175</td>
      <td>84.0</td>
      <td>86.75</td>
      <td>89.5</td>
      <td>92.25</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3.0</td>
      <td>80.666667</td>
      <td>23.629078</td>
      <td>54.0</td>
      <td>71.50</td>
      <td>89.0</td>
      <td>94.00</td>
      <td>99.0</td>
      <td>3.0</td>
      <td>84.666667</td>
      <td>...</td>
      <td>89.0</td>
      <td>96.0</td>
      <td>3.0</td>
      <td>60.666667</td>
      <td>12.342339</td>
      <td>47.0</td>
      <td>55.50</td>
      <td>64.0</td>
      <td>67.50</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1.0</td>
      <td>82.000000</td>
      <td>NaN</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>82.00</td>
      <td>82.0</td>
      <td>1.0</td>
      <td>46.000000</td>
      <td>...</td>
      <td>46.0</td>
      <td>46.0</td>
      <td>1.0</td>
      <td>85.000000</td>
      <td>NaN</td>
      <td>85.0</td>
      <td>85.00</td>
      <td>85.0</td>
      <td>85.00</td>
      <td>85.0</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 24 columns</p>
</div>


