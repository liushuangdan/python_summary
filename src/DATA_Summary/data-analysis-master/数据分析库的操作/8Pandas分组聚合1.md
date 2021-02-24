
Pandas分组聚合
===
---

## 数据分析阶段：

### 数据规整（清洗）阶段后，下一阶段就是分组聚合

对数据集分组并对各组应用一个函数是数据分析中的重要环节

一般将数据准备好后，首先就是计算分组统计

sql能够方便的连接、过滤、转换和聚合数据，但sql能执行的分组运算种类有限，Pandas则强大灵活的多


```python
import numpy as np
import pandas as pd
```

某班若干位同学的三次语文，数学英语考试成绩


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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index   #行索引
```




    RangeIndex(start=0, stop=7, step=1)




```python
df.columns   #列索引
```




    Index(['name', 'chinese', 'math', 'english', 'test'], dtype='object')



---

数据聚合
===

一般指应用某些方法（自定义的聚合函数或系统自带Pandas的统计方法等）给数据降维

常见聚合方法：下面列举的都是非na值的计算结果


```python
df.sum()  #一维数据
```




    name       张三李四王五李四王五王五赵六
    chinese               417
    math                  484
    english               453
    test              一一一二二三一
    dtype: object




```python
df.sum(axis=1) #每一位的总分  每一行的所有列
```




    0    219
    1    196
    2    162
    3    185
    4    196
    5    227
    6    169
    dtype: int64




```python
df.count()  #按行计数
```




    name       7
    chinese    7
    math       7
    english    7
    test       7
    dtype: int64




```python
df.count(axis=1) #按列计数
```




    0    5
    1    5
    2    5
    3    5
    4    5
    5    5
    6    5
    dtype: int64




```python
df.describe()  #describe  也可以用在这里，但它并非聚合运算
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
      <th>count</th>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>59.571429</td>
      <td>69.142857</td>
      <td>64.714286</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14.105048</td>
      <td>19.351387</td>
      <td>18.838916</td>
    </tr>
    <tr>
      <th>min</th>
      <td>36.000000</td>
      <td>39.000000</td>
      <td>35.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>53.000000</td>
      <td>57.500000</td>
      <td>53.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>62.000000</td>
      <td>68.000000</td>
      <td>71.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>68.000000</td>
      <td>85.500000</td>
      <td>76.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>77.000000</td>
      <td>91.000000</td>
      <td>88.000000</td>
    </tr>
  </tbody>
</table>
</div>




--------


数据分组
===

分组：groupby()，一般指以下一个或多个操作步骤的集合

    Splitting 分组
    Applying 每个分组应用函数
    Combining 合并


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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 一般统计指标，聚合运算不能体现表格的进一步的信息
df.mean()
```




    chinese    59.571429
    math       69.142857
    english    64.714286
    dtype: float64




```python
#分组
df.groupby('name')
```




    <pandas.core.groupby.groupby.DataFrameGroupBy object at 0x0000000007DEDEF0>




--------------------------

 基础 ， 重要
=====

---


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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 先分组，后聚合
x = df.groupby('name').mean()
x
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
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
(44 + 68 + 36) / 3
```




    49.333333333333336




```python
x.loc['王五','chinese']
```




    57.666666666666664




```python
x.loc['张三','chinese']
```




    77.0



将分组传给变量


```python
classGroup = df.groupby('name')

classGroup
```




    <pandas.core.groupby.groupby.DataFrameGroupBy object at 0x0000000007E174A8>




```python
classGroup.min()

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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>36</td>
      <td>68</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>48</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
classGroup.sum()

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
      <td>77</td>
      <td>83</td>
      <td>59</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>109</td>
      <td>156</td>
      <td>116</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>173</td>
      <td>206</td>
      <td>206</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58</td>
      <td>39</td>
      <td>72</td>
    </tr>
  </tbody>
</table>
</div>




```python
classGroup.mean()
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
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>



如果不想使用分组作为索引，设置参数as_index = False


