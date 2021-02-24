
Pandas数据存取
===

---

数据的输入和输出是Pandas的基础操作

Pandas可以存取多种介质类型数据：常见的有：

* 文本类数据
    * csv
    * JSON
* 二进制磁盘数据
    * Excel
    * pkl
    * HDF5
* 数据库
    * SQL（略）
* Web API数据
    * HTML
* 其他
    * 内存

---

文本类数据文件读入Pandas时会自动推断每列数据类型（类型推断）并转化。

二进制类数据文件会在格式中存储数据类型

对Pandas不能直接支持或不方便使用的数据格式，

可以使用支持软件将其转为csv或xlsx格式后使用Pandas读写，如SPSS文件



```python
import numpy as np
import pandas as pd
```


```python
av = [
    ['小明','male',18,170,60,'北京海淀',61],
    ['小华','female',28,160,50,'上海静安',74],
    ['小红','female',22,175,64,'广州天河',59],
    ['小靑','male',31,182,80,'深圳南山',82],
    ['小兰','female',25,165,55,'杭州西湖',98],
]
a = pd.DataFrame(
    av,
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




```python
a.info()
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
    


```python
df = pd.DataFrame(np.random.randn(1000, 4),columns=['A', 'B', 'C', 'D'])
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
      <td>0.971470</td>
      <td>-0.910323</td>
      <td>0.559249</td>
      <td>1.075287</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.354050</td>
      <td>-0.557734</td>
      <td>-1.302378</td>
      <td>1.464031</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.181755</td>
      <td>0.838199</td>
      <td>-0.103647</td>
      <td>-0.239950</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.797444</td>
      <td>-0.784848</td>
      <td>-0.878766</td>
      <td>1.070386</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.393892</td>
      <td>-0.894993</td>
      <td>1.104146</td>
      <td>-0.550882</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.991452</td>
      <td>-0.571119</td>
      <td>-0.225624</td>
      <td>-0.898736</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.213550</td>
      <td>0.765152</td>
      <td>-0.328068</td>
      <td>0.715214</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-2.738036</td>
      <td>-0.073490</td>
      <td>-0.054538</td>
      <td>-0.589355</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-1.739574</td>
      <td>0.265254</td>
      <td>-0.516565</td>
      <td>-0.944410</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.116646</td>
      <td>0.318442</td>
      <td>0.899953</td>
      <td>-0.672622</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.406266</td>
      <td>0.139849</td>
      <td>-0.146476</td>
      <td>-0.332747</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.688098</td>
      <td>0.912993</td>
      <td>0.889713</td>
      <td>-0.272609</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.734708</td>
      <td>-0.509685</td>
      <td>1.374228</td>
      <td>0.487075</td>
    </tr>
    <tr>
      <th>13</th>
      <td>-0.620682</td>
      <td>-0.425317</td>
      <td>1.334744</td>
      <td>-0.339170</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-1.272188</td>
      <td>-2.378728</td>
      <td>-0.451680</td>
      <td>0.674662</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.308439</td>
      <td>-1.242873</td>
      <td>1.985861</td>
      <td>-1.760328</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.326332</td>
      <td>-0.308578</td>
      <td>0.022306</td>
      <td>0.905072</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-1.250010</td>
      <td>-0.773064</td>
      <td>0.284679</td>
      <td>0.910661</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-0.187829</td>
      <td>-1.038055</td>
      <td>1.337365</td>
      <td>1.416580</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.724382</td>
      <td>3.070201</td>
      <td>-0.678422</td>
      <td>-0.600846</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.229085</td>
      <td>-0.513108</td>
      <td>0.643235</td>
      <td>-0.164983</td>
    </tr>
    <tr>
      <th>21</th>
      <td>-0.496122</td>
      <td>2.355930</td>
      <td>0.872267</td>
      <td>-1.342849</td>
    </tr>
    <tr>
      <th>22</th>
      <td>0.025463</td>
      <td>1.008532</td>
      <td>-1.297462</td>
      <td>1.878374</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1.491304</td>
      <td>-0.303352</td>
      <td>0.203386</td>
      <td>1.531170</td>
    </tr>
    <tr>
      <th>24</th>
      <td>0.086712</td>
      <td>-1.054256</td>
      <td>0.916509</td>
      <td>0.150382</td>
    </tr>
    <tr>
      <th>25</th>
      <td>-0.367296</td>
      <td>-0.250115</td>
      <td>0.607016</td>
      <td>-1.941563</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.346743</td>
      <td>0.059370</td>
      <td>-1.414952</td>
      <td>-1.172916</td>
    </tr>
    <tr>
      <th>27</th>
      <td>-0.081799</td>
      <td>-0.498255</td>
      <td>-1.550495</td>
      <td>-0.949339</td>
    </tr>
    <tr>
      <th>28</th>
      <td>0.593236</td>
      <td>1.344904</td>
      <td>1.152445</td>
      <td>0.566880</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2.321404</td>
      <td>-0.298681</td>
      <td>-0.481925</td>
      <td>0.912140</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>-0.143725</td>
      <td>0.183996</td>
      <td>0.453441</td>
      <td>-1.440529</td>
    </tr>
    <tr>
      <th>971</th>
      <td>0.045530</td>
      <td>0.104548</td>
      <td>-0.721135</td>
      <td>1.640193</td>
    </tr>
    <tr>
      <th>972</th>
      <td>-0.725313</td>
      <td>-0.302477</td>
      <td>0.103637</td>
      <td>0.299864</td>
    </tr>
    <tr>
      <th>973</th>
      <td>1.643769</td>
      <td>0.673424</td>
      <td>1.785893</td>
      <td>1.061021</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2.206223</td>
      <td>-2.170208</td>
      <td>-0.402996</td>
      <td>-0.890067</td>
    </tr>
    <tr>
      <th>975</th>
      <td>1.451025</td>
      <td>-0.065624</td>
      <td>0.166981</td>
      <td>-0.309620</td>
    </tr>
    <tr>
      <th>976</th>
      <td>-0.122171</td>
      <td>-1.778694</td>
      <td>-3.048161</td>
      <td>-1.799536</td>
    </tr>
    <tr>
      <th>977</th>
      <td>-0.605187</td>
      <td>0.509859</td>
      <td>-0.378514</td>
      <td>0.252206</td>
    </tr>
    <tr>
      <th>978</th>
      <td>0.780935</td>
      <td>0.351821</td>
      <td>0.938628</td>
      <td>1.076653</td>
    </tr>
    <tr>
      <th>979</th>
      <td>0.470542</td>
      <td>1.353116</td>
      <td>-0.432134</td>
      <td>1.287247</td>
    </tr>
    <tr>
      <th>980</th>
      <td>-1.488928</td>
      <td>1.260615</td>
      <td>-1.211009</td>
      <td>1.523660</td>
    </tr>
    <tr>
      <th>981</th>
      <td>-0.031728</td>
      <td>0.392340</td>
      <td>0.910436</td>
      <td>-1.383338</td>
    </tr>
    <tr>
      <th>982</th>
      <td>-0.995186</td>
      <td>-1.093517</td>
      <td>-0.300063</td>
      <td>0.493835</td>
    </tr>
    <tr>
      <th>983</th>
      <td>0.792182</td>
      <td>-0.267352</td>
      <td>1.390696</td>
      <td>1.498959</td>
    </tr>
    <tr>
      <th>984</th>
      <td>-0.794723</td>
      <td>1.052508</td>
      <td>-1.113050</td>
      <td>0.101865</td>
    </tr>
    <tr>
      <th>985</th>
      <td>-1.027141</td>
      <td>-1.199244</td>
      <td>-0.990809</td>
      <td>-1.395599</td>
    </tr>
    <tr>
      <th>986</th>
      <td>-0.969678</td>
      <td>-1.167831</td>
      <td>-0.854208</td>
      <td>-1.183604</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1.609280</td>
      <td>0.767694</td>
      <td>0.506747</td>
      <td>0.041865</td>
    </tr>
    <tr>
      <th>988</th>
      <td>1.367448</td>
      <td>2.697807</td>
      <td>-1.199477</td>
      <td>-0.086055</td>
    </tr>
    <tr>
      <th>989</th>
      <td>-0.390024</td>
      <td>-2.051293</td>
      <td>0.910944</td>
      <td>-0.460113</td>
    </tr>
    <tr>
      <th>990</th>
      <td>-0.821939</td>
      <td>-1.416562</td>
      <td>-0.685051</td>
      <td>-0.521237</td>
    </tr>
    <tr>
      <th>991</th>
      <td>-0.287810</td>
      <td>0.808191</td>
      <td>0.293922</td>
      <td>-0.085264</td>
    </tr>
    <tr>
      <th>992</th>
      <td>0.466382</td>
      <td>2.880704</td>
      <td>2.343967</td>
      <td>-0.243972</td>
    </tr>
    <tr>
      <th>993</th>
      <td>0.175811</td>
      <td>-0.547227</td>
      <td>0.242304</td>
      <td>-1.290218</td>
    </tr>
    <tr>
      <th>994</th>
      <td>0.225000</td>
      <td>-0.321088</td>
      <td>-0.074606</td>
      <td>-0.336083</td>
    </tr>
    <tr>
      <th>995</th>
      <td>-1.198251</td>
      <td>0.777643</td>
      <td>-1.145068</td>
      <td>0.721212</td>
    </tr>
    <tr>
      <th>996</th>
      <td>1.061066</td>
      <td>-0.883506</td>
      <td>0.780252</td>
      <td>0.657456</td>
    </tr>
    <tr>
      <th>997</th>
      <td>-0.423743</td>
      <td>-0.674806</td>
      <td>1.540011</td>
      <td>0.863288</td>
    </tr>
    <tr>
      <th>998</th>
      <td>-0.482636</td>
      <td>0.732125</td>
      <td>0.428839</td>
      <td>0.038669</td>
    </tr>
    <tr>
      <th>999</th>
      <td>1.576860</td>
      <td>0.727269</td>
      <td>1.560673</td>
      <td>0.291709</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>



---

Pandas存取CSV
---

* CSV

    * Comma-Separated Values，逗号分隔值
    
    * 以纯文本形式存储表格数据的一种格式
    
    * 二维表格数据结构
    
CSV是一种简单、通用的文件格式，常用于在不同程序和环境之间中转表格数据，

这些程序本身是在不兼容的格式上进行操作的（往往是私有的和/或无规范的格式），

基本所有数据类软件和环境都支持读写CSV文件

---

CSV表格：ceshi.csv

name,age,address,grade

张三,18,"aaa,bbb",60

张三,18,"北,京",60

张三,18,北京,60



```python
pd.read_csv('ceshi.csv',encoding='GBK')
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
      <th>address</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>18</td>
      <td>aaa,bbb</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>张三</td>
      <td>18</td>
      <td>北,京</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>



