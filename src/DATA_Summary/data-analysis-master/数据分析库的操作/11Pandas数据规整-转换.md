
---

Pandas数据规整 - 转换
===





```python
import numpy as np
import pandas as pd
```


Pandas数据排序
===

.sort_index() 在指定轴上根据索引进行排序，索引排序后内容会跟随排序


```python
b = pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



## sort_index() 按索引排序


```python
b.sort_index()  # 默认按行索引排序，默认升序
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
      <th>a</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>b</th>
      <td>15</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>c</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>d</th>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
b.sort_index(axis=1, ascending=False)  # 按列索引排序，降序
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
      <th>4</th>
      <th>3</th>
      <th>2</th>
      <th>1</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>c</th>
      <td>4</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>a</th>
      <td>9</td>
      <td>8</td>
      <td>7</td>
      <td>6</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>14</td>
      <td>13</td>
      <td>12</td>
      <td>11</td>
      <td>10</td>
    </tr>
    <tr>
      <th>b</th>
      <td>19</td>
      <td>18</td>
      <td>17</td>
      <td>16</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



## sort_values() 按值排序


```python
dates = pd.date_range('20130101', periods = 10)
dates
df = pd.DataFrame(np.random.randn(10,4), index = dates, columns = ['A','B','C','D'])
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
      <th>2013-01-01</th>
      <td>0.054111</td>
      <td>0.520730</td>
      <td>-0.078286</td>
      <td>-1.761937</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.214259</td>
      <td>-0.218209</td>
      <td>0.013929</td>
      <td>-0.015321</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.729056</td>
      <td>1.966048</td>
      <td>0.219564</td>
      <td>2.000185</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.604133</td>
      <td>1.488920</td>
      <td>-0.308874</td>
      <td>0.902186</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.282761</td>
      <td>-0.358652</td>
      <td>1.553194</td>
      <td>0.162584</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.958058</td>
      <td>-0.306626</td>
      <td>0.314786</td>
      <td>-0.425420</td>
    </tr>
    <tr>
      <th>2013-01-07</th>
      <td>0.319470</td>
      <td>2.273635</td>
      <td>-0.882977</td>
      <td>0.563816</td>
    </tr>
    <tr>
      <th>2013-01-08</th>
      <td>1.174884</td>
      <td>0.923861</td>
      <td>-0.344344</td>
      <td>-0.680491</td>
    </tr>
    <tr>
      <th>2013-01-09</th>
      <td>-1.154599</td>
      <td>0.684099</td>
      <td>0.413360</td>
      <td>-1.266799</td>
    </tr>
    <tr>
      <th>2013-01-10</th>
      <td>0.590378</td>
      <td>0.209942</td>
      <td>1.348995</td>
      <td>0.035341</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 默认按行排序（这一列的所有行）
df.sort_values(by='A')  # 指定排序基准列

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
      <th>2013-01-09</th>
      <td>-1.154599</td>
      <td>0.684099</td>
      <td>0.413360</td>
      <td>-1.266799</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.958058</td>
      <td>-0.306626</td>
      <td>0.314786</td>
      <td>-0.425420</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.729056</td>
      <td>1.966048</td>
      <td>0.219564</td>
      <td>2.000185</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>0.054111</td>
      <td>0.520730</td>
      <td>-0.078286</td>
      <td>-1.761937</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.214259</td>
      <td>-0.218209</td>
      <td>0.013929</td>
      <td>-0.015321</td>
    </tr>
    <tr>
      <th>2013-01-07</th>
      <td>0.319470</td>
      <td>2.273635</td>
      <td>-0.882977</td>
      <td>0.563816</td>
    </tr>
    <tr>
      <th>2013-01-10</th>
      <td>0.590378</td>
      <td>0.209942</td>
      <td>1.348995</td>
      <td>0.035341</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.604133</td>
      <td>1.488920</td>
      <td>-0.308874</td>
      <td>0.902186</td>
    </tr>
    <tr>
      <th>2013-01-08</th>
      <td>1.174884</td>
      <td>0.923861</td>
      <td>-0.344344</td>
      <td>-0.680491</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.282761</td>
      <td>-0.358652</td>
      <td>1.553194</td>
      <td>0.162584</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values(by='A', ascending=False)  # 倒序
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
      <th>2013-01-05</th>
      <td>1.282761</td>
      <td>-0.358652</td>
      <td>1.553194</td>
      <td>0.162584</td>
    </tr>
    <tr>
      <th>2013-01-08</th>
      <td>1.174884</td>
      <td>0.923861</td>
      <td>-0.344344</td>
      <td>-0.680491</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.604133</td>
      <td>1.488920</td>
      <td>-0.308874</td>
      <td>0.902186</td>
    </tr>
    <tr>
      <th>2013-01-10</th>
      <td>0.590378</td>
      <td>0.209942</td>
      <td>1.348995</td>
      <td>0.035341</td>
    </tr>
    <tr>
      <th>2013-01-07</th>
      <td>0.319470</td>
      <td>2.273635</td>
      <td>-0.882977</td>
      <td>0.563816</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.214259</td>
      <td>-0.218209</td>
      <td>0.013929</td>
      <td>-0.015321</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>0.054111</td>
      <td>0.520730</td>
      <td>-0.078286</td>
      <td>-1.761937</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.729056</td>
      <td>1.966048</td>
      <td>0.219564</td>
      <td>2.000185</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.958058</td>
      <td>-0.306626</td>
      <td>0.314786</td>
      <td>-0.425420</td>
    </tr>
    <tr>
      <th>2013-01-09</th>
      <td>-1.154599</td>
      <td>0.684099</td>
      <td>0.413360</td>
      <td>-1.266799</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 按列排序（一行的所有列）
df.sort_values(axis=1, by='2013-01-03', ascending=False)  # 按列排序，指定行基准为...，降序
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
      <th>D</th>
      <th>B</th>
      <th>C</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.761937</td>
      <td>0.520730</td>
      <td>-0.078286</td>
      <td>0.054111</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.015321</td>
      <td>-0.218209</td>
      <td>0.013929</td>
      <td>0.214259</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>2.000185</td>
      <td>1.966048</td>
      <td>0.219564</td>
      <td>-0.729056</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.902186</td>
      <td>1.488920</td>
      <td>-0.308874</td>
      <td>0.604133</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.162584</td>
      <td>-0.358652</td>
      <td>1.553194</td>
      <td>1.282761</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.425420</td>
      <td>-0.306626</td>
      <td>0.314786</td>
      <td>-0.958058</td>
    </tr>
    <tr>
      <th>2013-01-07</th>
      <td>0.563816</td>
      <td>2.273635</td>
      <td>-0.882977</td>
      <td>0.319470</td>
    </tr>
    <tr>
      <th>2013-01-08</th>
      <td>-0.680491</td>
      <td>0.923861</td>
      <td>-0.344344</td>
      <td>1.174884</td>
    </tr>
    <tr>
      <th>2013-01-09</th>
      <td>-1.266799</td>
      <td>0.684099</td>
      <td>0.413360</td>
      <td>-1.154599</td>
    </tr>
    <tr>
      <th>2013-01-10</th>
      <td>0.035341</td>
      <td>0.209942</td>
      <td>1.348995</td>
      <td>0.590378</td>
    </tr>
  </tbody>
</table>
</div>



关于排序中的缺失值问题

排序不论升序降序，缺失值永远排在最后


```python
a = pd.DataFrame(np.arange(12).reshape(3,4), index=['a','b','c'])
a
b = pd.DataFrame(np.arange(20).reshape(4,5), index=['c','a','d','b'])
b