```python
df.groupby('name', as_index = False).mean()
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>



### 同时以多列作为基准分组


```python
x2 = df.groupby(['name','test']).mean()
x2
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
      <td>77</td>
      <td>83</td>
      <td>59</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">李四</th>
      <th>一</th>
      <td>73</td>
      <td>88</td>
      <td>35</td>
    </tr>
    <tr>
      <th>二</th>
      <td>36</td>
      <td>68</td>
      <td>81</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">王五</th>
      <th>一</th>
      <td>62</td>
      <td>53</td>
      <td>47</td>
    </tr>
    <tr>
      <th>三</th>
      <td>48</td>
      <td>91</td>
      <td>88</td>
    </tr>
    <tr>
      <th>二</th>
      <td>63</td>
      <td>62</td>
      <td>71</td>
    </tr>
    <tr>
      <th>赵六</th>
      <th>一</th>
      <td>58</td>
      <td>39</td>
      <td>72</td>
    </tr>
  </tbody>
</table>
</div>




```python
x2.columns
```




    Index(['chinese', 'math', 'english'], dtype='object')




```python
x2.index
# 注意levels和labels的对应关系，labels才是索引
```




    MultiIndex(levels=[['张三', '李四', '王五', '赵六'], ['一', '三', '二']],
               labels=[[0, 1, 1, 2, 2, 2, 3], [0, 0, 2, 0, 1, 2, 0]],
               names=['name', 'test'])




```python
# 给多列做分组,不将分组列作为索引
x2 = df.groupby(['name','test'],as_index = False).mean()

x2
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
      <td>77</td>
      <td>83</td>
      <td>59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>一</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李四</td>
      <td>二</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>王五</td>
      <td>一</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>三</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>二</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>一</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
    </tr>
  </tbody>
</table>
</div>



## 了解：分组的内部结构

分组不能直接输出，遍历查看分组内部的信息



```python
df.groupby('name')
```




    <pandas.core.groupby.groupby.DataFrameGroupBy object at 0x0000000007CD8198>




```python
for method, group in df.groupby('name'):
#     print(method)
    print(group)
#     print(type(group))
    x3 = group
    
x3
```

      name  chinese  math  english test
    0   张三       77    83       59    一
      name  chinese  math  english test
    1   李四       73    88       35    一
    3   李四       36    68       81    二
      name  chinese  math  english test
    2   王五       62    53       47    一
    4   王五       63    62       71    二
    5   王五       48    91       88    三
      name  chinese  math  english test
    6   赵六       58    39       72    一
    




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
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 多列分组遍历内部结构

for (k1,k2) ,group in df.groupby(['name','test']):
    print(k1)
#     print(k2)
#     print(group)
```

    张三
    李四
    李四
    王五
    王五
    王五
    赵六
    


```python
for (k1,k2) ,group in df.groupby(['name','test']):
#     print(k1)
    print(k2)
#     print(group)
```

    一
    一
    二
    一
    三
    二
    一
    


```python
for (k1,k2) ,group in df.groupby(['name','test']):
#     print(k1)
#     print(k2)
    print(group)
```

      name  chinese  math  english test
    0   张三       77    83       59    一
      name  chinese  math  english test
    1   李四       73    88       35    一
      name  chinese  math  english test
    3   李四       36    68       81    二
      name  chinese  math  english test
    2   王五       62    53       47    一
      name  chinese  math  english test
    5   王五       48    91       88    三
      name  chinese  math  english test
    4   王五       63    62       71    二
      name  chinese  math  english test
    6   赵六       58    39       72    一
    

## 分组转为列表或字典


```python
df.groupby('name')
```




    <pandas.core.groupby.groupby.DataFrameGroupBy object at 0x0000000007E2DD68>




```python
# 分组转为列表
x4 = list(df.groupby('name'))
x4
```




    [('张三',   name  chinese  math  english test
      0   张三       77    83       59    一),
     ('李四',   name  chinese  math  english test
      1   李四       73    88       35    一
      3   李四       36    68       81    二),
     ('王五',   name  chinese  math  english test
      2   王五       62    53       47    一
      4   王五       63    62       71    二
      5   王五       48    91       88    三),
     ('赵六',   name  chinese  math  english test
      6   赵六       58    39       72    一)]




```python
x4[2]

```




    ('王五',   name  chinese  math  english test
     2   王五       62    53       47    一
     4   王五       63    62       71    二
     5   王五       48    91       88    三)




