关于pylab
====

---

大量旧版教学资料代码，常在IPython或Jupyter执行代码前使用魔术命令：

`%pylab inline`

或者使用命令行打开IPython和Jupyter Notebook时，增加参数：

`ipython --pylab`
`jupyter notebook --pylab=inline`

此命令自动载入常用Python科学计算库，等同于在页面载入：

```python
import numpy
import matplotlib
from matplotlib import pylab, mlab, pyplot
np = numpy
plt = pyplot

from IPython.core.pylabtools import figsize, getfigs

from pylab import *
from numpy import 
```
* 这种传统载入方式模拟了MATLAB代码的写法
    * 优点：让软件一开始就进入科学计算环境，方便程序员从传统数据环境切换到Python
    * 缺点：污染命名空间，载入后除非重启环境否则无法卸除，代码只能在iPython类的特定环境执行，换个Python环境即执行失败，不建议使用
* 注意：大量旧版资料和代码必须在此载入环境下才能执行成功

非IPython环境可以用下面代码载入pylab

* Python原生环境、Pycharm或Spyder集成模式下:from pylab import *
* 或者直接将交互终端设置为IPython即可