## 写入CSV
* 默认是utf-8格式
* 保存其他格式

注意：Excel打开utf-8的csv文件，中文会乱码，建议保存为gbk


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




```python
a.to_csv('foo.csv')  #默认是utf-8的编码格式。
```


```python
a.to_csv('foo2.csv',encoding='GBK')
```

## 读取CSV
注意文本文件编码格式问题

* UTF-8，默认支持
* 其他编码，需要手动设置参数 encoding



```python
pd.read_csv('foo.csv')   #utf-8 格式，默认打开
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
      <th>Unnamed: 0</th>
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
      <th>0</th>
      <td>1</td>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
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
pd.read_csv('foo2.csv',encoding='GBK')  #除默认utf-8编码文件外，其他编码格式需要手动指定编码。
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
      <th>Unnamed: 0</th>
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
      <th>0</th>
      <td>1</td>
      <td>小明</td>
      <td>male</td>
      <td>18</td>
      <td>170</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>小华</td>
      <td>female</td>
      <td>28</td>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>小红</td>
      <td>female</td>
      <td>22</td>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>小靑</td>
      <td>male</td>
      <td>31</td>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
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



## 进阶：csv写入很热读取的常见参数设置



写入csv设置


```python
a.to_csv(
    'foo3.csv',
    index = False,  #不保存行索引
    header= False,  #不保存列索引。
    columns = ['name','address','grade'],  #只保存指定列
    
)
```


```python
a2 = pd.read_csv('foo3.csv')
a2
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
      <th>小明</th>
      <th>北京海淀</th>
      <th>61</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小华</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>小红</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小靑</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>小兰</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 读取后列类型正常
a2.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4 entries, 0 to 3
    Data columns (total 3 columns):
    小明      4 non-null object
    北京海淀    4 non-null object
    61      4 non-null int64
    dtypes: int64(1), object(2)
    memory usage: 176.0+ bytes
    

### 读取csv常见设置


```python
a3 = pd.read_csv(
    'foo.csv', #读取文件路径 因为在同级目录下，所以是直接写文件名。
    sep=',',#指定分隔符，csv默认逗号，如果是table表格数据一般为\t。
    
    #列索引
#     header = 0 ,# 列索引，默认0将第一行设为表头(其他行号也可以),
    #header=None,  # None不将第一行设为表头（列索引），
    
#     header=[0,1,2],  # [0,1]列表可将多行同时设为表头（层次化索引）
#     names=['x','姓名', '性别', '年龄', '身高', '体重', '地址', '成绩'],  # 配合header=0，自定义列索引    
    
    
    # 行索引
    #index_col=None,  # 行索引，默认值None：不使用数据列，而是使用系统自带索引
    
#     index_col=0,  # 1,2,3使用某列（默认列索引）作为行索引
    index_col=['name','sex','age'],  # （自定义多列 作为层次化索引），
#     index_col=[0,1,2,3],
    
    #读取指定的行和列
#     usecols = [0,2,4], #读取指定列。默认索引
#     usecols=['name', 'address', 'grade'],  # 读取指定列，自定义索引
#     nrows=3,  # 读取前几行
#     skiprows=3, # 从表格开始算起，忽略的行
#     skiprows=[2,4]  # [2,3,4]跳过文件第2/3/4行
#     skipfooter=2,  # 从表格末尾算起忽略的行，必须配合engine='python'否则会报警告
#     engine='python',  # 引擎。c更快，python更完善
    
    # 替换空值
#     na_values=['male'],  # 将csv中某些字符替换为空值
#     keep_default_na=True,  # 默认True同时使用系统自带空值替换和自定义空值，如 NA,N/A等，False只使用自定义空值

    encoding='utf-8',  # 编码，默认utf-8,引擎是python时需要手动设置    
    
    
    )
a3
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
      <th></th>
      <th>Unnamed: 0</th>
      <th>heigh</th>
      <th>weight</th>
      <th>address</th>
      <th>grade</th>
    </tr>
    <tr>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>小明</th>
      <th>male</th>
      <th>18</th>
      <td>1</td>
      <td>170</td>
      <td>60</td>
      <td>北京海淀</td>
      <td>61</td>
    </tr>
    <tr>
      <th>小华</th>
      <th>female</th>
      <th>28</th>
      <td>2</td>
      <td>160</td>
      <td>50</td>
      <td>上海静安</td>
      <td>74</td>
    </tr>
    <tr>
      <th>小红</th>
      <th>female</th>
      <th>22</th>
      <td>3</td>
      <td>175</td>
      <td>64</td>
      <td>广州天河</td>
      <td>59</td>
    </tr>
    <tr>
      <th>小靑</th>
      <th>male</th>
      <th>31</th>
      <td>4</td>
      <td>182</td>
      <td>80</td>
      <td>深圳南山</td>
      <td>82</td>
    </tr>
    <tr>
      <th>小兰</th>
      <th>female</th>
      <th>25</th>
      <td>5</td>
      <td>165</td>
      <td>55</td>
      <td>杭州西湖</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
#层次化索引读取
# header=[0,1,2],  # [0,1]列表可将多行同时设为表头（层次化索引）
#需要把索引设置成这种层次索引
a3['name']['小明']['小华'][0]
```




    '小红'




```python
a3.loc['小明'].loc['male'].loc[18]['address']
```




    '北京海淀'



 合并时间列及自定义某列为行索引
 ---
 
多用于时间序列，金融数据分析

参数：parse_dates

尝试将数据解析为日期