```python
x4[2][0]

```




    '王五'




```python
x4[2][1]
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
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 分组转为字典
x5 = dict(list(df.groupby('name')))
x5
```




    {'张三':   name  chinese  math  english test
     0   张三       77    83       59    一, '李四':   name  chinese  math  english test
     1   李四       73    88       35    一
     3   李四       36    68       81    二, '王五':   name  chinese  math  english test
     2   王五       62    53       47    一
     4   王五       63    62       71    二
     5   王五       48    91       88    三, '赵六':   name  chinese  math  english test
     6   赵六       58    39       72    一}




```python
x5['王五']
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
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
  </tbody>
</table>
</div>



选取1列或列的子集
===

对于大数据集，很可能只需要对部分列进行聚合

下列三种写法结果一样

    传入标量形式的单个列名(单值列表)，返回Series
    
    分组聚合传入列表或数组(多个值的列表，或者二维列表)，返回DataFrame


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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 默认给所有列做分组聚合
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
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
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
# 只给chinese l lie 做分组聚合

#传入标量或列名，返回Series

df['chinese'].groupby(df['name']).mean()  #正常写法，下面写法的原理写法，写着复杂，效率高。

```




    name
    张三    77.000000
    李四    54.500000
    王五    57.666667
    赵六    58.000000
    Name: chinese, dtype: float64




```python
df.groupby('name')['chinese'].mean()  # 是上面协大的简写（语法糖），推荐********，写着简单，效率高
```




    name
    张三    77.000000
    李四    54.500000
    王五    57.666667
    赵六    58.000000
    Name: chinese, dtype: float64




```python
df.groupby('name').mean()['chinese']  #结果一致，但是计算原理不一致，写着最简单，效率低（会运算所有列）
```




    name
    张三    77.000000
    李四    54.500000
    王五    57.666667
    赵六    58.000000
    Name: chinese, dtype: float64




```python
# 多列聚合
df.groupby('name')['chinese','english'].mean()
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
      <th>english</th>
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
      <td>77.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#传入列表或数组，返回DataFrame
df[['chinese']].groupby(df['name']).mean()
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
      <td>77.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name')[['chinese']].mean()
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
      <td>77.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').mean()[['chinese']]
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
      <td>77.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
    </tr>
  </tbody>
</table>
</div>



## 更多操作


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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
#  分组以后计数
df.groupby('name').size()
```




    name
    张三    1
    李四    2
    王五    3
    赵六    1
    dtype: int64




```python
#分组数据在每一列的出现的行数
df.groupby('name').count()
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
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## 关于describe()快速综合统计


```python
df.describe()
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
      <th>count</th>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>59.571429</td>
      <td>69.142857</td>
      <td>64.714286</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14.105048</td>
      <td>19.351387</td>
      <td>18.838916</td>
    </tr>
    <tr>
      <th>min</th>
      <td>36.000000</td>
      <td>39.000000</td>
      <td>35.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>53.000000</td>
      <td>57.500000</td>
      <td>53.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>62.000000</td>
      <td>68.000000</td>
      <td>71.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>68.000000</td>
      <td>85.500000</td>
      <td>76.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>77.000000</td>
      <td>91.000000</td>
      <td>88.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['chinese']
