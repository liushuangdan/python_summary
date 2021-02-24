
Pandas数据规整-合并
===


数据合并

Pandas提供了大量方法，能轻松的对Series，DataFrame执行合并操作

* 追加 .append()

* 简单合并 .concat()  concat()合并的前提是索引一致

* 复杂合并 .merge()和.join()

    * merge()函数用于复杂综合数据合并,操作复杂，功能强大
    * 按行索引合并 join()函数用于按索引合并，操作简单，功能单一
* 合并重叠数据（一个表为主，先填充再合并）：combine_first


```python
import numpy as np
import pandas as pd
```

# 追加 append()


```python
df = pd.DataFrame(np.random.randn(8, 4), columns = ['A','B','C','D'])
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.608713</td>
      <td>1.133601</td>
      <td>-0.387001</td>
      <td>-0.833521</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.665263</td>
      <td>0.292946</td>
      <td>-1.419200</td>
      <td>-1.897477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.054422</td>
      <td>1.080865</td>
      <td>1.021990</td>
      <td>1.498744</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.485375</td>
      <td>0.407789</td>
      <td>0.503487</td>
      <td>0.382787</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2.199215</td>
      <td>-1.487788</td>
      <td>1.893095</td>
      <td>-0.214528</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.584068</td>
      <td>0.956783</td>
      <td>-0.566554</td>
      <td>-0.179507</td>
    </tr>
  </tbody>
</table>
</div>




```python
s = df.loc[[3, 5]]
s
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
  </tbody>
</table>
</div>




```python
#追加合并

df.append(s)
df.append(s, ignore_index = True)   #不使用追加表的索引
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.608713</td>
      <td>1.133601</td>
      <td>-0.387001</td>
      <td>-0.833521</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.665263</td>
      <td>0.292946</td>
      <td>-1.419200</td>
      <td>-1.897477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.054422</td>
      <td>1.080865</td>
      <td>1.021990</td>
      <td>1.498744</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.485375</td>
      <td>0.407789</td>
      <td>0.503487</td>
      <td>0.382787</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2.199215</td>
      <td>-1.487788</td>
      <td>1.893095</td>
      <td>-0.214528</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.584068</td>
      <td>0.956783</td>
      <td>-0.566554</td>
      <td>-0.179507</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.append(s, ignore_index = True)   #不使用追加表的索引
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.608713</td>
      <td>1.133601</td>
      <td>-0.387001</td>
      <td>-0.833521</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.665263</td>
      <td>0.292946</td>
      <td>-1.419200</td>
      <td>-1.897477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.054422</td>
      <td>1.080865</td>
      <td>1.021990</td>
      <td>1.498744</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.485375</td>
      <td>0.407789</td>
      <td>0.503487</td>
      <td>0.382787</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2.199215</td>
      <td>-1.487788</td>
      <td>1.893095</td>
      <td>-0.214528</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.584068</td>
      <td>0.956783</td>
      <td>-0.566554</td>
      <td>-0.179507</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
  </tbody>
</table>
</div>



### DataFrame和Series追加合并


```python
s2 = pd.Series([1,2,3,4], index = ['A','B','C','D'])
s2
```




    A    1
    B    2
    C    3
    D    4
    dtype: int64




```python
df.append(s2, ignore_index=True)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.608713</td>
      <td>1.133601</td>
      <td>-0.387001</td>
      <td>-0.833521</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.665263</td>
      <td>0.292946</td>
      <td>-1.419200</td>
      <td>-1.897477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.054422</td>
      <td>1.080865</td>
      <td>1.021990</td>
      <td>1.498744</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.998903</td>
      <td>0.066551</td>
      <td>0.137134</td>
      <td>0.760518</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.485375</td>
      <td>0.407789</td>
      <td>0.503487</td>
      <td>0.382787</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.386431</td>
      <td>-0.674478</td>
      <td>-2.071466</td>
      <td>-0.500711</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2.199215</td>
      <td>-1.487788</td>
      <td>1.893095</td>
      <td>-0.214528</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.584068</td>
      <td>0.956783</td>
      <td>-0.566554</td>
      <td>-0.179507</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>4.000000</td>
    </tr>
  </tbody>
</table>
</div>



# 连接 .concat()