可以使用列表指定需要解析的一组列名，如果列表元素为字典包含的列表或元组，会将多个列组合到一起再解析日期解析（如日期和时间分别在两个列的情况）

参数：keep_date_col

如果连接多列解析日期，保存参与连接的列，默认False

---

数据：**aaa.csv**

data,time,time2,name,age

20100101,000000,00:00:00,"张三",18

20100101,230000,23:00:00,"李,四",28



```python
t = pd.read_csv ('aaa.csv',encoding='GBK')
t
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
      <th>data</th>
      <th>time</th>
      <th>time2</th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20100101</td>
      <td>0</td>
      <td>00:00:00</td>
      <td>张三</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20100101</td>
      <td>230000</td>
      <td>23:00:00</td>
      <td>李,四</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>




```python
t.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2 entries, 0 to 1
    Data columns (total 5 columns):
    data     2 non-null int64
    time     2 non-null int64
    time2    2 non-null object
    name     2 non-null object
    age      2 non-null int64
    dtypes: int64(3), object(2)
    memory usage: 160.0+ bytes
    


```python
# 手动处理将时间列转为时间类型

t = pd.read_csv(
    'aaa.csv',
#     parse_dates = ['data'],#指定某列解析为时间格式
#     parse_dates=['data', 'time', 'time2'],  # 指定多列解析为时间，不是所有格式都能正确解析 
    parse_dates = {'s': ['data','time2']},
    keep_date_col=True,  # 保留合并前的列
    index_col='s',  # 指定某列作为行索引
    encoding='GBK',
)
t


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
      <th>data</th>
      <th>time</th>
      <th>time2</th>
      <th>name</th>
      <th>age</th>
    </tr>
    <tr>
      <th>s</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-01 00:00:00</th>
      <td>20100101</td>
      <td>0</td>
      <td>00:00:00</td>
      <td>张三</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2010-01-01 23:00:00</th>
      <td>20100101</td>
      <td>230000</td>
      <td>23:00:00</td>
      <td>李,四</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>



# Pandas存取Excel（xlsx）

写入


```python
df.head()
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
      <td>0.971470</td>
      <td>-0.910323</td>
      <td>0.559249</td>
      <td>1.075287</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.354050</td>
      <td>-0.557734</td>
      <td>-1.302378</td>
      <td>1.464031</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.181755</td>
      <td>0.838199</td>
      <td>-0.103647</td>
      <td>-0.239950</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.797444</td>
      <td>-0.784848</td>
      <td>-0.878766</td>
      <td>1.070386</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.393892</td>
      <td>-0.894993</td>
      <td>1.104146</td>
      <td>-0.550882</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.to_excel('foo.xlsx')
```


```python
df.to_excel('foo1.xlsx','abc')  #自定义工作表表名，默认是sheet1
df.to_excel('foo1.xlsx',sheet_name='abc') #同上
```

将多个变量写入同一Excel多个工作表中


```python
#复杂写法

#创建表格
writer = pd.ExcelWriter('output.xlsx')

#增加单元表
a.to_excel(
    writer,
    'Sheet1',
)
df.to_excel(
    writer,
    'sheet2',   #工作表表名
    index = 0,  #不要行索引
    header = None,  #不要咧索引
)

#写入
writer.save()

```

读取


```python
# e = pd.read_excel('output.xlsx')   #默认读取第一个工作表
# e = pd.read_excel('output.xlsx','Sheet1')  #指定读取某个工作表
e = pd.read_excel('output.xlsx',None)  #读取所有工作表
e
e['Sheet1']

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
# e.info()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-139-618380ce167a> in <module>()
    ----> 1 e.info()
    

    AttributeError: 'collections.OrderedDict' object has no attribute 'info'


### 复杂读取参数



```python
x = pd.read_excel(
    
    'output.xlsx',
    
#     sheet_name=1,  # 工作表名，默认第一个工作表,注意新版pandas是sheet_name
#     sheet_name=[0,1],  # 选中的多个工作表，按照索引来查看的。
    sheet_name=None,  # 所有的工作表

#     header=None,  # 不使用行做列索引
#     header=1,  # 使用某行做列索引
#     header=[0,1,2],  # 多行做层次化索引
    
#     index_col=1,  # 不设行索引，多个[1,2,3]层次化索引
    
#     nrows=3,  # 读取前多少行(pandas0.23.0新版才支持)
#     skiprows=[2,4],  # 跳过的行，从表起始位置算，[2,4]列表参数也可
#     skipfooter=2,  # 跳过的行，从表结束位置算，默认为0，不能用列表

#     na_values='male',# 表示为NAN,na_values可以用一个列表或集合的字符串表示缺失值
#     keep_default_na=True, # 默认True在系统自带空值替换符后追加NA值，如 NA,N/A等，False只使用自定义空值
)

x

```




    OrderedDict([('Sheet1',   name     sex  age  heigh  weight address  grade
                  1   小明    male   18    170      60    北京海淀     61
                  2   小华  female   28    160      50    上海静安     74
                  3   小红  female   22    175      64    广州天河     59
                  4   小靑    male   31    182      80    深圳南山     82
                  5   小兰  female   25    165      55    杭州西湖     98),
                 ('sheet2',       0.971470  -0.910323   0.559249   1.075287
                  0    -1.354050  -0.557734  -1.302378   1.464031
                  1     1.181755   0.838199  -0.103647  -0.239950
                  2    -0.797444  -0.784848  -0.878766   1.070386
                  3     0.393892  -0.894993   1.104146  -0.550882
                  4    -0.991452  -0.571119  -0.225624  -0.898736
                  5     1.213550   0.765152  -0.328068   0.715214
                  6    -2.738036  -0.073490  -0.054538  -0.589355
                  7    -1.739574   0.265254  -0.516565  -0.944410
                  8    -0.116646   0.318442   0.899953  -0.672622
                  9    -0.406266   0.139849  -0.146476  -0.332747
                  10   -0.688098   0.912993   0.889713  -0.272609
                  11   -0.734708  -0.509685   1.374228   0.487075
                  12   -0.620682  -0.425317   1.334744  -0.339170
                  13   -1.272188  -2.378728  -0.451680   0.674662
                  14    0.308439  -1.242873   1.985861  -1.760328
                  15   -0.326332  -0.308578   0.022306   0.905072
                  16   -1.250010  -0.773064   0.284679   0.910661
                  17   -0.187829  -1.038055   1.337365   1.416580
                  18    0.724382   3.070201  -0.678422  -0.600846
                  19    0.229085  -0.513108   0.643235  -0.164983
                  20   -0.496122   2.355930   0.872267  -1.342849
                  21    0.025463   1.008532  -1.297462   1.878374
                  22    1.491304  -0.303352   0.203386   1.531170
                  23    0.086712  -1.054256   0.916509   0.150382
                  24   -0.367296  -0.250115   0.607016  -1.941563
                  25   -0.346743   0.059370  -1.414952  -1.172916
                  26   -0.081799  -0.498255  -1.550495  -0.949339
                  27    0.593236   1.344904   1.152445   0.566880
                  28    2.321404  -0.298681  -0.481925   0.912140
                  29   -0.047032  -0.731323  -0.402732  -1.129732
                  ..         ...        ...        ...        ...
                  969  -0.143725   0.183996   0.453441  -1.440529
                  970   0.045530   0.104548  -0.721135   1.640193
                  971  -0.725313  -0.302477   0.103637   0.299864
                  972   1.643769   0.673424   1.785893   1.061021
                  973   2.206223  -2.170208  -0.402996  -0.890067
                  974   1.451025  -0.065624   0.166981  -0.309620
                  975  -0.122171  -1.778694  -3.048161  -1.799536
                  976  -0.605187   0.509859  -0.378514   0.252206
                  977   0.780935   0.351821   0.938628   1.076653
                  978   0.470542   1.353116  -0.432134   1.287247
                  979  -1.488928   1.260615  -1.211009   1.523660
                  980  -0.031728   0.392340   0.910436  -1.383338
                  981  -0.995186  -1.093517  -0.300063   0.493835
                  982   0.792182  -0.267352   1.390696   1.498959
                  983  -0.794723   1.052508  -1.113050   0.101865
                  984  -1.027141  -1.199244  -0.990809  -1.395599
                  985  -0.969678  -1.167831  -0.854208  -1.183604
                  986   1.609280   0.767694   0.506747   0.041865
                  987   1.367448   2.697807  -1.199477  -0.086055
                  988  -0.390024  -2.051293   0.910944  -0.460113
                  989  -0.821939  -1.416562  -0.685051  -0.521237
                  990  -0.287810   0.808191   0.293922  -0.085264
                  991   0.466382   2.880704   2.343967  -0.243972
                  992   0.175811  -0.547227   0.242304  -1.290218
                  993   0.225000  -0.321088  -0.074606  -0.336083
                  994  -1.198251   0.777643  -1.145068   0.721212
                  995   1.061066  -0.883506   0.780252   0.657456
                  996  -0.423743  -0.674806   1.540011   0.863288
                  997  -0.482636   0.732125   0.428839   0.038669
                  998   1.576860   0.727269   1.560673   0.291709
                  
                  [999 rows x 4 columns])])