```




    0    77
    1    73
    2    62
    3    36
    4    63
    5    48
    6    58
    Name: chinese, dtype: int32




```python
df['chinese'].describe()
```




    count     7.000000
    mean     59.571429
    std      14.105048
    min      36.000000
    25%      53.000000
    50%      62.000000
    75%      68.000000
    max      77.000000
    Name: chinese, dtype: float64



dataframe分组后之所以可以进行describe操作，原因是生成的结果是层次化索引（相当于3维数据）


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
      <td>77.000000</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>77.00</td>
      <td>77.0</td>
      <td>77.00</td>
      <td>77.0</td>
      <td>1.0</td>
      <td>59.000000</td>
      <td>...</td>
      <td>59.0</td>
      <td>59.0</td>
      <td>1.0</td>
      <td>83.000000</td>
      <td>NaN</td>
      <td>83.0</td>
      <td>83.0</td>
      <td>83.0</td>
      <td>83.0</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2.0</td>
      <td>54.500000</td>
      <td>26.162951</td>
      <td>36.0</td>
      <td>45.25</td>
      <td>54.5</td>
      <td>63.75</td>
      <td>73.0</td>
      <td>2.0</td>
      <td>58.000000</td>
      <td>...</td>
      <td>69.5</td>
      <td>81.0</td>
      <td>2.0</td>
      <td>78.000000</td>
      <td>14.142136</td>
      <td>68.0</td>
      <td>73.0</td>
      <td>78.0</td>
      <td>83.0</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3.0</td>
      <td>57.666667</td>
      <td>8.386497</td>
      <td>48.0</td>
      <td>55.00</td>
      <td>62.0</td>
      <td>62.50</td>
      <td>63.0</td>
      <td>3.0</td>
      <td>68.666667</td>
      <td>...</td>
      <td>79.5</td>
      <td>88.0</td>
      <td>3.0</td>
      <td>68.666667</td>
      <td>19.857828</td>
      <td>53.0</td>
      <td>57.5</td>
      <td>62.0</td>
      <td>76.5</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1.0</td>
      <td>58.000000</td>
      <td>NaN</td>
      <td>58.0</td>
      <td>58.00</td>
      <td>58.0</td>
      <td>58.00</td>
      <td>58.0</td>
      <td>1.0</td>
      <td>72.000000</td>
      <td>...</td>
      <td>72.0</td>
      <td>72.0</td>
      <td>1.0</td>
      <td>39.000000</td>
      <td>NaN</td>
      <td>39.0</td>
      <td>39.0</td>
      <td>39.0</td>
      <td>39.0</td>
      <td>39.0</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 24 columns</p>
</div>




```python
df.groupby('name').describe()['chinese']
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
      <td>77.000000</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>77.00</td>
      <td>77.0</td>
      <td>77.00</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>2.0</td>
      <td>54.500000</td>
      <td>26.162951</td>
      <td>36.0</td>
      <td>45.25</td>
      <td>54.5</td>
      <td>63.75</td>
      <td>73.0</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>3.0</td>
      <td>57.666667</td>
      <td>8.386497</td>
      <td>48.0</td>
      <td>55.00</td>
      <td>62.0</td>
      <td>62.50</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>1.0</td>
      <td>58.000000</td>
      <td>NaN</td>
      <td>58.0</td>
      <td>58.00</td>
      <td>58.0</td>
      <td>58.00</td>
      <td>58.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').describe().stack()   #堆叠旋转，将内层的列索引转为内层的行索引

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
      <th>english</th>
      <th>math</th>
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
      <th rowspan="7" valign="top">张三</th>
      <th>count</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>min</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>77.000000</td>
      <td>59.000000</td>
      <td>83.000000</td>
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
      <td>54.500000</td>
      <td>58.000000</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>26.162951</td>
      <td>32.526912</td>
      <td>14.142136</td>
    </tr>
    <tr>
      <th>min</th>
      <td>36.000000</td>
      <td>35.000000</td>
      <td>68.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>45.250000</td>
      <td>46.500000</td>
      <td>73.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>54.500000</td>
      <td>58.000000</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>63.750000</td>
      <td>69.500000</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>73.000000</td>
      <td>81.000000</td>
      <td>88.000000</td>
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
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.386497</td>
      <td>20.599353</td>
      <td>19.857828</td>
    </tr>
    <tr>
      <th>min</th>
      <td>48.000000</td>
      <td>47.000000</td>
      <td>53.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>55.000000</td>
      <td>59.000000</td>
      <td>57.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>62.000000</td>
      <td>71.000000</td>
      <td>62.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>62.500000</td>
      <td>79.500000</td>
      <td>76.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>63.000000</td>
      <td>88.000000</td>
      <td>91.000000</td>
    </tr>
    <tr>
      <th rowspan="7" valign="top">赵六</th>
      <th>count</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
    <tr>
      <th>min</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>58.000000</td>
      <td>72.000000</td>
      <td>39.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name').describe().unstack()   #Series,