```python
df = pd.DataFrame(np.random.randn(10, 4))
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.292558</td>
      <td>1.093953</td>
      <td>0.002249</td>
      <td>0.021471</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.469323</td>
      <td>1.457726</td>
      <td>1.608742</td>
      <td>0.106506</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.145514</td>
      <td>0.160136</td>
      <td>1.569160</td>
      <td>1.614615</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.790061</td>
      <td>-0.340697</td>
      <td>-0.366011</td>
      <td>-0.432241</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.018275</td>
      <td>1.590433</td>
      <td>2.062223</td>
      <td>2.190167</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.628959</td>
      <td>-0.875532</td>
      <td>0.326061</td>
      <td>-0.368389</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.692785</td>
      <td>0.044703</td>
      <td>0.027657</td>
      <td>-0.095128</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.019091</td>
      <td>-1.435424</td>
      <td>-1.283300</td>
      <td>0.541989</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.159100</td>
      <td>0.300605</td>
      <td>-0.332208</td>
      <td>-0.625929</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.805078</td>
      <td>-0.431684</td>
      <td>1.999406</td>
      <td>-0.264300</td>
    </tr>
  </tbody>
</table>
</div>




```python
x = df.loc[:2]
x

y = df.loc[4:6]
y

z = df[-2:]
z
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
      <th>8</th>
      <td>-0.159100</td>
      <td>0.300605</td>
      <td>-0.332208</td>
      <td>-0.625929</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.805078</td>
      <td>-0.431684</td>
      <td>1.999406</td>
      <td>-0.264300</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([x,y,z])   #将合并表格放入列表
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
      <td>0.292558</td>
      <td>1.093953</td>
      <td>0.002249</td>
      <td>0.021471</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.469323</td>
      <td>1.457726</td>
      <td>1.608742</td>
      <td>0.106506</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.145514</td>
      <td>0.160136</td>
      <td>1.569160</td>
      <td>1.614615</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.018275</td>
      <td>1.590433</td>
      <td>2.062223</td>
      <td>2.190167</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.628959</td>
      <td>-0.875532</td>
      <td>0.326061</td>
      <td>-0.368389</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.692785</td>
      <td>0.044703</td>
      <td>0.027657</td>
      <td>-0.095128</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.159100</td>
      <td>0.300605</td>
      <td>-0.332208</td>
      <td>-0.625929</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.805078</td>
      <td>-0.431684</td>
      <td>1.999406</td>
      <td>-0.264300</td>
    </tr>
  </tbody>
</table>
</div>



# 复杂合并 .merge()和.join()

merge()函数用于复杂综合数据合并,操作复杂，功能强大

join()是merge()的一个特殊用法，用于按索引合并，操作简单，功能单一


```python
# df1，姓名和分组
df1 = pd.DataFrame({
    'name': ['张三', '李四', '王五', '赵六'],
    'group': ['DBA', 'PM','PM', 'HR']
})
df1
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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df2，姓名和入职时间
df2 = pd.DataFrame({
    'name': ['李四', '赵六', '张三', '王五'],
    'date': [2004, 2008, 2012, 2014]
})
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
      <th>name</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>李四</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>1</th>
      <td>赵六</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>张三</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>3</th>
      <td>王五</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>



两个表必须有相关性，才有合并的需要

以相同的列索引为基准，合并

合并两个对象，默认匹配相同过的列名，自动对齐合并


```python
df3 = pd.merge(df1, df2)
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
      <th>group</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>
</div>



要合并的样本量（行数）不同时，合并后的数据会自动扩展，不损失信息


```python
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
      <th>group</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df4，每个分组的领导，行数少
df4 = pd.DataFrame({
    'group': ['DBA', 'PM', 'HR'],
    'leader': ['钱大', '孙二', '周三']
})
df4
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
      <th>group</th>
      <th>leader</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DBA</td>
      <td>钱大</td>
    </tr>
    <tr>
      <th>1</th>
      <td>PM</td>
      <td>孙二</td>
    </tr>
    <tr>
      <th>2</th>
      <td>HR</td>
      <td>周三</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 样本量（行数）不同时，合并后的数据会自动扩展，不损失信息
pd.merge(df3, df4)
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
      <th>group</th>
      <th>date</th>
      <th>leader</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>2012</td>
      <td>钱大</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>2004</td>
      <td>孙二</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>2014</td>
      <td>孙二</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2008</td>
      <td>周三</td>
    </tr>
  </tbody>
</table>
</div>



分组和技能，行数多


```python
df1
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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
df5 = pd.DataFrame({
    'group': ['DBA', 'DBA','PM', 'PM', 'HR', 'HR'],
    'skills': ['Linux', '数据库', 'Axuer RP', '社交','招聘', '组织']
})
df5
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
      <th>group</th>
      <th>skills</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DBA</td>
      <td>Linux</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DBA</td>
      <td>数据库</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PM</td>
      <td>Axuer RP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PM</td>
      <td>社交</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HR</td>
      <td>招聘</td>
    </tr>
    <tr>
      <th>5</th>
      <td>HR</td>
      <td>组织</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df5)
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
      <th>group</th>
      <th>skills</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>Linux</td>
    </tr>
    <tr>
      <th>1</th>
      <td>张三</td>
      <td>DBA</td>
      <td>数据库</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李四</td>
      <td>PM</td>
      <td>Axuer RP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>PM</td>
      <td>社交</td>
    </tr>
    <tr>
      <th>4</th>
      <td>王五</td>
      <td>PM</td>
      <td>Axuer RP</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王五</td>
      <td>PM</td>
      <td>社交</td>
    </tr>
    <tr>
      <th>6</th>
      <td>赵六</td>
      <td>HR</td>
      <td>招聘</td>
    </tr>
    <tr>
      <th>7</th>
      <td>赵六</td>
      <td>HR</td>
      <td>组织</td>
    </tr>
  </tbody>
