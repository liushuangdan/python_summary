Python数据课程 软件和环境安装
===

----

Python数据分析相关技术用到的环境、软件和工具的使用

----


安装软件：
---

3个软件

* Python开发/Anaconda3-5.2.0-Windows-x86_64.exe
    * 安装注意：

        1. 用管理员用户登录操作系统安装软件
        1. 安装路径：修改盘符(不要装在C盘，权限问题)，建议不要修改其他路径（路径不能带空格和中文）。如将安装路径改为e:\Anaconda3
        1. 建议选中：
            * add anaconda to the system path environment variable
            * （将anaconda添加到系统路径环境变量）
            * 这样系统终端也能执行Anaconda命令，否则只有Anaconda自带的终端猜能执行命令
        1. 建议选中：
        register anaconda as the system python3.7
        （将Anaconda注册为系统python3.7）
        这样其他Python编辑器、IDE可以找到并使用Anaconda的Python解释器
        1. 最后，选择是否安装 VSCode, skip跳过
            * ###### 注意：选中此项后，Anaconda自带的Python解释器会覆盖系统原来安装的Python，解决方法见后
---
* 检查Anaconda环境是否安装成功：

    1. 快捷键win+R，输入cmd回车，打开系统终端
    1. 输入命令python -V，查看信息
    1. 输入命令conda -V，查看信息
---
* chrome浏览器
    * 设为默认浏览器
    
* VSCode文本编辑器：安装后需联网下载几个插件,插件面板搜索：
    * Chinese ...：中文简体语言包
    * Markdown Preview Enhanced：markdown预览
    * Python ：执行Python程序（需安装Python环境）

---

#### 打开系统终端两种方式
* windows+r - cmd - 回车
    * 进入当前用户系统目录
* 进入目录，shift键，鼠标右键，打开终端
    * 进入本目录

---

#### 测试Anaconda环境是否正常

进入终端，输入命令

```bash
python -V
conda -V

d:
cd Python12/01
dir

jupyter notebook
```

如果执行`jupyter notebook`不自动弹出Chrome浏览器，或者弹出其他浏览器，可以复制终端的URL直接粘贴到Chrome浏览器访问网页
* 终端右键 - 标记
* 鼠标从最左侧到最右侧选中URL，回车复制
* Chrome浏览器上粘贴URL回车访问