```




                    name
    chinese  count  张三       1.000000
                    李四       2.000000
                    王五       3.000000
                    赵六       1.000000
             mean   张三      77.000000
                    李四      54.500000
                    王五      57.666667
                    赵六      58.000000
             std    张三            NaN
                    李四      26.162951
                    王五       8.386497
                    赵六            NaN
             min    张三      77.000000
                    李四      36.000000
                    王五      48.000000
                    赵六      58.000000
             25%    张三      77.000000
                    李四      45.250000
                    王五      55.000000
                    赵六      58.000000
             50%    张三      77.000000
                    李四      54.500000
                    王五      62.000000
                    赵六      58.000000
             75%    张三      77.000000
                    李四      63.750000
                    王五      62.500000
                    赵六      58.000000
             max    张三      77.000000
                    李四      73.000000
                              ...    
    math     count  王五       3.000000
                    赵六       1.000000
             mean   张三      83.000000
                    李四      78.000000
                    王五      68.666667
                    赵六      39.000000
             std    张三            NaN
                    李四      14.142136
                    王五      19.857828
                    赵六            NaN
             min    张三      83.000000
                    李四      68.000000
                    王五      53.000000
                    赵六      39.000000
             25%    张三      83.000000
                    李四      73.000000
                    王五      57.500000
                    赵六      39.000000
             50%    张三      83.000000
                    李四      78.000000
                    王五      62.000000
                    赵六      39.000000
             75%    张三      83.000000
                    李四      83.000000
                    王五      76.500000
                    赵六      39.000000
             max    张三      83.000000
                    李四      88.000000
                    王五      91.000000
                    赵六      39.000000
    Length: 96, dtype: float64




----


按列分组
===

本质上，groupby传入的数据并不是行索引或列索引，而是任意一个和数据结构对应的序列（列表、数组、字典）



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
      <td>77</td>
      <td>83</td>
      <td>59</td>
      <td>一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>73</td>
      <td>88</td>
      <td>35</td>
      <td>一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>62</td>
      <td>53</td>
      <td>47</td>
      <td>一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>36</td>
      <td>68</td>
      <td>81</td>
      <td>二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>63</td>
      <td>62</td>
      <td>71</td>
      <td>二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>48</td>
      <td>91</td>
      <td>88</td>
      <td>三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>58</td>
      <td>39</td>
      <td>72</td>
      <td>一</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('name',axis = 0).mean()
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
      <td>77.000000</td>
      <td>83.000000</td>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>54.500000</td>
      <td>78.000000</td>
      <td>58.000000</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>57.666667</td>
      <td>68.666667</td>
      <td>68.666667</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>58.000000</td>
      <td>39.000000</td>
      <td>72.000000</td>
    </tr>
  </tbody>
</table>
</div>



原理：使用 True,False做按列分组


```python
aaa = [True, True, True, False, False]
df.groupby(aaa, axis=1).sum()
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
      <th>False</th>
      <th>True</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>59</td>
      <td>160</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>161</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47</td>
      <td>115</td>
    </tr>
    <tr>
      <th>3</th>
      <td>81</td>
      <td>104</td>
    </tr>
    <tr>
      <th>4</th>
      <td>71</td>
      <td>125</td>
    </tr>
    <tr>
      <th>5</th>
      <td>88</td>
      <td>139</td>
    </tr>
    <tr>
      <th>6</th>
      <td>72</td>
      <td>97</td>
    </tr>
  </tbody>
</table>
</div>




```python
77+83
```




    160




```python
# 按列分组，改进
df.dtypes
```




    name       object
    chinese     int32
    math        int32
    english     int32
    test       object
    dtype: object




