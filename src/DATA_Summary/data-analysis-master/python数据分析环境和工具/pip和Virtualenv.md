
------

Python包管理器pip和环境管理器Virtualenv
===

---

# pip包管理器

Python包/库是Python核心之外的、能够完成某些特定功能的代码集合，供Python使用

* Python自带库：原生自带，不需要安装，载入即可使用
* 第三方库：需要安装
----

附录：Windows 命令窗口的打开/选择/复制/粘贴/停止执行任务操作

* 打开：快捷键`win + R `- 输入`cmd`回车
    * 或者 按住 `Shift` 键，文件夹内鼠标右键-在此处打开命令窗口
* 选择：鼠标右键 - 标记 - 从左向右拖动鼠标选择要选取的文本
* 复制：选取文本后，回车复制
* 粘贴：鼠标右键 粘贴
* 停止执行任务：快捷键`CTRL + C`

常用DOS命令

```python
# 进入某个盘符，如E盘
e:

# 进入子目录
cd m1/m2

# 进入上层目录
cd ../

# 查看本目录列表
dir

```
---
# 用pip管理包

pip是Python3自带的包管理工具，（旧版Python自带包管理器是`easy_install`，如pip无法使用可以备用）

pip官方源网址为：https://pypi.python.org/pypi 可搜索需要的包安装

`注意Linux下系统环境包操作命令一般需要加 sudo`

```python
# 安装包：
pip install 包名

# 升级包：（不存在则安装，已存在则升级(更新)）
pip install -U 包名

# 卸载包：
pip uninstall 包名

# 查看包：
pip show 包名

# 查看已安装包列表：
pip list # 命令执行后顶部警告是可能未来要修改数据输出格式
# 或 pip freeze
```

如果命令返回数据太长无法翻页，可将**输出存入文本文件**，如：

`pip freeze > e:/log123.txt`

##### 某些原因导致包安装不成功时：

* 切换pip软件源地址，见下
* 如果是Windows环境下，下载离线包安装
    * 某些包带有C扩展需要编译（Windows系统缺乏编译环境无法安装）
    * 某些包只支持Py2不支持Python3，可到这里下载编译好的包（whl文件，用于Windows）并使用pip命令本地安装（不能改名）
`pip install e:/包名.whl`

##### 如果pip命令出错无法使用时：

* 执行安装包命令前先退出所有正在运行的Python程序和编辑器
* 还不行尝试使用 `easy_install pip` 命令重新安装pip

-----

# pip修改镜像源地址

当在线安装包无法访问官方源时，（官方pip源 https://pypi.python.org/pypi 有时会被屏蔽无法访问，或访问过慢导致安装失败），可以修改镜像源地址为国内源

* pip豆瓣源（推荐）：https://pypi.doubanio.com/simple/
* pip科大源：https://lug.ustc.edu.cn/wiki/mirrors/help/pypi
* pip清华源：https://mirrors.tuna.tsinghua.edu.cn/help/pypi/


##### 1：个别包安装，可不行地址直接执行下列命令使用国内镜像源安装包

`pip install -i https://pypi.doubanio.com/simple 包名`

##### 2：大量安装，可修改pip下载源为国内源

大量安装，可将pip源地址改为国内源，方便快速下载Python包

修改配置文件，如果没有则在指定目录创建之（新建文本文件再修改后缀）

* Linux/MAC：~/.pip/pip.conf
* Windows：C:\Users\当前用户名\pip\pip.ini

```python
# Linux/MAC操作：

cd ~
mkdir .pip
cd .pip
touch pip.conf
vi pip.conf

# Windows操作
# 普通目录操作
```

打开pip.conf（或pip.ini），写入以下内容，保存

```python
[global]
index-url = https://pypi.doubanio.com/simple
format = columns
```

Pip国内源切换完成


---

# Virtualenv环境管理器

当需要在一个操作系统内同时安装和运行多个Python独立环境（不同版本，不同包）时，可以使用Virtualenv安装和管理多个Python独立子环境

`注意：Virtualenv是Python一个库，使用Virtualenv的前提是你的计算机里至少已经有一个Python环境`

子环境和系统Python环境独立，不互相影响

* 子环境安装的Python解释器时拷贝系统环境的，所以只能安装系统环境已有的Python解释器版本
* 子环境安装的库，默认和系统Python安装的库隔离，互不影响（可在新建子环境时选择继承系统环境库，一般不选）

下面命令仅在Linux下测试通过

```python
# 安装Virtualenv
## Windows安装Virtualenv
pip install virtualenv
## Linux安装Virtualenv
sudo pip3 install virtualenv

# 创建一个目录，终端进入目录后

# 创建一个独立Python环境，命名为venv
# 子环境默认Python版本是安装virtualenv的系统Python版本，这里为Python3.5
virtualenv venvku

# 终端进入子环境，方便管理环境（可以给子环境安装包等）
# 终端进入子环境后前面显示环境名称
## Windows命令
cd venvku/scripts
activate
## Linux命令
source venvku/bin/activate

# 终端退出子环境（回到系统环境，前面显示名称会变）
# Window执行下面命令时终端目录需在venvku/scripts下
deactivate
```

下面是创建子环境的进阶操作：
`注：Virtualenv只能新建系统已有的Python版本环境`

```python
# 如要创建系统其它版本Python，下面命令
# Windows下一般只有一个Python版本环境(Python解释器路径)，下面命令无效
virtualenv -p /usr/bin/python2.7 venv27

# 默认子环境不使用系统Python安装的库，如要子环境能访问系统Python的安装库
# （直接使用系统Python的安装包，不用再次安装，不是将包拷到子环境。不推荐因为这样子环境无法就无法独立，互相影响）
# Windows的Anaconda环境，无效
virtualenv --system-site-packages venvku
# 新建环境包管理独立
virtualenv --no-site-packages venvku
```

---

为使各个Python工程完全独立（独立程序、独立环境（安装库）），推荐每个Python工程都新建一个Python子环境

* 其他方式（交互式、VSCode等）新建的Python工程可直接使用终端命令新建的子环境
* PyCharm新建工程时会默认新建一个Virtualenv子环境，供本工程使用
    * 可以直接使用PyCharm创建的子环境，用终端管理（安装库），推荐
    * 或用终端新建子环境后，PyCharm新建工程时手动选择此子环境