```python
x['sheet2']
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
      <th>0.9714695310733813</th>
      <th>-0.9103226300144159</th>
      <th>0.5592492516125814</th>
      <th>1.075286593165145</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.354050</td>
      <td>-0.557734</td>
      <td>-1.302378</td>
      <td>1.464031</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.181755</td>
      <td>0.838199</td>
      <td>-0.103647</td>
      <td>-0.239950</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.797444</td>
      <td>-0.784848</td>
      <td>-0.878766</td>
      <td>1.070386</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.393892</td>
      <td>-0.894993</td>
      <td>1.104146</td>
      <td>-0.550882</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.991452</td>
      <td>-0.571119</td>
      <td>-0.225624</td>
      <td>-0.898736</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.213550</td>
      <td>0.765152</td>
      <td>-0.328068</td>
      <td>0.715214</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-2.738036</td>
      <td>-0.073490</td>
      <td>-0.054538</td>
      <td>-0.589355</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.739574</td>
      <td>0.265254</td>
      <td>-0.516565</td>
      <td>-0.944410</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.116646</td>
      <td>0.318442</td>
      <td>0.899953</td>
      <td>-0.672622</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.406266</td>
      <td>0.139849</td>
      <td>-0.146476</td>
      <td>-0.332747</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.688098</td>
      <td>0.912993</td>
      <td>0.889713</td>
      <td>-0.272609</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.734708</td>
      <td>-0.509685</td>
      <td>1.374228</td>
      <td>0.487075</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.620682</td>
      <td>-0.425317</td>
      <td>1.334744</td>
      <td>-0.339170</td>
    </tr>
    <tr>
      <th>13</th>
      <td>-1.272188</td>
      <td>-2.378728</td>
      <td>-0.451680</td>
      <td>0.674662</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.308439</td>
      <td>-1.242873</td>
      <td>1.985861</td>
      <td>-1.760328</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-0.326332</td>
      <td>-0.308578</td>
      <td>0.022306</td>
      <td>0.905072</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-1.250010</td>
      <td>-0.773064</td>
      <td>0.284679</td>
      <td>0.910661</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.187829</td>
      <td>-1.038055</td>
      <td>1.337365</td>
      <td>1.416580</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.724382</td>
      <td>3.070201</td>
      <td>-0.678422</td>
      <td>-0.600846</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.229085</td>
      <td>-0.513108</td>
      <td>0.643235</td>
      <td>-0.164983</td>
    </tr>
    <tr>
      <th>20</th>
      <td>-0.496122</td>
      <td>2.355930</td>
      <td>0.872267</td>
      <td>-1.342849</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0.025463</td>
      <td>1.008532</td>
      <td>-1.297462</td>
      <td>1.878374</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1.491304</td>
      <td>-0.303352</td>
      <td>0.203386</td>
      <td>1.531170</td>
    </tr>
    <tr>
      <th>23</th>
      <td>0.086712</td>
      <td>-1.054256</td>
      <td>0.916509</td>
      <td>0.150382</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-0.367296</td>
      <td>-0.250115</td>
      <td>0.607016</td>
      <td>-1.941563</td>
    </tr>
    <tr>
      <th>25</th>
      <td>-0.346743</td>
      <td>0.059370</td>
      <td>-1.414952</td>
      <td>-1.172916</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.081799</td>
      <td>-0.498255</td>
      <td>-1.550495</td>
      <td>-0.949339</td>
    </tr>
    <tr>
      <th>27</th>
      <td>0.593236</td>
      <td>1.344904</td>
      <td>1.152445</td>
      <td>0.566880</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2.321404</td>
      <td>-0.298681</td>
      <td>-0.481925</td>
      <td>0.912140</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.047032</td>
      <td>-0.731323</td>
      <td>-0.402732</td>
      <td>-1.129732</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>969</th>
      <td>-0.143725</td>
      <td>0.183996</td>
      <td>0.453441</td>
      <td>-1.440529</td>
    </tr>
    <tr>
      <th>970</th>
      <td>0.045530</td>
      <td>0.104548</td>
      <td>-0.721135</td>
      <td>1.640193</td>
    </tr>
    <tr>
      <th>971</th>
      <td>-0.725313</td>
      <td>-0.302477</td>
      <td>0.103637</td>
      <td>0.299864</td>
    </tr>
    <tr>
      <th>972</th>
      <td>1.643769</td>
      <td>0.673424</td>
      <td>1.785893</td>
      <td>1.061021</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2.206223</td>
      <td>-2.170208</td>
      <td>-0.402996</td>
      <td>-0.890067</td>
    </tr>
    <tr>
      <th>974</th>
      <td>1.451025</td>
      <td>-0.065624</td>
      <td>0.166981</td>
      <td>-0.309620</td>
    </tr>
    <tr>
      <th>975</th>
      <td>-0.122171</td>
      <td>-1.778694</td>
      <td>-3.048161</td>
      <td>-1.799536</td>
    </tr>
    <tr>
      <th>976</th>
      <td>-0.605187</td>
      <td>0.509859</td>
      <td>-0.378514</td>
      <td>0.252206</td>
    </tr>
    <tr>
      <th>977</th>
      <td>0.780935</td>
      <td>0.351821</td>
      <td>0.938628</td>
      <td>1.076653</td>
    </tr>
    <tr>
      <th>978</th>
      <td>0.470542</td>
      <td>1.353116</td>
      <td>-0.432134</td>
      <td>1.287247</td>
    </tr>
    <tr>
      <th>979</th>
      <td>-1.488928</td>
      <td>1.260615</td>
      <td>-1.211009</td>
      <td>1.523660</td>
    </tr>
    <tr>
      <th>980</th>
      <td>-0.031728</td>
      <td>0.392340</td>
      <td>0.910436</td>
      <td>-1.383338</td>
    </tr>
    <tr>
      <th>981</th>
      <td>-0.995186</td>
      <td>-1.093517</td>
      <td>-0.300063</td>
      <td>0.493835</td>
    </tr>
    <tr>
      <th>982</th>
      <td>0.792182</td>
      <td>-0.267352</td>
      <td>1.390696</td>
      <td>1.498959</td>
    </tr>
    <tr>
      <th>983</th>
      <td>-0.794723</td>
      <td>1.052508</td>
      <td>-1.113050</td>
      <td>0.101865</td>
    </tr>
    <tr>
      <th>984</th>
      <td>-1.027141</td>
      <td>-1.199244</td>
      <td>-0.990809</td>
      <td>-1.395599</td>
    </tr>
    <tr>
      <th>985</th>
      <td>-0.969678</td>
      <td>-1.167831</td>
      <td>-0.854208</td>
      <td>-1.183604</td>
    </tr>
    <tr>
      <th>986</th>
      <td>1.609280</td>
      <td>0.767694</td>
      <td>0.506747</td>
      <td>0.041865</td>
    </tr>
    <tr>
      <th>987</th>
      <td>1.367448</td>
      <td>2.697807</td>
      <td>-1.199477</td>
      <td>-0.086055</td>
    </tr>
    <tr>
      <th>988</th>
      <td>-0.390024</td>
      <td>-2.051293</td>
      <td>0.910944</td>
      <td>-0.460113</td>
    </tr>
    <tr>
      <th>989</th>
      <td>-0.821939</td>
      <td>-1.416562</td>
      <td>-0.685051</td>
      <td>-0.521237</td>
    </tr>
    <tr>
      <th>990</th>
      <td>-0.287810</td>
      <td>0.808191</td>
      <td>0.293922</td>
      <td>-0.085264</td>
    </tr>
    <tr>
      <th>991</th>
      <td>0.466382</td>
      <td>2.880704</td>
      <td>2.343967</td>
      <td>-0.243972</td>
    </tr>
    <tr>
      <th>992</th>
      <td>0.175811</td>
      <td>-0.547227</td>
      <td>0.242304</td>
      <td>-1.290218</td>
    </tr>
    <tr>
      <th>993</th>
      <td>0.225000</td>
      <td>-0.321088</td>
      <td>-0.074606</td>
      <td>-0.336083</td>
    </tr>
    <tr>
      <th>994</th>
      <td>-1.198251</td>
      <td>0.777643</td>
      <td>-1.145068</td>
      <td>0.721212</td>
    </tr>
    <tr>
      <th>995</th>
      <td>1.061066</td>
      <td>-0.883506</td>
      <td>0.780252</td>
      <td>0.657456</td>
    </tr>
    <tr>
      <th>996</th>
      <td>-0.423743</td>
      <td>-0.674806</td>
      <td>1.540011</td>
      <td>0.863288</td>
    </tr>
    <tr>
      <th>997</th>
      <td>-0.482636</td>
      <td>0.732125</td>
      <td>0.428839</td>
      <td>0.038669</td>
    </tr>
    <tr>
      <th>998</th>
      <td>1.576860</td>
      <td>0.727269</td>
      <td>1.560673</td>
      <td>0.291709</td>
    </tr>
  </tbody>
</table>
<p>999 rows × 4 columns</p>
</div>




```python
x['Sheet1']
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