c = a + b
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>5.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>b</th>
      <td>19.0</td>
      <td>21.0</td>
      <td>23.0</td>
      <td>25.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>c</th>
      <td>8.0</td>
      <td>10.0</td>
      <td>12.0</td>
      <td>14.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.sort_values(by=0)  # 升序，缺失值在最后

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
      <th>a</th>
      <td>5.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>c</th>
      <td>8.0</td>
      <td>10.0</td>
      <td>12.0</td>
      <td>14.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>b</th>
      <td>19.0</td>
      <td>21.0</td>
      <td>23.0</td>
      <td>25.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
c.sort_values(by=0, ascending=False)  # 降序，缺失值还在最后
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
      <th>b</th>
      <td>19.0</td>
      <td>21.0</td>
      <td>23.0</td>
      <td>25.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>c</th>
      <td>8.0</td>
      <td>10.0</td>
      <td>12.0</td>
      <td>14.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>a</th>
      <td>5.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



随机排列和随机采样
===

## 随机排列
利用numpy.random.permutation函数可以实现对Series或DataFrame的列的随机排序工作（permuting，随机重排序）

通过需要排列的轴的长度调用permutation，可产生一个表示新顺序的整数数组：


```python
# 随机排列序列
a = [1,2,3,4,5,6,7]
np.random.permutation(a)
```




    array([2, 4, 3, 7, 5, 1, 6])