</table>
</div>



两个表没有同名列时，如何合并
===

两个对象没有同名列时，用left_on和right_on强制指定列名对应合并


```python
# df1，姓名 name 和分组
df1
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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df6，姓名2 username 和薪资
df6 = pd.DataFrame({
    'username': ['王五', '张三', '赵六', '李四'],
    'salary': [10000, 160000, 7000, 120000]
})
df6
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
      <th>username</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>王五</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>张三</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>120000</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df6, left_on='name', right_on='username')
pd.merge(df1, df6, left_on='name', right_on='username').drop('username', axis=1)
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
      <th>group</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>120000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>7000</td>
    </tr>
  </tbody>
</table>
</div>



按照行索引合并
===
当要合并数据的行索引相关时，指定 merge() 函数的参数 left_index 与 right_index 的值为 True，就可以实现自动依照索引序号合并

join()函数也能实现，写法更简单

merge()的优势在于更灵活，尤其是当数据集索引值差别很大，数据合并又必须以其中一组数据的索引值为依据时


```python
# df1a，将df1的name列设为行索引
df1a = df1.set_index('name')
df1a
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
      <th>group</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>DBA</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>PM</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>PM</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df2a，将df2的name列设为行索引
df2a = df2.set_index('name')
df2a
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
      <th>date</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>李四</th>
      <td>2004</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>2008</td>
    </tr>
    <tr>
      <th>张三</th>
      <td>2012</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>



按索引合并，最简单的方式 ：join()


```python
# join只用于以行索引为基准合并
df1a.join(df2a)
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
      <th>group</th>
      <th>date</th>
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
      <td>DBA</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>PM</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>PM</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>HR</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge实现,同上
pd.merge(df1a, df2a, left_index=True, right_index=True)
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
      <th>group</th>
      <th>date</th>
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
      <td>DBA</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>PM</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>PM</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>HR</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>
</div>



两数据索引差异巨大，又必须以一个索引为主合并


```python
# df1a，姓名和分组，姓名为行索引
df1a
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
      <th>group</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>DBA</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>PM</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>PM</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df6，姓名2和薪资
df6
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
      <th>username</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>王五</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>张三</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>120000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 指定一个表的行索引和另一个表的列为基准合并
pd.merge(df1a, df6, left_index=True, right_on='username')
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
      <th>group</th>
      <th>username</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>DBA</td>
      <td>张三</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PM</td>
      <td>李四</td>
      <td>120000</td>
    </tr>
    <tr>
      <th>0</th>
      <td>PM</td>
      <td>王五</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>HR</td>
      <td>赵六</td>
      <td>7000</td>
    </tr>
  </tbody>
</table>
</div>



-----

两个对应列不完全重复的数据集的合并
===

参数 how

* how='inner'，交集，两个表共有的行
* how='outer'，并集，两个表所有的行
* how='left'，表1的行
* how='right'，表2的行


```python
# df1，姓名和分组
df1

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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df7，姓名和时间，姓名列不完全一致
df7 = pd.DataFrame({'name':['张一', '李二', '赵六'], 'data':[2000,2001,2002]})
df7
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
      <th>data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张一</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李二</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>2002</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df7)
pd.merge(df1, df7, how='inner')  # 交集
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
      <th>group</th>
      <th>data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2002</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df7, how='outer')  # 并集
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
      <th>group</th>
      <th>data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2002.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>张一</td>
      <td>NaN</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>李二</td>
      <td>NaN</td>
      <td>2001.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df7, how='left')  # 以左表为基准
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
      <th>group</th>
      <th>data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2002.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df7, how='right')  # 以右表为基准
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
      <th>group</th>
      <th>data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>赵六</td>
      <td>HR</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>1</th>
      <td>张一</td>
      <td>NaN</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李二</td>
      <td>NaN</td>
      <td>2001</td>
    </tr>
  </tbody>
</table>
</div>



合并数据集中包含两个或以上相同列名时
===

参数 on 指定用于合并的主键

合并后的数据集中，之前相同的列名会被默认加上 _x 等后缀用于区分

参数 suffixes 可以自定义后缀


```python
# df1，姓名和分组
df1
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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df8，相同的姓名和分组
df8 = pd.DataFrame({
    'name': ['张三', '王五', '赵六', '李四'],
    'group': ['code', 'VP','VP', 'code']
})
df8
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
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>code</td>
    </tr>
    <tr>
      <th>1</th>
      <td>王五</td>
      <td>VP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>VP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>李四</td>
      <td>code</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, df8, on='name')  # 两表超过1个列名相同，手动指定合并基准列
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
      <th>group_x</th>
      <th>group_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>code</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>code</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>VP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>VP</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过设置参数 suffixes 自定义后缀