-------------------------------------

# Json

### JSON（JavaScript Object Notation）是通过HTTP请求在Web浏览器和其他应用程序之间发送数据的标准格式之一

#### JSON和CSV比较：

JSON是多维数据文件，CSV是二维数据文件

JSON数据比较冗余，体积较大，CSV精简，体积小

JSON多用于WEB数据交互，CSV多用于计算机软件程序数据交互

如果JSON数据格式维度超过2维，转为DataFrame后，只能将0/1维转为表格，其他维度的JSON会存入表格单元格


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



写入


```python
a.to_json('foo.json')
```

读取


```python
pd.read_json('foo.json')
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



----

Pandas存取pkl
===


pkl是Python专有的二进制数据存储格式，可以存储原生的Python数据类型


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




```python
a.to_pickle('foo.pkl')
```


```python
p = pd.read_pickle('foo.pkl')
p
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
p.info()
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
    


----

使用HDF5格式
===

科学领域大数据存储的通行标准，如天文、物理、地球科学等


```python
frame = pd.DataFrame({'a': np.random.randn(100)})
frame.loc[:10]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.545833</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.331485</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.011306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.085044</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.623065</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.581317</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.029992</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.337090</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.907710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.884964</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.453825</td>
    </tr>
  </tbody>
</table>
</div>



简单读取


```python
#存储
frame.to_hdf('mydata.h5','obj1')

```


```python
#读取
x = pd.read_hdf('mydata.h5')  # 文件内只存储了一个变量,如果多个变量读取出错
x.loc[:10]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.545833</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.331485</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.011306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.085044</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.623065</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.581317</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.029992</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.337090</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.907710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.884964</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.453825</td>
    </tr>
  </tbody>
</table>
</div>




```python
x = pd.read_hdf('mydata.h5','obj1')  # 指定变量名输出
x.loc[:10]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.545833</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.331485</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.011306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.085044</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.623065</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.581317</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.029992</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.337090</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.907710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.884964</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.453825</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 设置存储模式，默认fixed
frame.to_hdf('mydata2.h5', 'obj1', format='table')
```


```python
# 高级查询模式，只能在table模式下实现
x = pd.read_hdf('mydata2.h5','obj1', where=['index < 5 and index > 1'])
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
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>1.011306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.085044</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.623065</td>
    </tr>
  </tbody>
</table>
</div>



复杂应用


```python
# 创建或读取HDF5文件（没有就创建，有就读取）
store = pd.HDFStore('mydata3.h5')
store
```




    <class 'pandas.io.pytables.HDFStore'>
    File path: mydata3.h5




```python
# 插入数据到h5
store['obj1'] = frame
store
```




    <class 'pandas.io.pytables.HDFStore'>
    File path: mydata3.h5




```python
# 继续插入
store['obj1_col'] = frame['a']
store
```




    <class 'pandas.io.pytables.HDFStore'>
    File path: mydata3.h5




```python
#读取
store['obj1']
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.545833</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.331485</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.011306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.085044</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-1.623065</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.581317</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.029992</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.337090</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.907710</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.884964</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.453825</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.722596</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.609966</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.187275</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-0.430286</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.521102</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.382130</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.047734</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-1.036313</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.666919</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.439724</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1.998140</td>
    </tr>
    <tr>
      <th>22</th>
      <td>-0.636233</td>
    </tr>
    <tr>
      <th>23</th>
      <td>0.910963</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-1.197317</td>
    </tr>
    <tr>
      <th>25</th>
      <td>-0.475087</td>
    </tr>
    <tr>
      <th>26</th>
      <td>0.629060</td>
    </tr>
    <tr>
      <th>27</th>
      <td>0.458871</td>
    </tr>
    <tr>
      <th>28</th>
      <td>-2.026899</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.207946</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>-0.805222</td>
    </tr>
    <tr>
      <th>71</th>
      <td>-0.102193</td>
    </tr>
    <tr>
      <th>72</th>
      <td>-0.030742</td>
    </tr>
    <tr>
      <th>73</th>
      <td>0.973290</td>
    </tr>
    <tr>
      <th>74</th>
      <td>0.462811</td>
    </tr>
    <tr>
      <th>75</th>
      <td>2.006082</td>
    </tr>
    <tr>
      <th>76</th>
      <td>-1.640565</td>
    </tr>
    <tr>
      <th>77</th>
      <td>0.111313</td>
    </tr>
    <tr>
      <th>78</th>
      <td>0.523204</td>
    </tr>
    <tr>
      <th>79</th>
      <td>-0.193813</td>
    </tr>
    <tr>
      <th>80</th>
      <td>2.143838</td>
    </tr>
    <tr>
      <th>81</th>
      <td>0.765496</td>
    </tr>
    <tr>
      <th>82</th>
      <td>-1.459714</td>
    </tr>
    <tr>
      <th>83</th>
      <td>-0.611186</td>
    </tr>
    <tr>
      <th>84</th>
      <td>0.148676</td>
    </tr>
    <tr>
      <th>85</th>
      <td>-1.896926</td>
    </tr>
    <tr>
      <th>86</th>
      <td>-2.152605</td>
    </tr>
    <tr>
      <th>87</th>
      <td>0.340162</td>
    </tr>
    <tr>
      <th>88</th>
      <td>-0.819917</td>
    </tr>
    <tr>
      <th>89</th>
      <td>-0.989251</td>
    </tr>
    <tr>
      <th>90</th>
      <td>0.901735</td>
    </tr>
    <tr>
      <th>91</th>
      <td>-0.310940</td>
    </tr>
    <tr>
      <th>92</th>
      <td>0.330087</td>
    </tr>
    <tr>
      <th>93</th>
      <td>-1.592673</td>
    </tr>
    <tr>
      <th>94</th>
      <td>1.602411</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.448390</td>
    </tr>
    <tr>
      <th>96</th>
      <td>-0.831902</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1.803686</td>
    </tr>
    <tr>
      <th>98</th>
      <td>0.704141</td>
    </tr>
    <tr>
      <th>99</th>
      <td>-0.497465</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 1 columns</p>
</div>




```python
store['obj1_col'] = frame['a']
store
```




    <class 'pandas.io.pytables.HDFStore'>
    File path: mydata3.h5




```python
#读取
store['obj1_col'][:10]
```




    0   -1.545833
    1   -0.331485
    2    1.011306
    3   -0.085044
    4   -1.623065
    5    0.581317
    6   -0.029992
    7   -0.337090
    8    1.907710
    9   -0.884964
    Name: a, dtype: float64



