Redis
===

---

> Redis 一个内存数据库，通过 Key-Value 键值对的的方式存储数据。由于 Redis 的数据都存储在内存中，所以访问速度非常快，因此 Redis 大量用于缓存系统，存储热点数据，可以极大的提高网站的响应速度。

![](../images/redis.png)

## 优点

* 支持数据的持久化，通过配置可以将内存中的数据保存在磁盘中，Redis 重启以后再将数据加载到内存中；

* 支持列表，哈希，有序集合等数据结构，极大的扩展了 Redis 用途；

* 原子操作，Redis 的所有操作都是原子性的，这使得基于 Redis 实现分布式锁非常简单；

* 支持发布/订阅功能，数据过期功能；

#### 环境准备

> http://www.runoob.com/redis/redis-install.html


## Ubuntu 下安装

在 Ubuntu 系统安装 Redi 可以使用以下命令:

```bash
$sudo apt-get update
$sudo apt-get install redis-server
```

## Ubuntu 下安装

```bash
$sudo apt-get update
$sudo apt-get install redis-server
```

## 启动 Redis

```bash
$ redis-server
```

## 查看 redis 是否启动

```bash
$ redis-cli
```

##### 以上命令将打开以下终端：

```sql
redis 127.0.0.1:6379>
```

127.0.0.1 是本机 IP ，6379 是 redis 服务端口。现在我们输入 PING 命令。

```sql
redis 127.0.0.1:6379> ping
PONG
```

以上说明我们已经成功安装了redis。