```python
df = pd.DataFrame(np.arange(5 * 4).reshape((5, 4)))
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
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
```




    RangeIndex(start=0, stop=5, step=1)




```python
df.columns
```




    RangeIndex(start=0, stop=4, step=1)




```python
# 打乱行索引
np.random.permutation(df.index)
```




    array([2, 0, 4, 1, 3], dtype=int64)



随机排序，按行索引


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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[[2,1,3,0,4]]
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
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[np.random.permutation(df.index)]
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
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



随机重排行索引和列索引


```python
index2 = np.random.permutation(df.index)
index2

columns2 = np.random.permutation(df.columns)
columns2

df.loc[index2, columns2]
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
      <th>3</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>19</td>
      <td>16</td>
      <td>17</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11</td>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



随机采样
===

choice(),从一个序列中随机抽取某些值


```python
a = [1,2,3,4,5,6,7]

np.random.choice(a)  # 从序列中随机抽取1个值
np.random.choice(a, size=3)  # 抽3个
np.random.choice(a, size=3, replace=False)  # 不重复抽取
```




    array([2, 3, 6])



### 随机采样


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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



## 按行随机抽取


```python
df.index
index2 = np.random.choice(df.index, size=3, replace=False)
index2

df.loc[index2]
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
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



## 按行，按列随机抽取


```python
index2 = np.random.choice(df.index, size=3, replace=False)
index2

columns2 = np.random.choice(df.columns, size=2, replace=False)
columns2

df.loc[index2, columns2]
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
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>15</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



重新索引(修改索引)
===

reindex(), 重新索引，创建一个适应新索引的新对象

一种变相的查询方式，类似在查询中加入新行新列


```python
obj = pd.Series([4.5,7,2,-5.3], index = ['d','b','a','c'])
obj
```




    d    4.5
    b    7.0
    a    2.0
    c   -5.3
    dtype: float64




```python
obj.index

```




    Index(['d', 'b', 'a', 'c'], dtype='object')




```python
obj.index.values
```




    array(['d', 'b', 'a', 'c'], dtype=object)



直接修改索引

有问题  不合适

* 索引修改后，值没有跟着改变
* 修改值必须和原索引长度保持一致，不能增加或删除索引


```python
obj.index = ['a','b','c','d']
obj
```




    a    4.5
    b    7.0
    c    2.0
    d   -5.3
    dtype: float64




```python
# obj.index = ['a','b','c']  # 长度不一致，报错
```

使用rename 修改索引


```python
obj
```




    a    4.5
    b    7.0
    c    2.0
    d   -5.3
    dtype: float64




```python
obj.rename({'a': 'aa', 'b': 'ccc', 'x': 'xx'})
```




    aa     4.5
    ccc    7.0
    c      2.0
    d     -5.3
    dtype: float64



正规做法：使用reindex（）修改索引


```python
obj
```




    a    4.5
    b    7.0
    c    2.0
    d   -5.3
    dtype: float64




```python
obj.reindex(['b','d','a','c','e'])
```




    b    7.0
    d   -5.3
    a    4.5
    c    2.0
    e    NaN
    dtype: float64




```python
#新增的缺失值，填充默认值
obj.reindex(['b','d','a','c','e'], fill_value=0)
```




    b    7.0
    d   -5.3
    a    4.5
    c    2.0
    e    0.0
    dtype: float64




```python
obj2 = pd.Series(['blue','purple','yellow'], index = [0,2,4])
obj2
```




    0      blue
    2    purple
    4    yellow
    dtype: object




```python
range(6)
```




    range(0, 6)




```python
obj2.reindex(range(6))
```




    0      blue
    1       NaN
    2    purple
    3       NaN
    4    yellow
    5       NaN
    dtype: object




```python
# 填充缺失值，指定填充值
obj2.reindex(range(6), fill_value=0)
```




    0      blue
    1         0
    2    purple
    3         0
    4    yellow
    5         0
    dtype: object




```python
# 前向，后向填充
obj2.reindex(range(6), method='ffill')