```python
df.groupby(df.dtypes,axis = 1).sum()
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
      <th>int32</th>
      <th>object</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>219</td>
      <td>张三一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>196</td>
      <td>李四一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>162</td>
      <td>王五一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>185</td>
      <td>李四二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>196</td>
      <td>王五二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>227</td>
      <td>王五三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>169</td>
      <td>赵六一</td>
    </tr>
  </tbody>
</table>
</div>




```python
bbb = ['object','int32','int32','int32','object'] # 等同于上面
df.groupby(bbb, axis=1).sum()
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
      <th>int32</th>
      <th>object</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>219</td>
      <td>张三一</td>
    </tr>
    <tr>
      <th>1</th>
      <td>196</td>
      <td>李四一</td>
    </tr>
    <tr>
      <th>2</th>
      <td>162</td>
      <td>王五一</td>
    </tr>
    <tr>
      <th>3</th>
      <td>185</td>
      <td>李四二</td>
    </tr>
    <tr>
      <th>4</th>
      <td>196</td>
      <td>王五二</td>
    </tr>
    <tr>
      <th>5</th>
      <td>227</td>
      <td>王五三</td>
    </tr>
    <tr>
      <th>6</th>
      <td>169</td>
      <td>赵六一</td>
    </tr>
  </tbody>
</table>
</div>



通过字典或Series进行分组
===

分组信息除了数组，还可以有其他形式，例如字典


```python
people = pd.DataFrame(np.random.randn(5, 5),
                      columns=['a', 'bc', 'c', 'd', 'e'],
                      index=['Joe', 'Steve', 'Wes', 'Jim', 'Travis']
                     )
people.iloc[2:3, [1, 2]] = np.nan
people
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
      <th>bc</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Joe</th>
      <td>0.677573</td>
      <td>1.433495</td>
      <td>-1.199981</td>
      <td>-1.299846</td>
      <td>-0.357880</td>
    </tr>
    <tr>
      <th>Steve</th>
      <td>-0.630918</td>
      <td>0.773755</td>
      <td>-0.002952</td>
      <td>-1.977579</td>
      <td>-0.071699</td>
    </tr>
    <tr>
      <th>Wes</th>
      <td>0.821230</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.453509</td>
      <td>0.166227</td>
    </tr>
    <tr>
      <th>Jim</th>
      <td>-0.730808</td>
      <td>-0.734256</td>
      <td>1.181295</td>
      <td>0.025160</td>
      <td>-0.184937</td>
    </tr>
    <tr>
      <th>Travis</th>
      <td>0.353297</td>
      <td>-0.013643</td>
      <td>0.455428</td>
      <td>-1.284179</td>
      <td>1.032548</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 假设已知列的分组关系，并希望根据分组计算列的和

mapping = {'a': 'red', 'bc': 'red', 'c': 'blue','d': 'blue', 'e': 'red', 'f': 'orange'}  # 多了一个f，不会影响分组

people.groupby(mapping, axis = 1).sum()

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
      <th>blue</th>
      <th>red</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Joe</th>
      <td>-2.499827</td>
      <td>1.753188</td>
    </tr>
    <tr>
      <th>Steve</th>
      <td>-1.980531</td>
      <td>0.071138</td>
    </tr>
    <tr>
      <th>Wes</th>
      <td>-0.453509</td>
      <td>0.987457</td>
    </tr>
    <tr>
      <th>Jim</th>
      <td>1.206455</td>
      <td>-1.650001</td>
    </tr>
    <tr>
      <th>Travis</th>
      <td>-0.828751</td>
      <td>1.372203</td>
    </tr>
  </tbody>
</table>
</div>




```python
-1.148644 + -1.113152  # joe行 c/d列相加   蓝色第一行
```




    -2.261796




```python
0.677573 + 1.433495 - 0.357880
```




    1.753188




```python
# 如果传值为Series，效果和字典一样
ccc = pd.Series(mapping)
ccc


```




    a        red
    bc       red
    c       blue
    d       blue
    e        red
    f     orange
    dtype: object




```python
people.groupby(ccc, axis=1).sum()
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
      <th>blue</th>
      <th>red</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Joe</th>
      <td>-2.499827</td>
      <td>1.753188</td>
    </tr>
    <tr>
      <th>Steve</th>
      <td>-1.980531</td>
      <td>0.071138</td>
    </tr>
    <tr>
      <th>Wes</th>
      <td>-0.453509</td>
      <td>0.987457</td>
    </tr>
    <tr>
      <th>Jim</th>
      <td>1.206455</td>
      <td>-1.650001</td>
    </tr>
    <tr>
      <th>Travis</th>
      <td>-0.828751</td>
      <td>1.372203</td>
    </tr>
  </tbody>
