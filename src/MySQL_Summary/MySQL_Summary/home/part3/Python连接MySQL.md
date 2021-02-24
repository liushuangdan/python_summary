Python3 MySQL 数据库连接
===

---

MySQL 可应用于多种语言，包括 PERL, C, C++, JAVA 和 PHP

* ### 什么是 PyMySQL？


```sql
PyMySQL 是在 Python3.x 版本中用于连接 MySQL 服务器的一个库，Python2中则使用mysqldb。

PyMySQL 遵循 Python 数据库 API v2.0 规范，并包含了 pure-Python MySQL 客户端库。
```

* ### PyMySQL 安装

```bash
在使用 PyMySQL 之前，我们需要确保 PyMySQL 已安装。

PyMySQL 下载地址：https://github.com/PyMySQL/PyMySQL。

如果还未安装，我们可以使用以下命令安装最新版的 PyMySQL：

$ pip3 install PyMySQL
```


* ### 数据库连接

> 通过如下代码测试数据库连接

```python
 #!/usr/bin/python3

 import pymysql

 # 打开数据库连接
 db = pymysql.connect("localhost","root","123456","mydb" )

 # 使用 cursor() 方法创建一个游标对象 cursor
 cursor = db.cursor()

 # 使用 execute()  方法执行 SQL 查询 
 cursor.execute("SELECT VERSION()")

 # 使用 fetchone() 方法获取单条数据.
 data = cursor.fetchone()

 print ("Database version : %s " % data)

 # 关闭数据库连接
 db.close()
```

## 连接数据库可选参数

```python
pymysql 链接数据库

参数1，mysql服务器的地址  参数2 登录mysql的用户名  参数3 登录的密码 参数4 选择的库 5.设置编码 6，设置返回的数据格式 

db = pymysql.connect(
    '127.0.0.1',
    'root',
    '123456',
    'py10',
    charset='utf8',
    cursorclass=pymysql.cursors.DictCursor
    )
```