```




    0      blue
    1      blue
    2    purple
    3    purple
    4    yellow
    5    yellow
    dtype: object




```python
obj2.reindex(range(6), method='bfill')
```




    0      blue
    1    purple
    2    purple
    3    yellow
    4    yellow
    5       NaN
    dtype: object



### DataFrame的索引重建


```python
frame = pd.DataFrame(np.random.randint(0,100,(3,3)), index = ['语文','数学','英语'], columns = ['张三','李四','王五'])
frame
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
      <th>李四</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81</td>
      <td>37</td>
      <td>36</td>
    </tr>
    <tr>
      <th>数学</th>
      <td>95</td>
      <td>92</td>
      <td>49</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31</td>
      <td>75</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 重建行索引
frame.reindex(['语文', '编程', '英语'])
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
      <th>李四</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81.0</td>
      <td>37.0</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>编程</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31.0</td>
      <td>75.0</td>
      <td>55.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 重建列索引
frame.reindex(['张三', '赵六', '王五'], axis=1)

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
      <th>赵六</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81</td>
      <td>NaN</td>
      <td>36</td>
    </tr>
    <tr>
      <th>数学</th>
      <td>95</td>
      <td>NaN</td>
      <td>49</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31</td>
      <td>NaN</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.reindex(columns=['张三', '赵六', '王五'])
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
      <th>赵六</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81</td>
      <td>NaN</td>
      <td>36</td>
    </tr>
    <tr>
      <th>数学</th>
      <td>95</td>
      <td>NaN</td>
      <td>49</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31</td>
      <td>NaN</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 重建行列索引
frame.reindex(index=['语文', '编程', '英语'], columns=['张三', '赵六', '王五'])
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
      <th>赵六</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81.0</td>
      <td>NaN</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>编程</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31.0</td>
      <td>NaN</td>
      <td>55.0</td>
    </tr>
  </tbody>
</table>
</div>



用查询方式实现重建行列索引的效果


```python
frame
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
      <th>李四</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81</td>
      <td>37</td>
      <td>36</td>
    </tr>
    <tr>
      <th>数学</th>
      <td>95</td>
      <td>92</td>
      <td>49</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31</td>
      <td>75</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.loc[['语文', '编程', '英语'], ['张三', '赵六', '王五']]  # 警告，建议使用reindex方法
```

    D:\Anaconda\anaconda\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: 
    Passing list-likes to .loc or [] with any missing label will raise
    KeyError in the future, you can use .reindex() as an alternative.
    
    See the documentation here:
    https://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate-loc-reindex-listlike
      """Entry point for launching an IPython kernel.
    




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
      <th>赵六</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>语文</th>
      <td>81.0</td>
      <td>NaN</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>编程</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>英语</th>
      <td>31.0</td>
      <td>NaN</td>
      <td>55.0</td>
    </tr>
  </tbody>
</table>
</div>



例2


```python
frame.index = [1,2,4]
frame.columns = [1,2,3]
frame
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>81</td>
      <td>37</td>
      <td>36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>95</td>
      <td>92</td>
      <td>49</td>
    </tr>
    <tr>
      <th>4</th>
      <td>31</td>
      <td>75</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 重建行列索引
frame.reindex(index=[1,2,10,4], columns=[3,1,5,2])

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
      <th>3</th>
      <th>1</th>
      <th>5</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>36.0</td>
      <td>81.0</td>
      <td>NaN</td>
      <td>37.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>49.0</td>
      <td>95.0</td>
      <td>NaN</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>55.0</td>
      <td>31.0</td>
      <td>NaN</td>
      <td>75.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# frame.reindex([1,2,10,4])
frame.reindex([1,2,10,4], method='ffill')  # 前向填充，按实际行索引排序填充
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>81</td>
      <td>37</td>
      <td>36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>95</td>
      <td>92</td>
      <td>49</td>
    </tr>
    <tr>
      <th>10</th>
      <td>31</td>
      <td>75</td>
      <td>55</td>
    </tr>
    <tr>
      <th>4</th>
      <td>31</td>
      <td>75</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>



## 带有重复值的轴索引

许多Pandas函数要求标签唯一，但这不是强制的


```python
obj = pd.Series(range(5), index = ['a','a','b','b','c'])
obj
```




    a    0
    a    1
    b    2
    b    3
    c    4
    dtype: int64




```python
# 重复所有，查询时，会返回所有重复值
obj['a']
```




    a    0
    a    1
    dtype: int64




```python
# 索引的is_unique属性判断索引值是否唯一，不是唯一，那么就会返回 False
obj.index.is_unique
```




    False


