
Pandas数据规整-重塑和轴向旋转
===

----

有许多用于重新排列表格型数据的基础运算。这些函数也称作重塑（reshape）或轴向旋转（pivot）运算。

数据重塑和轴向旋转操作：表示转换一个表格或向量的结构，使其适合于进一步的分析

## 重塑层次化索引

---

层次化索引为DataFrame数据的重排任务提供了一种具有良好一致性的方式。主要功能有二：

stack：列转行，将数据的列“旋转”为行

    （少用一般用于将DataFrame转为层次化Series用）

** unstack **：行转列，将数据的行“旋转”为列 

    （常用：一般用于将层次化Series转为DataFrame）

    二者互为逆运算
    


 Series 没有stack属性


```python
import numpy as np
import pandas as pd
```


```python
# 一个行列索引都带name的DataFrame对象
data = pd.DataFrame(
    np.arange(6).reshape((2, 3)),
    index=pd.Index(['Ohio','Colorado'], name='state'),
    columns=pd.Index(['one', 'two', 'three'], name='number')
)
data
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
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.index
```




    Index(['Ohio', 'Colorado'], dtype='object', name='state')




```python
data.columns
```




    Index(['one', 'two', 'three'], dtype='object', name='number')



## stack：列转行，将数据的列“旋转”为行索引

列索引，逆时针转为行索引


```python
data
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
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 列转行，stack方法将列转换为行，得到一个Series
result = data.stack()
result
```




    state     number
    Ohio      one       0
              two       1
              three     2
    Colorado  one       3
              two       4
              three     5
    dtype: int32



## unstack：行转列，将数据的行“旋转”为列

 对层次化索引的Series，可以用unstack将其重排为一个DataFrame


```python
result.unstack()
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
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.unstack()  #先把航索引顺时针旋转插入原来的列索引，然后再将整个Series逆时针旋转，摔倒，结果
```




    number  state   
    one     Ohio        0
            Colorado    3
    two     Ohio        1
            Colorado    4
    three   Ohio        2
            Colorado    5
    dtype: int32




```python
# result.stack()   #报错。Series  对象没有列，所以没有Stack（） 方法
```


```python
result
```




    state     number
    Ohio      one       0
              two       1
              three     2
    Colorado  one       3
              two       4
              three     5
    dtype: int32



### unstack默认操作的是最内层（stack也是如此）。传入分层级别的编号或name即可对其它级别进行unstack操作


```python
result
```




    state     number
    Ohio      one       0
              two       1
              three     2
    Colorado  one       3
              two       4
              three     5
    dtype: int32




```python
result.unstack()   #默认旋转最里层索引

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
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.unstack(0)   #旋转第0层索引，最外层
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
      <th>state</th>
      <th>Ohio</th>
      <th>Colorado</th>
    </tr>
    <tr>
      <th>number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.unstack('state')  # 写索引name也行
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
      <th>state</th>
      <th>Ohio</th>
      <th>Colorado</th>
    </tr>
    <tr>
      <th>number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.unstack().unstack()  #变为一个新的表，但是这个时候是将原表行和列交换
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
      <th>state</th>
      <th>Ohio</th>
      <th>Colorado</th>
    </tr>
    <tr>
      <th>number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



小总结：
* 可以将一个DataFrame类型的层次化索引进行stack或者unstack
    * data.stack()
    * data.unstack()
* 但是不能将其stack或者unstack之后得到的Series类型进行stack操作
    * data.stack（）之后
        * data.stack().unstack()即为恢复原格式
        * data.stack().stack() 不能进行此操作，会报错
    * data.unstack()之后
        * data.unstack().unstack()变为一个新的表，其实就是将原表行和列交换
        * data.unstack().stack() 不能进行此操作，会报错
 