</table>
</div>



通过函数进行分组
===

比起字典或Series，函数是一种更原生的方法定义分组映射

任何被当做分组键的函数都会在各个索引值上被调用一次，其返回值就会被用作分组名称


```python
people
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
      <th>bc</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Joe</th>
      <td>0.677573</td>
      <td>1.433495</td>
      <td>-1.199981</td>
      <td>-1.299846</td>
      <td>-0.357880</td>
    </tr>
    <tr>
      <th>Steve</th>
      <td>-0.630918</td>
      <td>0.773755</td>
      <td>-0.002952</td>
      <td>-1.977579</td>
      <td>-0.071699</td>
    </tr>
    <tr>
      <th>Wes</th>
      <td>0.821230</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.453509</td>
      <td>0.166227</td>
    </tr>
    <tr>
      <th>Jim</th>
      <td>-0.730808</td>
      <td>-0.734256</td>
      <td>1.181295</td>
      <td>0.025160</td>
      <td>-0.184937</td>
    </tr>
    <tr>
      <th>Travis</th>
      <td>0.353297</td>
      <td>-0.013643</td>
      <td>0.455428</td>
      <td>-1.284179</td>
      <td>1.032548</td>
    </tr>
  </tbody>
</table>
</div>




```python
len('Joe'), len('Steve')
```




    (3, 5)




```python
people.groupby(len).sum()
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
      <th>bc</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>0.767994</td>
      <td>0.699239</td>
      <td>-0.018686</td>
      <td>-1.728195</td>
      <td>-0.376590</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.630918</td>
      <td>0.773755</td>
      <td>-0.002952</td>
      <td>-1.977579</td>
      <td>-0.071699</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.353297</td>
      <td>-0.013643</td>
      <td>0.455428</td>
      <td>-1.284179</td>
      <td>1.032548</td>
    </tr>
  </tbody>
</table>
</div>




```python
0.677573 + 0.821230 - 0.730808  # 名字3个字符的 a列 相加
```




    0.7679950000000001



传入函数和传入其他类型结合


```python
people
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
      <th>bc</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Joe</th>
      <td>0.677573</td>
      <td>1.433495</td>
      <td>-1.199981</td>
      <td>-1.299846</td>
      <td>-0.357880</td>
    </tr>
    <tr>
      <th>Steve</th>
      <td>-0.630918</td>
      <td>0.773755</td>
      <td>-0.002952</td>
      <td>-1.977579</td>
      <td>-0.071699</td>
    </tr>
    <tr>
      <th>Wes</th>
      <td>0.821230</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.453509</td>
      <td>0.166227</td>
    </tr>
    <tr>
      <th>Jim</th>
      <td>-0.730808</td>
      <td>-0.734256</td>
      <td>1.181295</td>
      <td>0.025160</td>
      <td>-0.184937</td>
    </tr>
    <tr>
      <th>Travis</th>
      <td>0.353297</td>
      <td>-0.013643</td>
      <td>0.455428</td>
      <td>-1.284179</td>
      <td>1.032548</td>
    </tr>
  </tbody>
</table>
</div>




```python
xxx = ['one','one','one','two','two']

people.groupby([len, xxx]).sum()
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
      <th>a</th>
      <th>bc</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>one</th>
      <td>1.498802</td>
      <td>1.433495</td>
      <td>-1.199981</td>
      <td>-1.753355</td>
      <td>-0.191653</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.730808</td>
      <td>-0.734256</td>
      <td>1.181295</td>
      <td>0.025160</td>
      <td>-0.184937</td>
    </tr>
    <tr>
      <th>5</th>
      <th>one</th>
      <td>-0.630918</td>
      <td>0.773755</td>
      <td>-0.002952</td>
      <td>-1.977579</td>
      <td>-0.071699</td>
    </tr>
    <tr>
      <th>6</th>
      <th>two</th>
      <td>0.353297</td>
      <td>-0.013643</td>
      <td>0.455428</td>
      <td>-1.284179</td>
      <td>1.032548</td>
    </tr>
  </tbody>
</table>
</div>




```python
0.677573 + 0.821230  # joe was a列相加
```




    1.498803


