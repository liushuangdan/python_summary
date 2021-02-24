MongoDB
===

----

![](../images/mongodb.png)

> MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。
> 
> MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。


## 什么是MongoDB ?

> MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。
> 
> 在高负载的情况下，添加更多的节点，可以保证服务器性能。
> 
> MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。
> 
> MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。> MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

## 主要特点

* MongoDB的提供了一个面向文档存储，操作起来比较简单和容易。
* 你可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
* 你可以通过本地或者网络创建数据镜像，这使得MongoDB有更强的扩展性。
* 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
* Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
* MongoDb 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
* Mongodb中的Map/reduce主要是用来对数据进行批量处理和聚合操作。
* Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
* Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
* GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
* MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
* MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
* MongoDB安装简单。

## ubuntu16.04通过apt-get方式安装MongoDB

虽然Ubuntu本身也提供MongoDB安装包，但往往官网的安装包版本更新。

```bash
~$ apt-cache show mongodb-clients
Package: mongodb-clients
Priority: optional
Section: universe/database
Installed-Size: 160066
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Laszlo Boszormenyi (GCS) <gcs@debian.org>
Architecture: amd64
Source: mongodb
Version: 1:2.6.10-0ubuntu1   # 版本号
```

* ### 安装

    * #### 1.导入包管理系统使用的公钥

        ```bash
        sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
        ```

    * #### 2.为MongoDB创建一个列表文件
        根据版本创建/etc/apt/sources.list.d/mongodb-org-3.4.list 列表文件

        Ubuntu 16.04

        ```bash
        echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
        ```

    * #### 3.更新本地包数据库

        ```bash
        sudo apt-get update
        ```

    * #### 4.安装最新版本的MongoDB

        ```bash
        sudo apt-get install -y mongodb-org
        ```

    * #### 5.查看配置文件

        ```bash
        配置文件mongod.conf所在路径:

        /etc/mongod.conf

        内容:
        ```

        ```sql
        #mongod.conf

        #for documentation of all options, see:
        #http://docs.mongodb.org/manual/reference/configuration-options/

        #Where and how to store data.
        storage:
        dbPath: /var/lib/mongodb   #数据库存储路径
        journal:
            enabled: true
        #engine:
        #mmapv1:
        #wiredTiger:
        ```

        ```sql
        # where to write logging data.
        systemLog:
        destination: file
        logAppend: true     #以追加的方式写入日志
        path: /var/log/mongodb/mongod.log   #日志文件路径

        #network interfaces
        net:
        port: 27017
        bindIp: 127.0.0.1   #绑定监听的ip 127.0.0.1只能监听本地的连接，可以改为0.0.0.0

        #processManagement:

        #security:

        #operationProfiling:

        #replication:

        #sharding:

        ## Enterprise-Only Options:

        #auditLog:

        #snmp:
        ```

    * #### 6.启动和关闭MongoDB

        ```sql
        sudo service mongod start  # 启动
        sudo service mongod stop   # 关闭
        ```
        ```
        hupeng@hupeng-vm:~$ ps aux | grep mongod   # 查看守护进程mongod的运行状态
        mongodb   18454  9.5  1.5 292152 61952 ?        Ssl  12:27   0:00 /usr/bin/mongod --quiet --config /etc/mongod.conf
        hupeng    18475  0.0  0.0  15964   936 pts/4    R+   12:27   0:00 grep --color=auto mongod
        ```

* ### 卸载

    * #### 1.关闭守护进程mongod

        ```bash
        sudo service mongod stop
        ```

    * #### 2.卸载安装的软件包

        ```bash
        sudo apt-get purge mongodb-org*
        ```

    * #### 3.移除数据库和日志文件（数据库和日志文件的路径取决于/etc/mongod.conf文件中的配置)

        ```bash
        sudo rm -r /var/log/
        mongodb
        sudo rm 
        -r /var/lib/mongodb
        ```

> 参考文档: https://docs.mongodb.com/master/tutorial/install-mongodb-on-ubuntu/