高级用法


```python
# put 是直接复制的显示版本，可以自定义格式化格式

store.put('obj2',frame,format = 'table')
store
```




    <class 'pandas.io.pytables.HDFStore'>
    File path: mydata3.h5




```python
# select 是高级版读取，可以增加查询条件
store.select('obj2',where = ['index >= 10 and index <= 20'])
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>-0.453825</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.722596</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.609966</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.187275</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-0.430286</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.521102</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.382130</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.047734</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-1.036313</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.666919</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.439724</td>
    </tr>
  </tbody>
</table>
</div>




------

XML和HTML：Web信息收集
===

网页中有多个表格的，返回列表，可按列表索引逐个输出

* 有些网站由于网络原因、反爬虫、服务器原因导致无法抓取网页内容，400、500错误，这时可以将网页另存到本地后读取
* 有些网站的表格HTML结构复杂混乱，导致解析表格结构出错，只能手动处理


```python
#table = pd.read_html('http://www.stats.gov.cn/tjsj/zxfb/201806/t20180630_1607071.html')  # 某些网络下无法抓取

table = pd.read_html('2018年6月中国采购经理指数运行情况.html')  # 保存到本地读取
table
```




    [           0     1       2     3        4     5     6
     0       单位：%   NaN     NaN   NaN      NaN   NaN   NaN
     1        NaN   PMI     NaN   NaN      NaN   NaN   NaN
     2         生产   新订单  原材料 库存  从业人员  供应商配送时间   NaN   NaN
     3    2017年6月  51.7    54.4  53.1     48.6  49.0  49.9
     4    2017年7月  51.4    53.5  52.8     48.5  49.2  50.1
     5    2017年8月  51.7    54.1  53.1     48.3  49.1  49.3
     6    2017年9月  52.4    54.7  54.8     48.9  49.0  49.3
     7   2017年10月  51.6    53.4  52.9     48.6  49.0  48.7
     8   2017年11月  51.8    54.3  53.6     48.4  48.8  49.5
     9   2017年12月  51.6    54.0  53.4     48.0  48.5  49.3
     10   2018年1月  51.3    53.5  52.6     48.8  48.3  49.2
     11   2018年2月  50.3    50.7  51.0     49.3  48.1  48.4
     12   2018年3月  51.5    53.1  53.3     49.6  49.1  50.1
     13   2018年4月  51.4    53.1  52.9     49.5  49.0  50.2
     14   2018年5月  51.9    54.1  53.8     49.6  49.1  50.1
     15   2018年6月  51.5    53.6  53.2     48.8  49.0  50.2,
                0       1     2     3          4      5       6      7         8
     0       单位：%     NaN   NaN   NaN        NaN    NaN     NaN    NaN       NaN
     1        NaN  新出口 订单    进口   采购量  主要原材料购进价格  出厂 价格  产成品 库存  在手 订单  生产经营活动预期
     2    2017年6月    52.0  51.2  52.5       50.4   49.1    46.3   47.2      58.7
     3    2017年7月    50.9  51.1  52.7       57.9   52.7    46.1   46.3      59.1
     4    2017年8月    50.4  51.4  52.9       65.3   57.4    45.5   46.1      59.5
     5    2017年9月    51.3  51.1  53.8       68.4   59.4    44.2   47.4      59.4
     6   2017年10月    50.1  50.3  53.2       63.4   55.2    46.1   45.6      57.0
     7   2017年11月    50.8  51.0  53.5       59.8   53.8    46.1   46.6      57.9
     8   2017年12月    51.9  51.2  53.6       62.2   54.4    45.8   46.3      58.7
     9    2018年1月    49.5  50.4  52.9       59.7   51.8    47.0   45.3      56.8
     10   2018年2月    49.0  49.8  50.8       53.4   49.2    46.7   44.9      58.2
     11   2018年3月    51.3  51.3  53.0       53.4   48.9    47.3   46.0      58.7
     12   2018年4月    50.7  50.2  52.6       53.0   50.2    47.2   46.2      58.4
     13   2018年5月    51.2  50.9  53.0       56.7   53.2    46.1   45.9      58.7
     14   2018年6月    49.8  50.0  52.8       57.7   53.3    46.3   45.5      57.9,
                0     1     2       3     4     5        6
     0       单位：%   NaN   NaN     NaN   NaN   NaN      NaN
     1        NaN  商务活动   新订单  投入品 价格  销售价格  从业人员  业务活动 预期
     2    2017年6月  54.9  51.4    51.2  49.3  49.6     61.1
     3    2017年7月  54.5  51.1    53.1  50.9  49.5     61.1
     4    2017年8月  53.4  50.9    54.4  51.5  49.5     61.0
     5    2017年9月  55.4  52.3    56.1  51.7  49.7     61.7
     6   2017年10月  54.3  51.1    54.3  51.6  49.4     60.6
     7   2017年11月  54.8  51.8    56.2  52.8  49.2     61.6
     8   2017年12月  55.0  52.0    54.8  52.6  49.3     60.9
     9    2018年1月  55.3  51.9    53.9  52.6  49.4     61.7
     10   2018年2月  54.4  50.5    53.2  49.9  49.6     61.2
     11   2018年3月  54.6  50.1    49.9  49.3  49.2     61.1
     12   2018年4月  54.8  51.1    52.7  50.6  49.0     61.5
     13   2018年5月  54.9  51.0    54.2  50.6  49.2     61.0
     14   2018年6月  55.0  50.6    53.5  51.1  48.9     60.8,
                0      1     2     3        4
     0       单位：%    NaN   NaN   NaN      NaN
     1        NaN  新出口订单  在手订单    存货  供应商配送时间
     2    2017年6月   49.8  44.6  45.9     51.8
     3    2017年7月   52.1  43.9  45.9     51.7
     4    2017年8月   49.0  44.0  45.5     51.1
     5    2017年9月   49.7  44.2  47.0     51.6
     6   2017年10月   50.7  43.9  46.4     51.1
     7   2017年11月   50.9  44.1  46.5     51.6
     8   2017年12月   51.5  43.8  46.3     51.3
     9    2018年1月   50.1  44.4  46.5     51.3
     10   2018年2月   45.9  43.8  47.6     50.7
     11   2018年3月   50.4  44.3  46.2     51.6
     12   2018年4月   50.0  44.4  46.7     51.5
     13   2018年5月   49.1  44.1  46.0     51.7
     14   2018年6月   48.2  44.0  46.4     51.6,
                                                        0  \
     0  document.write(unescape("%3Cspan id='_ideConac...   
     
                                                        1   2  
     0  版权所有：中华人民共和国国家统计局  地址：北京市西城区月坛南街57号（100826）  京... NaN  ]




```python
table[0]
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
      <th>5</th>
      <th>6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>单位：%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>PMI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>生产</td>
      <td>新订单</td>
      <td>原材料 库存</td>
      <td>从业人员</td>
      <td>供应商配送时间</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017年6月</td>
      <td>51.7</td>
      <td>54.4</td>
      <td>53.1</td>
      <td>48.6</td>
      <td>49.0</td>
      <td>49.9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017年7月</td>
      <td>51.4</td>
      <td>53.5</td>
      <td>52.8</td>
      <td>48.5</td>
      <td>49.2</td>
      <td>50.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017年8月</td>
      <td>51.7</td>
      <td>54.1</td>
      <td>53.1</td>
      <td>48.3</td>
      <td>49.1</td>
      <td>49.3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017年9月</td>
      <td>52.4</td>
      <td>54.7</td>
      <td>54.8</td>
      <td>48.9</td>
      <td>49.0</td>
      <td>49.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年10月</td>
      <td>51.6</td>
      <td>53.4</td>
      <td>52.9</td>
      <td>48.6</td>
      <td>49.0</td>
      <td>48.7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017年11月</td>
      <td>51.8</td>
      <td>54.3</td>
      <td>53.6</td>
      <td>48.4</td>
      <td>48.8</td>
      <td>49.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2017年12月</td>
      <td>51.6</td>
      <td>54.0</td>
      <td>53.4</td>
      <td>48.0</td>
      <td>48.5</td>
      <td>49.3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018年1月</td>
      <td>51.3</td>
      <td>53.5</td>
      <td>52.6</td>
      <td>48.8</td>
      <td>48.3</td>
      <td>49.2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018年2月</td>
      <td>50.3</td>
      <td>50.7</td>
      <td>51.0</td>
      <td>49.3</td>
      <td>48.1</td>
      <td>48.4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018年3月</td>
      <td>51.5</td>
      <td>53.1</td>
      <td>53.3</td>
      <td>49.6</td>
      <td>49.1</td>
      <td>50.1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018年4月</td>
      <td>51.4</td>
      <td>53.1</td>
      <td>52.9</td>
      <td>49.5</td>
      <td>49.0</td>
      <td>50.2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018年5月</td>
      <td>51.9</td>
      <td>54.1</td>
      <td>53.8</td>
      <td>49.6</td>
      <td>49.1</td>
      <td>50.1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2018年6月</td>
      <td>51.5</td>
      <td>53.6</td>
      <td>53.2</td>
      <td>48.8</td>
      <td>49.0</td>
      <td>50.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