pd.merge(df1, df8, on='name', suffixes=['_L', '_R'])
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
      <th>group_L</th>
      <th>group_R</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>DBA</td>
      <td>code</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>PM</td>
      <td>code</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五</td>
      <td>PM</td>
      <td>VP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>HR</td>
      <td>VP</td>
    </tr>
  </tbody>
</table>
</div>



合并重叠数据
===

有一类数据组合问题不能用简单的合并（merge）或连接（concatenation(concat)）运算来处理。 如合并全部或部分重叠的两个数据集

举例，我们使用NumPy的where函数，它表示一种等价于面向数组的if-else

以a为基准合并，a的缺失值使用b填充
===

先给a打补丁（用b填充a的缺失值，再合并）


```python
a = pd.Series([np.nan, 2.5, np.nan, 3.5, 4.5, np.nan], index=['f', 'e', 'd', 'c', 'b', 'a'])
b = pd.Series(np.arange(len(a), dtype=np.float64), index=['f', 'e', 'd', 'c', 'b', 'a'])
b[-1] = np.nan
```


```python
a

```




    f    NaN
    e    2.5
    d    NaN
    c    3.5
    b    4.5
    a    NaN
    dtype: float64




```python
b
```




    f    0.0
    e    1.0
    d    2.0
    c    3.0
    b    4.0
    a    NaN
    dtype: float64



将a的缺失值使用b填充


```python
a.isnull()
```




    f     True
    e    False
    d     True
    c    False
    b    False
    a     True
    dtype: bool




```python
# 方法1
np.where(a.isnull(), b, a)
```




    array([0. , 2.5, 2. , 3.5, 4.5, nan])




```python
# 方法2
ax = a.copy()
ax

ax[ax.isnull()] = b
ax
```




    f    0.0
    e    2.5
    d    2.0
    c    3.5
    b    4.5
    a    NaN
    dtype: float64



Series有一个combine_first方法，实现的也是类似功能，

除了用b填充a的缺失值，还带有pandas数据对齐的合并功能

## 例子：以a2为基准合并，a2缺失数据使用b2填充



```python
a2 = a[2:]
a2

```




    d    NaN
    c    3.5
    b    4.5
    a    NaN
    dtype: float64




```python
b2 = b[:-2]
b2
```




    f    0.0
    e    1.0
    d    2.0
    c    3.0
    dtype: float64



使用原生方式打补丁




```python

a22 = a2.copy()
a22[a22.isnull()] = b2
a22
```




    d    2.0
    c    3.5
    b    4.5
    a    NaN
    dtype: float64



使用combine_first方法，先打补丁，再合并


```python
a2.combine_first(b2)
```




    a    NaN
    b    4.5
    c    3.5
    d    2.0
    e    1.0
    f    0.0
    dtype: float64



### 对于DataFrame，combine_first会在列上应用同样操作，可以将其看做：


用传递对象中的数据为调用对象的缺失数据“打补丁”


```python
df11 = pd.DataFrame({'a': [1., np.nan, 5., np.nan], 'b': [np.nan, 2., np.nan, 6.], 'c': range(2, 18, 4)})
df21 = pd.DataFrame({'a': [5., 4., np.nan, 3., 7.], 'b': [np.nan, 3., 4., 6., 8.]})

```


```python
df11

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
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>6.0</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
df21

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.0</td>
      <td>8.0</td>
    </tr>
  </tbody>
</table>
</div>



### 以df11为基准，先填充缺失值（用df21的值填充df11），再合并(df21的多余行列合并到df11上)


```python
df11.combine_first(df21)   
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
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>4.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>6.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 以df21为基准，先填充（用df11的值填充df21），再合并


```python
df21.combine_first(df11)
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
      <th>0</th>
      <td>5.0</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>3.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>4.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>6.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