table[1]
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
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>单位：%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>新出口 订单</td>
      <td>进口</td>
      <td>采购量</td>
      <td>主要原材料购进价格</td>
      <td>出厂 价格</td>
      <td>产成品 库存</td>
      <td>在手 订单</td>
      <td>生产经营活动预期</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017年6月</td>
      <td>52.0</td>
      <td>51.2</td>
      <td>52.5</td>
      <td>50.4</td>
      <td>49.1</td>
      <td>46.3</td>
      <td>47.2</td>
      <td>58.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017年7月</td>
      <td>50.9</td>
      <td>51.1</td>
      <td>52.7</td>
      <td>57.9</td>
      <td>52.7</td>
      <td>46.1</td>
      <td>46.3</td>
      <td>59.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017年8月</td>
      <td>50.4</td>
      <td>51.4</td>
      <td>52.9</td>
      <td>65.3</td>
      <td>57.4</td>
      <td>45.5</td>
      <td>46.1</td>
      <td>59.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017年9月</td>
      <td>51.3</td>
      <td>51.1</td>
      <td>53.8</td>
      <td>68.4</td>
      <td>59.4</td>
      <td>44.2</td>
      <td>47.4</td>
      <td>59.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017年10月</td>
      <td>50.1</td>
      <td>50.3</td>
      <td>53.2</td>
      <td>63.4</td>
      <td>55.2</td>
      <td>46.1</td>
      <td>45.6</td>
      <td>57.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年11月</td>
      <td>50.8</td>
      <td>51.0</td>
      <td>53.5</td>
      <td>59.8</td>
      <td>53.8</td>
      <td>46.1</td>
      <td>46.6</td>
      <td>57.9</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017年12月</td>
      <td>51.9</td>
      <td>51.2</td>
      <td>53.6</td>
      <td>62.2</td>
      <td>54.4</td>
      <td>45.8</td>
      <td>46.3</td>
      <td>58.7</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018年1月</td>
      <td>49.5</td>
      <td>50.4</td>
      <td>52.9</td>
      <td>59.7</td>
      <td>51.8</td>
      <td>47.0</td>
      <td>45.3</td>
      <td>56.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018年2月</td>
      <td>49.0</td>
      <td>49.8</td>
      <td>50.8</td>
      <td>53.4</td>
      <td>49.2</td>
      <td>46.7</td>
      <td>44.9</td>
      <td>58.2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018年3月</td>
      <td>51.3</td>
      <td>51.3</td>
      <td>53.0</td>
      <td>53.4</td>
      <td>48.9</td>
      <td>47.3</td>
      <td>46.0</td>
      <td>58.7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018年4月</td>
      <td>50.7</td>
      <td>50.2</td>
      <td>52.6</td>
      <td>53.0</td>
      <td>50.2</td>
      <td>47.2</td>
      <td>46.2</td>
      <td>58.4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018年5月</td>
      <td>51.2</td>
      <td>50.9</td>
      <td>53.0</td>
      <td>56.7</td>
      <td>53.2</td>
      <td>46.1</td>
      <td>45.9</td>
      <td>58.7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018年6月</td>
      <td>49.8</td>
      <td>50.0</td>
      <td>52.8</td>
      <td>57.7</td>
      <td>53.3</td>
      <td>46.3</td>
      <td>45.5</td>
      <td>57.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
table[2]
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
      <th>5</th>
      <th>6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>单位：%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>商务活动</td>
      <td>新订单</td>
      <td>投入品 价格</td>
      <td>销售价格</td>
      <td>从业人员</td>
      <td>业务活动 预期</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017年6月</td>
      <td>54.9</td>
      <td>51.4</td>
      <td>51.2</td>
      <td>49.3</td>
      <td>49.6</td>
      <td>61.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017年7月</td>
      <td>54.5</td>
      <td>51.1</td>
      <td>53.1</td>
      <td>50.9</td>
      <td>49.5</td>
      <td>61.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017年8月</td>
      <td>53.4</td>
      <td>50.9</td>
      <td>54.4</td>
      <td>51.5</td>
      <td>49.5</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017年9月</td>
      <td>55.4</td>
      <td>52.3</td>
      <td>56.1</td>
      <td>51.7</td>
      <td>49.7</td>
      <td>61.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017年10月</td>
      <td>54.3</td>
      <td>51.1</td>
      <td>54.3</td>
      <td>51.6</td>
      <td>49.4</td>
      <td>60.6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年11月</td>
      <td>54.8</td>
      <td>51.8</td>
      <td>56.2</td>
      <td>52.8</td>
      <td>49.2</td>
      <td>61.6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017年12月</td>
      <td>55.0</td>
      <td>52.0</td>
      <td>54.8</td>
      <td>52.6</td>
      <td>49.3</td>
      <td>60.9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018年1月</td>
      <td>55.3</td>
      <td>51.9</td>
      <td>53.9</td>
      <td>52.6</td>
      <td>49.4</td>
      <td>61.7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018年2月</td>
      <td>54.4</td>
      <td>50.5</td>
      <td>53.2</td>
      <td>49.9</td>
      <td>49.6</td>
      <td>61.2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018年3月</td>
      <td>54.6</td>
      <td>50.1</td>
      <td>49.9</td>
      <td>49.3</td>
      <td>49.2</td>
      <td>61.1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018年4月</td>
      <td>54.8</td>
      <td>51.1</td>
      <td>52.7</td>
      <td>50.6</td>
      <td>49.0</td>
      <td>61.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018年5月</td>
      <td>54.9</td>
      <td>51.0</td>
      <td>54.2</td>
      <td>50.6</td>
      <td>49.2</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018年6月</td>
      <td>55.0</td>
      <td>50.6</td>
      <td>53.5</td>
      <td>51.1</td>
      <td>48.9</td>
      <td>60.8</td>
    </tr>
  </tbody>
</table>
</div>




```python
table[3]
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
      <td>单位：%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>新出口订单</td>
      <td>在手订单</td>
      <td>存货</td>
      <td>供应商配送时间</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017年6月</td>
      <td>49.8</td>
      <td>44.6</td>
      <td>45.9</td>
      <td>51.8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017年7月</td>
      <td>52.1</td>
      <td>43.9</td>
      <td>45.9</td>
      <td>51.7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017年8月</td>
      <td>49.0</td>
      <td>44.0</td>
      <td>45.5</td>
      <td>51.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017年9月</td>
      <td>49.7</td>
      <td>44.2</td>
      <td>47.0</td>
      <td>51.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017年10月</td>
      <td>50.7</td>
      <td>43.9</td>
      <td>46.4</td>
      <td>51.1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年11月</td>
      <td>50.9</td>
      <td>44.1</td>
      <td>46.5</td>
      <td>51.6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017年12月</td>
      <td>51.5</td>
      <td>43.8</td>
      <td>46.3</td>
      <td>51.3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018年1月</td>
      <td>50.1</td>
      <td>44.4</td>
      <td>46.5</td>
      <td>51.3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018年2月</td>
      <td>45.9</td>
      <td>43.8</td>
      <td>47.6</td>
      <td>50.7</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018年3月</td>
      <td>50.4</td>
      <td>44.3</td>
      <td>46.2</td>
      <td>51.6</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018年4月</td>
      <td>50.0</td>
      <td>44.4</td>
      <td>46.7</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018年5月</td>
      <td>49.1</td>
      <td>44.1</td>
      <td>46.0</td>
      <td>51.7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018年6月</td>
      <td>48.2</td>
      <td>44.0</td>
      <td>46.4</td>
      <td>51.6</td>
    </tr>
  </tbody>
</table>
</div>



Pandas从剪贴板（内存）读取数据
===

多用于将网页表格内容直接转换为 DataFrame

从下方的html地址中进入到HTML中，然后选中要复制的表格内容，然后右击鼠标选择复制

最后在下面的读取 clipboard中的数据的代码 运行一下，就可以读出内存中的数据


```python
#  https://cn.investing.com/currencies/usd-cny-historical-data

pd.read_clipboard(header=None, engine='python')
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
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018年10月15日</td>
      <td>6.9194</td>
      <td>6.9222</td>
      <td>6.9302</td>
      <td>6.9164</td>
      <td>-0.04%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018年10月14日</td>
      <td>6.9222</td>
      <td>6.9222</td>
      <td>6.9222</td>
      <td>6.9222</td>
      <td>-0.00%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018年10月12日</td>
      <td>6.9225</td>
      <td>6.8914</td>
      <td>6.9322</td>
      <td>6.8914</td>
      <td>0.47%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018年10月11日</td>
      <td>6.8899</td>
      <td>6.9243</td>
      <td>6.9350</td>
      <td>6.8899</td>
      <td>-0.50%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018年10月10日</td>
      <td>6.9242</td>
      <td>6.9227</td>
      <td>6.9258</td>
      <td>6.9169</td>
      <td>0.02%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018年10月9日</td>
      <td>6.9227</td>
      <td>6.9300</td>
      <td>6.9300</td>
      <td>6.9082</td>
      <td>-0.12%</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2018年10月8日</td>
      <td>6.9307</td>
      <td>6.9040</td>
      <td>6.9338</td>
      <td>6.8947</td>
      <td>0.90%</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2018年10月7日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018年10月5日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018年10月4日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018年10月3日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018年10月2日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018年10月1日</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018年9月30日</td>
      <td>6.8689</td>
      <td>6.8690</td>
      <td>6.8690</td>
      <td>6.8689</td>
      <td>0.00%</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018年9月28日</td>
      <td>6.8689</td>
      <td>6.8872</td>
      <td>6.8905</td>
      <td>6.8678</td>
      <td>-0.31%</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2018年9月27日</td>
      <td>6.8902</td>
      <td>6.8788</td>
      <td>6.8933</td>
      <td>6.8700</td>
      <td>0.17%</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2018年9月26日</td>
      <td>6.8786</td>
      <td>6.8748</td>
      <td>6.8803</td>
      <td>6.8708</td>
      <td>0.18%</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2018年9月25日</td>
      <td>6.8665</td>
      <td>6.8608</td>
      <td>6.8842</td>
      <td>6.8605</td>
      <td>0.14%</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2018年9月24日</td>
      <td>6.8571</td>
      <td>6.8571</td>
      <td>6.8571</td>
      <td>6.8571</td>
      <td>-0.01%</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2018年9月23日</td>
      <td>6.8578</td>
      <td>6.8577</td>
      <td>6.8578</td>
      <td>6.8576</td>
      <td>0.01%</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2018年9月21日</td>
      <td>6.8571</td>
      <td>6.8357</td>
      <td>6.8604</td>
      <td>6.8337</td>
      <td>0.15%</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2018年9月20日</td>
      <td>6.8468</td>
      <td>6.8515</td>
      <td>6.8583</td>
      <td>6.8403</td>
      <td>-0.02%</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2018年9月19日</td>
      <td>6.8483</td>
      <td>6.8653</td>
      <td>6.8676</td>
      <td>6.8473</td>
      <td>-0.19%</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2018年9月18日</td>
      <td>6.8616</td>
      <td>6.8552</td>
      <td>6.8807</td>
      <td>6.8552</td>
      <td>0.07%</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2018年9月17日</td>
      <td>6.8570</td>
      <td>6.8695</td>
      <td>6.8781</td>
      <td>6.8558</td>
      <td>-0.14%</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2018年9月16日</td>
      <td>6.8666</td>
      <td>6.8709</td>
      <td>6.8709</td>
      <td>6.8654</td>
      <td>-0.03%</td>
    </tr>
  </tbody>
</table>
</div>




```python
# http://www.stats.gov.cn/tjsj/zxfb/201806/t20180630_1607071.html
# 解析表格出错，需要手动处理
pd.read_clipboard(header=None, engine='python')
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
      <td>2017年6月</td>
    </tr>
    <tr>
      <th>1</th>
      <td>51.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>54.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>53.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>48.6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>49.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>49.9</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年7月</td>
    </tr>
    <tr>
      <th>8</th>
      <td>51.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>53.5</td>
    </tr>
    <tr>
      <th>10</th>
      <td>52.8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>48.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>49.2</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2017年8月</td>
    </tr>
    <tr>
      <th>15</th>
      <td>51.7</td>
    </tr>
    <tr>
      <th>16</th>
      <td>54.1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>53.1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>48.3</td>
    </tr>
    <tr>
      <th>19</th>
      <td>49.1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>49.3</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2017年9月</td>
    </tr>
    <tr>
      <th>22</th>
      <td>52.4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>54.7</td>
    </tr>
    <tr>
      <th>24</th>
      <td>54.8</td>
    </tr>
    <tr>
      <th>25</th>
      <td>48.9</td>
    </tr>
    <tr>
      <th>26</th>
      <td>49.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>49.3</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2017年10月</td>
    </tr>
    <tr>
      <th>29</th>
      <td>51.6</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>61</th>
      <td>48.1</td>
    </tr>
    <tr>
      <th>62</th>
      <td>48.4</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2018年3月</td>
    </tr>
    <tr>
      <th>64</th>
      <td>51.5</td>
    </tr>
    <tr>
      <th>65</th>
      <td>53.1</td>
    </tr>
    <tr>
      <th>66</th>
      <td>53.3</td>
    </tr>
    <tr>
      <th>67</th>
      <td>49.6</td>
    </tr>
    <tr>
      <th>68</th>
      <td>49.1</td>
    </tr>
    <tr>
      <th>69</th>
      <td>50.1</td>
    </tr>
    <tr>
      <th>70</th>
      <td>2018年4月</td>
    </tr>
    <tr>
      <th>71</th>
      <td>51.4</td>
    </tr>
    <tr>
      <th>72</th>
      <td>53.1</td>
    </tr>
    <tr>
      <th>73</th>
      <td>52.9</td>
    </tr>
    <tr>
      <th>74</th>
      <td>49.5</td>
    </tr>
    <tr>
      <th>75</th>
      <td>49.0</td>
    </tr>
    <tr>
      <th>76</th>
      <td>50.2</td>
    </tr>
    <tr>
      <th>77</th>
      <td>2018年5月</td>
    </tr>
    <tr>
      <th>78</th>
      <td>51.9</td>
    </tr>
    <tr>
      <th>79</th>
      <td>54.1</td>
    </tr>
    <tr>
      <th>80</th>
      <td>53.8</td>
    </tr>
    <tr>
      <th>81</th>
      <td>49.6</td>
    </tr>
    <tr>
      <th>82</th>
      <td>49.1</td>
    </tr>
    <tr>
      <th>83</th>
      <td>50.1</td>
    </tr>
    <tr>
      <th>84</th>
      <td>2018年6月</td>
    </tr>
    <tr>
      <th>85</th>
      <td>51.5</td>
    </tr>
    <tr>
      <th>86</th>
      <td>53.6</td>
    </tr>
    <tr>
      <th>87</th>
      <td>53.2</td>
    </tr>
    <tr>
      <th>88</th>
      <td>48.8</td>
    </tr>
    <tr>
      <th>89</th>
      <td>49.0</td>
    </tr>
    <tr>
      <th>90</th>
      <td>50.2</td>
    </tr>
  </tbody>
</table>
<p>91 rows × 1 columns</p>
</div>


