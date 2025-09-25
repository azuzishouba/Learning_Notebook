# Redis数据库笔记
## Redis简介
Redis（Remote Dictionary Server）是一个开源的内存数据库，遵守 BSD 协议，它提供了一个高性能的键值（key-value）存储系统，常用于缓存、消息队列、会话存储等应用场景。

* **性能极高**：Redis 以其极高的性能而著称，能够支持每秒数十万次的读写操作24。这使得Redis成为处理高并发请求的理想选择，尤其是在需要快速响应的场景中，如缓存、会话管理、排行榜等。

* **丰富的数据类型**：Redis 不仅支持基本的键值存储，还提供了丰富的数据类型，包括字符串、列表、集合、哈希表、有序集合等。这些数据类型为开发者提供了灵活的数据操作能力，使得Redis可以适应各种不同的应用场景。

* **原子性操作**：Redis 的所有操作都是原子性的，这意味着操作要么完全执行，要么完全不执行。这种特性对于确保数据的一致性和完整性至关重要，尤其是在高并发环境下处理事务时。

* **持久化**：Redis 支持数据的持久化，可以将内存中的数据保存到磁盘中，以便在系统重启后恢复数据。这为 Redis 提供了数据安全性，确保数据不会因为系统故障而丢失。

* **支持发布/订阅模式**：Redis 内置了发布/订阅模式（Pub/Sub），允许客户端之间通过消息传递进行通信。这使得 Redis 可以作为消息队列和实时数据传输的平台。

* **单线程模型**：尽管 Redis 是单线程的，但它通过高效的事件驱动模型来处理并发请求，确保了高性能和低延迟。单线程模型也简化了并发控制的复杂性。

* **主从复制**：Redis 支持主从复制，可以通过从节点来备份数据或分担读请求，提高数据的可用性和系统的伸缩性。

* **应用场景广泛**：Redis 被广泛应用于各种场景，包括但不限于缓存系统、会话存储、排行榜、实时分析、地理空间数据索引等。

* **社区支持**：Redis 拥有一个活跃的开发者社区，提供了大量的文档、教程和第三方库，这为开发者提供了强大的支持和丰富的资源。

* **跨平台兼容性**：Redis 可以在多种操作系统上运行，包括 Linux、macOS 和 Windows，这使得它能够在不同的技术栈中灵活部署。

### Redis 与其他 key-value 存储有什么不同？

Redis 与其他 key-value 存储系统的主要区别在于其提供了丰富的数据类型、高性能的读写能力、原子性操作、持久化机制、以及丰富的特性集。

以下是 Redis 的一些独特之处：

* **丰富的数据类型**：Redis 不仅仅支持简单的 key-value 类型的数据，还提供了 list、set、zset（有序集合）、hash 等数据结构的存储。这些数据类型可以更好地满足特定的业务需求，使得 Redis 可以用于更广泛的应用场景。

* **高性能的读写能力**：Redis 能读的速度是 110000次/s，写的速度是 81000次/s。这种高性能主要得益于 Redis 将数据存储在内存中，从而显著提高了数据的访问速度。

* **原子性操作**：Redis 的所有操作都是原子性的，这意味着操作要么完全执行，要么完全不执行。这种特性对于确保数据的一致性和完整性非常重要。

* **持久化机制**：Redis 支持数据的持久化，可以将内存中的数据保存在磁盘中，以便在系统重启后能够再次加载使用。这为 Redis 提供了数据安全性，确保数据不会因为系统故障而丢失。

* **丰富的特性集**：Redis 还支持 publish/subscribe（发布/订阅）模式、通知、key 过期等高级特性。这些特性使得 Redis 可以用于消息队列、实时数据分析等复杂的应用场景。

* **主从复制和高可用性**：Redis 支持 master-slave 模式的数据备份，提供了数据的备份和主从复制功能，增强了数据的可用性和容错性。

* **支持 Lua 脚本**：Redis 支持使用 Lua 脚本来编写复杂的操作，这些脚本可以在服务器端执行，提供了更多的灵活性和强大的功能。

* **单线程模型**：尽管 Redis 是单线程的，但它通过高效的事件驱动模型来处理并发请求，确保了高性能和低延迟。
## Redis安装
### Windows 下安装

下载地址：https://github.com/redis-windows/redis-windows/releases。

Redis 支持 32 位和 64 位。这个需要根据你系统平台的实际情况选择，这里我们下载 Redis-x64-xxx.zip压缩包到 C 盘，解压后，将文件夹重新命名为 redis。
![](https://www.runoob.com/wp-content/uploads/2014/11/3B8D633F-14CE-42E3-B174-FCCD48B11FF3.jpg)

打开文件夹，内容如下：
![](https://www.runoob.com/wp-content/uploads/2014/11/C2CEBAA0-30B9-4340-8D23-78F6FEB8CBE2.png%22)

打开一个 cmd 窗口 使用 cd 命令切换目录到 C:\redis 运行：
```shell
redis-server.exe redis.windows.conf
```
如果想方便的话，可以把 redis 的路径加到系统的环境变量里，这样就省得再输路径了，后面的那个 redis.windows.conf 可以省略，如果省略，会启用默认的。输入之后，会显示如下界面：
![](https://www.runoob.com/wp-content/uploads/2014/11/redis-install1.png)

这时候另启一个 cmd 窗口，原来的不要关闭，不然就无法访问服务端了。

切换到 redis 目录下运行:
```shell
redis-cli.exe -h 127.0.0.1 -p 6379
```
设置键值对:
```shell
set myKey abc
```
取出键值对:
```shell
get myKey
```
![](https://www.runoob.com/wp-content/uploads/2014/11/redis-install2.jpg)

## Redis配置
Redis 的配置文件位于 Redis 安装目录下，文件名为 redis.conf(Windows 名为 redis.windows.conf)。

你可以通过 CONFIG 命令查看或设置配置项。
语法

Redis CONFIG 命令格式如下：
```shell
redis 127.0.0.1:6379> CONFIG GET CONFIG_SETTING_NAME
```
**实例**
```shell
redis 127.0.0.1:6379> CONFIG GET loglevel

1) "loglevel"
2) "notice"
```
使用 * 号获取所有配置项：

**实例**
```shell
redis 127.0.0.1:6379> CONFIG GET *

  1) "dbfilename"
  2) "dump.rdb"
  3) "requirepass"
  4) ""
  5) "masterauth"
  6) ""
  7) "unixsocket"
  8) ""
  9) "logfile"
 10) ""
 11) "pidfile"
 12) "/var/run/redis.pid"
 13) "maxmemory"
 14) "0"
 15) "maxmemory-samples"
 16) "3"
 17) "timeout"
 18) "0"
 19) "tcp-keepalive"
 20) "0"
 21) "auto-aof-rewrite-percentage"
 22) "100"
 23) "auto-aof-rewrite-min-size"
 24) "67108864"
 25) "hash-max-ziplist-entries"
 26) "512"
 27) "hash-max-ziplist-value"
 28) "64"
 29) "list-max-ziplist-entries"
 30) "512"
 31) "list-max-ziplist-value"
 32) "64"
 33) "set-max-intset-entries"
 34) "512"
 35) "zset-max-ziplist-entries"
 36) "128"
 37) "zset-max-ziplist-value"
 38) "64"
 39) "hll-sparse-max-bytes"
 40) "3000"
 41) "lua-time-limit"
 42) "5000"
 43) "slowlog-log-slower-than"
 44) "10000"
 45) "latency-monitor-threshold"
 46) "0"
 47) "slowlog-max-len"
 48) "128"
 49) "port"
 50) "6379"
 51) "tcp-backlog"
 52) "511"
 53) "databases"
 54) "16"
 55) "repl-ping-slave-period"
 56) "10"
 57) "repl-timeout"
 58) "60"
 59) "repl-backlog-size"
 60) "1048576"
 61) "repl-backlog-ttl"
 62) "3600"
 63) "maxclients"
 64) "4064"
 65) "watchdog-period"
 66) "0"
 67) "slave-priority"
 68) "100"
 69) "min-slaves-to-write"
 70) "0"
 71) "min-slaves-max-lag"
 72) "10"
 73) "hz"
 74) "10"
 75) "no-appendfsync-on-rewrite"
 76) "no"
 77) "slave-serve-stale-data"
 78) "yes"
 79) "slave-read-only"
 80) "yes"
 81) "stop-writes-on-bgsave-error"
 82) "yes"
 83) "daemonize"
 84) "no"
 85) "rdbcompression"
 86) "yes"
 87) "rdbchecksum"
 88) "yes"
 89) "activerehashing"
 90) "yes"
 91) "repl-disable-tcp-nodelay"
 92) "no"
 93) "aof-rewrite-incremental-fsync"
 94) "yes"
 95) "appendonly"
 96) "no"
 97) "dir"
 98) "/home/deepak/Downloads/redis-2.8.13/src"
 99) "maxmemory-policy"
100) "volatile-lru"
101) "appendfsync"
102) "everysec"
103) "save"
104) "3600 1 300 100 60 10000"
105) "loglevel"
106) "notice"
107) "client-output-buffer-limit"
108) "normal 0 0 0 slave 268435456 67108864 60 pubsub 33554432 8388608 60"
109) "unixsocketperm"
110) "0"
111) "slaveof"
112) ""
113) "notify-keyspace-events"
114) ""
115) "bind"
116) ""
```
### 编辑配置

你可以通过修改 redis.conf 文件或使用 CONFIG set 命令来修改配置。
语法

CONFIG SET 命令基本语法：
```shell
redis 127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE
```
**实例**
```shell
redis 127.0.0.1:6379> CONFIG SET loglevel "notice"
OK
redis 127.0.0.1:6379> CONFIG GET loglevel

1) "loglevel"
2) "notice"
```
## Redis 数据类型

Redis 主要支持以下几种数据类型：
* string（字符串）: 基本的数据存储单元，可以存储字符串、整数或者浮点数。
* hash（哈希）:一个键值对集合，可以存储多个字段。
* list（列表）:一个简单的列表，可以存储一系列的字符串元素。
* set（集合）:一个无序集合，可以存储不重复的字符串元素。
* zset(sorted set：有序集合): 类似于集合，但是每个元素都有一个分数（score）与之关联。
* 位图（Bitmaps）：基于字符串类型，可以对每个位进行操作。
* 超日志（HyperLogLogs）：用于基数统计，可以估算集合中的唯一元素数量。
* 地理空间（Geospatial）：用于存储地理位置信息。
* 发布/订阅（Pub/Sub）：一种消息通信模式，允许客户端订阅消息通道，并接收发布到该通道的消息。
* 流（Streams）：用于消息队列和日志存储，支持消息的持久化和时间排序。
* 模块（Modules）：Redis 支持动态加载模块，可以扩展 Redis 的功能。

### String（字符串）

string 是 redis 最基本的类型，你可以理解成与 Memcached 一模一样的类型，一个 key 对应一个 value。

string 类型是二进制安全的。意思是 redis 的 string 可以包含任何数据，比如jpg图片或者序列化的对象。

string 类型是 Redis 最基本的数据类型，string 类型的值最大能存储 512MB。
**常用命令**
* SET key value：设置键的值。
* GET key：获取键的值。
* INCR key：将键的值加 1。
* DECR key：将键的值减 1。
* APPEND key value：将值追加到键的值之后。

**实例**
```shell
redis 127.0.0.1:6379> SET runoob "菜鸟教程"
OK
redis 127.0.0.1:6379> GET runoob
"菜鸟教程"
```
在以上实例中我们使用了 Redis 的 SET 和 GET 命令。键为 runoob，对应的值为 菜鸟教程。

注意：一个键最大能存储 512MB。

### Hash（哈希）

Redis hash 是一个键值(key=>value)对集合，类似于一个小型的 NoSQL 数据库。

Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象。

每个哈希最多可以存储 2^32 - 1 个键值对。

#### 常用命令
* HSET key field value：设置哈希表中字段的值。
* HGET key field：获取哈希表中字段的值。
* HGETALL key：获取哈希表中所有字段和值。
* HDEL key field：删除哈希表中的一个或多个字段。

**实例**

DEL runoob 用于删除前面测试用过的 key，不然会报错：(error) WRONGTYPE Operation against a key holding the wrong kind of value 

![](https://www.runoob.com/wp-content/uploads/2014/11/B104156B-7270-4D03-8EB3-B72D4022ED78.jpg)

```shell
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> HMSET runoob field1 "Hello" field2 "World"
"OK"
redis 127.0.0.1:6379> HGET runoob field1
"Hello"
redis 127.0.0.1:6379> HGET runoob field2
"World"
```
实例中我们使用了 Redis HMSET, HGET 命令，HMSET 设置了两个 field=>value 对, HGET 获取对应 field 对应的 value。
### List（列表）

Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）。

列表最多可以存储 2^32 - 1 个元素。
#### 常用命令
* LPUSH key value：将值插入到列表头部。
* RPUSH key value：将值插入到列表尾部。
* LPOP key：移出并获取列表的第一个元素。
* RPOP key：移出并获取列表的最后一个元素。
* LRANGE key start stop：获取列表在指定范围内的元素。

**实例**
```shell
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> lpush runoob redis
(integer) 1
redis 127.0.0.1:6379> lpush runoob mongodb
(integer) 2
redis 127.0.0.1:6379> lpush runoob rabbitmq
(integer) 3
redis 127.0.0.1:6379> lrange runoob 0 10
1) "rabbitmq"
2) "mongodb"
3) "redis"
redis 127.0.0.1:6379>
```
### Set（集合）

Redis 的 Set 是 string 类型的无序集合。

集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。
#### 常用命令
* SADD key value：向集合添加一个或多个成员。
* SREM key value：移除集合中的一个或多个成员。
* SMEMBERS key：返回集合中的所有成员。
* SISMEMBER key value：判断值是否是集合的成员。

sadd 命令

添加一个 string 元素到 key 对应的 set 集合中，成功返回 1，如果元素已经在集合中返回 0。

sadd key member

实例

redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> sadd runoob redis
(integer) 1
redis 127.0.0.1:6379> sadd runoob mongodb
(integer) 1
redis 127.0.0.1:6379> sadd runoob rabbitmq
(integer) 1
redis 127.0.0.1:6379> sadd runoob rabbitmq
(integer) 0
redis 127.0.0.1:6379> smembers runoob

1) "redis"
2) "rabbitmq"
3) "mongodb"

注意：以上实例中 rabbitmq 添加了两次，但根据集合内元素的唯一性，第二次插入的元素将被忽略。

集合中最大的成员数为 232 - 1(4294967295, 每个集合可存储40多亿个成员)。

### zset(sorted set：有序集合)
Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。

不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。

zset的成员是唯一的,但分数(score)却可以重复。
#### 常用命令

* ZADD key score value：向有序集合添加一个或多个成员，或更新已存在成员的分数。
* ZRANGE key start stop [WITHSCORES]：返回指定范围内的成员。
* ZREM key value：移除有序集合中的一个或多个成员。
* ZSCORE key value：返回有序集合中，成员的分数值。

#### zadd 命令

添加元素到集合，元素在集合中存在则更新对应score
```shell
zadd key score member 
```
**实例**
```shell
redis 127.0.0.1:6379> DEL runoob
redis 127.0.0.1:6379> zadd runoob 0 redis
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 mongodb
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 rabbitmq
(integer) 1
redis 127.0.0.1:6379> zadd runoob 0 rabbitmq
(integer) 0
redis 127.0.0.1:6379> ZRANGEBYSCORE runoob 0 1000
1) "mongodb"
2) "rabbitmq"
3) "redis"
```
## Redis 命令

Redis 命令用于在 redis 服务上执行操作。

要在 redis 服务上执行命令需要一个 redis 客户端。Redis 客户端在我们之前下载的的 redis 的安装包中。

**语法**

Redis 客户端的基本语法为：
```shell
$ redis-cli
```
**实例**

以下实例讲解了如何启动 redis 客户端：

启动 redis 服务器，打开终端并输入命令 redis-cli，该命令会连接本地的 redis 服务。
```shell
$ redis-cli
redis 127.0.0.1:6379>
redis 127.0.0.1:6379> PING

PONG
```
在以上实例中我们连接到本地的 redis 服务并执行 PING 命令，该命令用于检测 redis 服务是否启动。
### 在远程服务上执行命令

如果需要在远程 redis 服务上执行命令，同样我们使用的也是 redis-cli 命令。
**语法**
```shell
$ redis-cli -h host -p port -a password
```
**实例**

以下实例演示了如何连接到主机为 127.0.0.1，端口为 6379 ，密码为 mypass 的 redis 服务上。
```shell
$redis-cli -h 127.0.0.1 -p 6379 -a "mypass"
redis 127.0.0.1:6379>
redis 127.0.0.1:6379> PING

PONG
```
## Redis 键(key)

Redis 键命令用于管理 redis 的键。
**语法**

Redis 键命令的基本语法如下：
```shell
redis 127.0.0.1:6379> COMMAND KEY_NAME
```
**实例**
```shell
redis 127.0.0.1:6379> SET runoobkey redis
OK
redis 127.0.0.1:6379> DEL runoobkey
(integer) 1
```
在以上实例中 DEL 是一个命令， runoobkey 是一个键。 如果键被删除成功，命令执行后输出 (integer) 1，否则将输出 (integer) 0
#### Redis keys 命令

下表给出了与 Redis 键相关的基本命令：
序号|命令及描述
--|--
1|DEL key 该命令用于在 key 存在时删除 key。
2|DUMP key 序列化给定 key ，并返回被序列化的值。
3|EXISTS key 检查给定 key 是否存在。
4|EXPIRE key seconds 为给定 key 设置过期时间，以秒计。
5|EXPIREAT key timestamp EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。
6|PEXPIRE key milliseconds 设置 key 的过期时间以毫秒计。
7|PEXPIREAT key milliseconds-timestamp 设置 key 过期时间的时间戳(unix timestamp) 以毫秒计
8|KEYS pattern 查找所有符合给定模式( pattern)的 key 。
9|MOVE key db 将当前数据库的 key 移动到给定的数据库 db 当中。
10|PERSIST key 移除 key 的过期时间，key 将持久保持。
11|PTTL key 以毫秒为单位返回 key 的剩余的过期时间。
12|TTL key 以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。
13|RANDOMKEY 从当前数据库中随机返回一个 key 。
14|RENAME key newkey 修改 key 的名称
15|RENAMENX key newkey 仅当 newkey 不存在时，将 key 改名为 newkey 。
16|SCAN cursor [MATCH pattern] [COUNT count] 迭代数据库中的数据库键。
17|TYPE key 返回 key 所储存的值的类型。
## Redis 字符串(String)

Redis 字符串数据类型的相关命令用于管理 redis 字符串值，基本语法如下：
**语法**
```shell
redis 127.0.0.1:6379> COMMAND KEY_NAME
```
**实例**
```shell
redis 127.0.0.1:6379> SET runoobkey redis
OK
redis 127.0.0.1:6379> GET runoobkey
"redis"
```
在以上实例中我们使用了 SET 和 GET 命令，键为 runoobkey。 

### Redis 字符串命令

下表列出了常用的 redis 字符串命令：
序号|命令及描述
--|--
1|SET key value 设置指定 key 的值。
2|GET key 获取指定 key 的值。
3|GETRANGE key start end返回 key 中字符串值的子字符
4|GETSET key value 将给定 key 的值设为 value ，并返回 key 的旧值(old value)。
5|GETBIT key offset 对 key 所储存的字符串值，获取指定偏移量上的位(bit)。
6|MGET key1 [key2..] 获取所有(一个或多个)给定 key 的值。
7|SETBIT key offset value 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)。
8|SETEX key seconds value 将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。
9|SETNX key value 只有在 key 不存在时设置 key 的值。
10|SETRANGE key offset value 用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。
11|STRLEN key 返回 key 所储存的字符串值的长度。
12|	MSET key value [key value ...] 同时设置一个或多个 key-value 对。
13|	MSETNX key value [key value ...] 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。
14|	PSETEX key milliseconds value 这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位。
15|	INCR key 将 key 中储存的数字值增一。
16|	INCRBY key increment 将 key 所储存的值加上给定的增量值（increment） 。
17|	INCRBYFLOAT key increment 将 key 所储存的值加上给定的浮点增量值（increment） 。
18|	DECR key 将 key 中储存的数字值减一。
19|	DECRBY key decrement key 所储存的值减去给定的减量值（decrement） 。
20|	APPEND key value 如果 key 已经存在并且是一个字符串， APPEND 命令将指定的 value 追加到该 key 原来值（value）的末尾。 
## Redis 哈希(Hash)

Redis hash 是一个 string 类型的 field（字段） 和 value（值） 的映射表，hash 特别适合用于存储对象。

Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）。
**实例**
```shell
127.0.0.1:6379>  HMSET runoobkey name "redis tutorial" description "redis basic commands for caching" likes 20 visitors 23000
OK
127.0.0.1:6379>  HGETALL runoobkey
1) "name"
2) "redis tutorial"
3) "description"
4) "redis basic commands for caching"
5) "likes"
6) "20"
7) "visitors"
8) "23000"
```
在以上实例中，我们设置了 redis 的一些描述信息(name, description, likes, visitors) 到哈希表的 runoobkey 中。

### Redis hash 命令

下表列出了 redis hash 基本的相关命令：
序号|命令及描述
--|--
1|HDEL key field1 [field2] 删除一个或多个哈希表字段
2|HEXISTS key field 查看哈希表 key 中，指定的字段是否存在。
3|HGET key field 获取存储在哈希表中指定字段的值。
4|HGETALL key 获取在哈希表中指定 key 的所有字段和值
5|HINCRBY key field increment 为哈希表 key 中的指定字段的整数值加上增量 increment 。
6|HINCRBYFLOAT key field increment 为哈希表 key 中的指定字段的浮点数值加上增量 increment 。
7|HKEYS key 获取哈希表中的所有字段
8|HLEN key 获取哈希表中字段的数量
9|HMGET key field1 [field2] 获取所有给定字段的值
10	|HMSET key field1 value1 [field2 value2 ] 同时将多个 field-value (域-值)对设置到哈希表 key 中。
11	|HSET key field value 将哈希表 key 中的字段 field 的值设为 value 。
12	|HSETNX key field value 只有在字段 field 不存在时，设置哈希表字段的值。
13	|HVALS key 获取哈希表中所有值。
14	|HSCAN key cursor [MATCH pattern] [COUNT count] 迭代哈希表中的键值对。
## Redis 列表(List)

Redis列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）

一个列表最多可以包含 232 - 1 个元素 (4294967295, 每个列表超过40亿个元素)。
**实例**
```shell
redis 127.0.0.1:6379> LPUSH runoobkey redis
(integer) 1
redis 127.0.0.1:6379> LPUSH runoobkey mongodb
(integer) 2
redis 127.0.0.1:6379> LPUSH runoobkey mysql
(integer) 3
redis 127.0.0.1:6379> LRANGE runoobkey 0 10

1) "mysql"
2) "mongodb"
3) "redis"
```
在以上实例中我们使用了 LPUSH 将三个值插入了名为 runoobkey 的列表当中。

### Redis 列表命令

下表列出了列表相关的基本命令：
序号|命令及描述
--|--
1|BLPOP key1 [key2 ] timeout 移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
2|BRPOP key1 [key2 ] timeou 移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
3|BRPOPLPUSH source destination timeout 从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
4|LINDEX key index 通过索引获取列表中的元素
5|LINSERT key BEFORE|AFTER pivot value 在列表的元素前或者后插入元素
6|LLEN key 获取列表长度
7|LPOP key 移出并获取列表的第一个元素
8|LPUSH key value1 [value2] 将一个或多个值插入到列表头部
9|LPUSHX key value 将一个值插入到已存在的列表头部
10|LRANGE key start stop 获取列表指定范围内的元素
11|LREM key count value 移除列表元素
12|LSET key index value 通过索引设置列表元素的值
13|LTRIM key start stop 对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。
14|RPOP key 移除列表的最后一个元素，返回值为移除的元素。
15|RPOPLPUSH source destination 移除列表的最后一个元素，并将该元素添加到另一个列表并返回
16|RPUSH key value1 [value2] 在列表中添加一个或多个值到列表尾部
17|RPUSHX key value 为已存在的列表添加值

## Redis 集合(Set)

Redis 的 Set 是 String 类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。

集合对象的编码可以是 intset 或者 hashtable。

Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。

集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。
**实例**
```shell
redis 127.0.0.1:6379> SADD runoobkey redis
(integer) 1
redis 127.0.0.1:6379> SADD runoobkey mongodb
(integer) 1
redis 127.0.0.1:6379> SADD runoobkey mysql
(integer) 1
redis 127.0.0.1:6379> SADD runoobkey mysql
(integer) 0
redis 127.0.0.1:6379> SMEMBERS runoobkey

1) "mysql"
2) "mongodb"
3) "redis"
```
在以上实例中我们通过 SADD 命令向名为 runoobkey 的集合插入的三个元素。

### Redis 集合命令

下表列出了 Redis 集合基本命令：
序号|命令及描述
--|--
1|SADD key member1 [member2] 向集合添加一个或多个成员
2|SCARD key 获取集合的成员数
3|SDIFF key1 [key2] 返回第一个集合与其他集合之间的差异。
4|SDIFFSTORE destination key1 [key2] 返回给定所有集合的差集并存储在 destination 中
5|SINTER key1 [key2] 返回给定所有集合的交集
6|SINTERSTORE destination key1 [key2] 返回给定所有集合的交集并存储在 destination 中
7|SISMEMBER key member 判断 member 元素是否是集合 key 的成员
8|SMEMBERS key 返回集合中的所有成员
9|SMOVE source destination member 将 member 元素从 source 集合移动到 destination 集合
10|SPOP key 移除并返回集合中的一个随机元素
11|SRANDMEMBER key [count] 返回集合中一个或多个随机数
12|SREM key member1 [member2] 移除集合中一个或多个成员
13|SUNION key1 [key2] 返回所有给定集合的并集
14|SUNIONSTORE destination key1 [key2] 所有给定集合的并集存储在 destination 集合中
15|SSCAN key cursor [MATCH pattern] [COUNT count] 迭代集合中的元素
## Redis 有序集合(sorted set)

Redis 有序集合和集合一样也是 string 类型元素的集合,且不允许重复的成员。

不同的是每个元素都会关联一个 double 类型的分数。redis 正是通过分数来为集合中的成员进行从小到大的排序。

有序集合的成员是唯一的,但分数(score)却可以重复。

集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。 集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。
**实例**
```shell
redis 127.0.0.1:6379> ZADD runoobkey 1 redis
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 2 mongodb
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
(integer) 1
redis 127.0.0.1:6379> ZADD runoobkey 3 mysql
(integer) 0
redis 127.0.0.1:6379> ZADD runoobkey 4 mysql
(integer) 0
redis 127.0.0.1:6379> ZRANGE runoobkey 0 10 WITHSCORES

1) "redis"
2) "1"
3) "mongodb"
4) "2"
5) "mysql"
6) "4"
```
在以上实例中我们通过命令 ZADD 向 redis 的有序集合中添加了三个值并关联上分数。
### Redis 有序集合命令

下表列出了 redis 有序集合的基本命令:
序号|命令及描述
--|--
1|ZADD key score1 member1 [score2 member2] 向有序集合添加一个或多个成员，或者更新已存在成员的分数
2|ZCARD key 获取有序集合的成员数
3|ZCOUNT key min max 计算在有序集合中指定区间分数的成员数
4|ZINCRBY key increment member 有序集合中对指定成员的分数加上增量 increment
5|ZINTERSTORE destination numkeys key [key ...] 计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 destination 中
6|ZLEXCOUNT key min max 在有序集合中计算指定字典区间内成员数量
7|ZRANGE key start stop [WITHSCORES] 通过索引区间返回有序集合指定区间内的成员
8|ZRANGEBYLEX key min max [LIMIT offset count] 通过字典区间返回有序集合的成员
9|ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT] 通过分数返回有序集合指定区间内的成员
10|ZRANK key member 返回有序集合中指定成员的索引
11|ZREM key member [member ...]移除有序集合中的一个或多个成员
12|ZREMRANGEBYLEX key min max 移除有序集合中给定的字典区间的所有成员
13|ZREMRANGEBYRANK key start stop 移除有序集合中给定的排名区间的所有成员
14|ZREMRANGEBYSCORE key min max 移除有序集合中给定的分数区间的所有成员
15|ZREVRANGE key start stop [WITHSCORES] 返回有序集中指定区间内的成员，通过索引，分数从高到低
16|ZREVRANGEBYSCORE key max min [WITHSCORES]返回有序集中指定分数区间内的成员，分数从高到低排序
17|ZREVRANK key member 返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序
18|ZSCORE key member 返回有序集中，成员的分数值
19|ZUNIONSTORE destination numkeys key [key ...] 计算给定的一个或多个有序集的并集，并存储在新的 key 中
20|ZSCAN key cursor [MATCH pattern] [COUNT count] 迭代有序集合中的元素（包括元素成员和元素分值）
## Redis HyperLogLog

Redis 在 2.8.9 版本添加了 HyperLogLog 结构。

Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定 的、并且是很小的。

在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。
### 什么是基数?

比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素的个数)为5。 基数估计就是在误差可接受的范围内，快速计算基数。
**实例**

以下实例演示了 HyperLogLog 的工作过程：
```shell
redis 127.0.0.1:6379> PFADD runoobkey "redis"

1) (integer) 1

redis 127.0.0.1:6379> PFADD runoobkey "mongodb"

1) (integer) 1

redis 127.0.0.1:6379> PFADD runoobkey "mysql"

1) (integer) 1

redis 127.0.0.1:6379> PFCOUNT runoobkey

(integer) 3
```
### Redis HyperLogLog 命令

下表列出了 redis HyperLogLog 的基本命令：
序号|命令及描述
--|--
1|PFADD key element [element ...] 添加指定元素到 HyperLogLog 中。
2|PFCOUNT key [key ...] 返回给定 HyperLogLog 的基数估算值。
3|PFMERGE destkey sourcekey [sourcekey ...] 将多个 HyperLogLog 合并为一个 HyperLogLog
## Redis 发布订阅

Redis 发布订阅 (pub/sub) 是一种消息通信模式：发送者 (pub) 发送消息，订阅者 (sub) 接收消息。

Redis 客户端可以订阅任意数量的频道。

下图展示了频道 channel1 ， 以及订阅这个频道的三个客户端 —— client2 、 client5 和 client1 之间的关系：
![](https://www.runoob.com/wp-content/uploads/2014/11/pubsub1.png)  
当有新消息通过 PUBLISH 命令发送给频道 channel1 时， 这个消息就会被发送给订阅它的三个客户端：
![](https://www.runoob.com/wp-content/uploads/2014/11/pubsub2.png)

**实例**

以下实例演示了发布订阅是如何工作的，需要开启两个 redis-cli 客户端。

在我们实例中我们创建了订阅频道名为 runoobChat:

第一个 redis-cli 客户端
```shell
redis 127.0.0.1:6379> SUBSCRIBE runoobChat

Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "runoobChat"
3) (integer) 1
```
现在，我们先重新开启个 redis 客户端，然后在同一个频道 runoobChat 发布两次消息，订阅者就能接收到消息。

第二个 redis-cli 客户端
```shell
redis 127.0.0.1:6379> PUBLISH runoobChat "Redis PUBLISH test"

(integer) 1

redis 127.0.0.1:6379> PUBLISH runoobChat "Learn redis by runoob.com"

(integer) 1

# 订阅者的客户端会显示如下消息
 1) "message"
2) "runoobChat"
3) "Redis PUBLISH test"
 1) "message"
2) "runoobChat"
3) "Learn redis by runoob.com"
```

### Redis 发布订阅命令

下表列出了 redis 发布订阅常用命令：
序号|命令及描述
--|--
1|PSUBSCRIBE pattern [pattern ...] 订阅一个或多个符合给定模式的频道。
2|PUBSUB subcommand [argument [argument ...]] 查看订阅与发布系统状态。
3|PUBLISH channel message 将信息发送到指定的频道。
4|PUNSUBSCRIBE [pattern [pattern ...]] 退订所有给定模式的频道。
5|SUBSCRIBE channel [channel ...]订阅给定的一个或多个频道的信息。
6|UNSUBSCRIBE [channel [channel ...]]
指退订给定的频道。
## Redis 事务
Redis 事务可以一次执行多个命令， 并且带有以下三个重要的保证：
* 批量操作在发送 EXEC 命令前被放入队列缓存。
* 收到 EXEC 命令后进入事务执行，事务中任意命令执行失败，其余的命令依然被执行。
* 在事务执行过程，其他客户端提交的命令请求不会插入到事务执行命令序列中。

一个事务从开始到执行会经历以下三个阶段：
* 开始事务。
* 命令入队。
* 执行事务。

**实例**

以下是一个事务的例子， 它先以 MULTI 开始一个事务， 然后将多个命令入队到事务中， 最后由 EXEC 命令触发事务， 一并执行事务中的所有命令：
```shell
redis 127.0.0.1:6379> MULTI
OK

redis 127.0.0.1:6379> SET book-name "Mastering C++ in 21 days"
QUEUED

redis 127.0.0.1:6379> GET book-name
QUEUED

redis 127.0.0.1:6379> SADD tag "C++" "Programming" "Mastering Series"
QUEUED

redis 127.0.0.1:6379> SMEMBERS tag
QUEUED

redis 127.0.0.1:6379> EXEC
1) OK
2) "Mastering C++ in 21 days"
3) (integer) 3
4) 1) "Mastering Series"
   2) "C++"
   3) "Programming"
```
***单个 Redis 命令的执行是原子性的，但 Redis 没有在事务上增加任何维持原子性的机制，所以 Redis 事务的执行并不是原子性的。***

事务可以理解为一个打包的批量执行脚本，但批量指令并非原子化的操作，中间某条指令的失败不会导致前面已做指令的回滚，也不会造成后续的指令不做。

比如：
```shell
redis 127.0.0.1:7000> multi
OK
redis 127.0.0.1:7000> set a aaa
QUEUED
redis 127.0.0.1:7000> set b bbb
QUEUED
redis 127.0.0.1:7000> set c ccc
QUEUED
redis 127.0.0.1:7000> exec
1) OK
2) OK
3) OK
```
如果在 set b bbb 处失败，set a 已成功不会回滚，set c 还会继续执行。
## Redis 脚本

Redis 脚本使用 Lua 解释器来执行脚本。 Redis 2.6 版本通过内嵌支持 Lua 环境。执行脚本的常用命令为 EVAL。
**语法**

Eval 命令的基本语法如下：
```shell
redis 127.0.0.1:6379> EVAL script numkeys key [key ...] arg [arg ...]
```
**实例**

以下实例演示了 redis 脚本工作过程：
```shell
redis 127.0.0.1:6379> EVAL "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second

1) "key1"
2) "key2"
3) "first"
4) "second"
```
### Redis 脚本命令

下表列出了 redis 脚本常用命令：
序号|命令及描述
--|--
1|EVAL script numkeys key [key ...] arg [arg ...]执行 Lua 脚本。
2|EVALSHA sha1 numkeys key [key ...] arg [arg ...]执行 Lua 脚本。
3|SCRIPT EXISTS script [script ...]查看指定的脚本是否已经被保存在缓存当中。
4|SCRIPT FLUSH从脚本缓存中移除所有脚本。
5|SCRIPT KILL杀死当前正在运行的 Lua 脚本。
6|SCRIPT LOAD script将脚本 script 添加到脚本缓存中，但并不立即执行这个脚本。

## Redis 连接

Redis 连接命令主要是用于连接 redis 服务。
实例

以下实例演示了客户端如何通过密码验证连接到 redis 服务，并检测服务是否在运行：
```shell
redis 127.0.0.1:6379> AUTH "password"
OK
redis 127.0.0.1:6379> PING
PONG
```
### Redis 连接命令

下表列出了 redis 连接的基本命令：
序号|命令及描述
--|--
1|AUTH password 验证密码是否正确
2|ECHO message 打印字符串
3|PING 查看服务是否运行
4|QUIT 关闭当前连接
5|SELECT index 切换到指定的数据库

## Redis 服务器

Redis 服务器命令主要是用于管理 redis 服务。
**实例**

以下实例演示了如何获取 redis 服务器的统计信息：
```shell
redis 127.0.0.1:6379> INFO

# Server
redis_version:2.8.13
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:c2238b38b1edb0e2
redis_mode:standalone
os:Linux 3.5.0-48-generic x86_64
arch_bits:64
multiplexing_api:epoll
gcc_version:4.7.2
process_id:3856
run_id:0e61abd297771de3fe812a3c21027732ac9f41fe
tcp_port:6379
uptime_in_seconds:11554
uptime_in_days:0
hz:10
lru_clock:16651447
config_file:

# Clients
connected_clients:1
client-longest_output_list:0
client-biggest_input_buf:0
blocked_clients:0

# Memory
used_memory:589016
used_memory_human:575.21K
used_memory_rss:2461696
used_memory_peak:667312
used_memory_peak_human:651.67K
used_memory_lua:33792
mem_fragmentation_ratio:4.18
mem_allocator:jemalloc-3.6.0

# Persistence
loading:0
rdb_changes_since_last_save:3
rdb_bgsave_in_progress:0
rdb_last_save_time:1409158561
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:0
rdb_current_bgsave_time_sec:-1
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok

# Stats
total_connections_received:24
total_commands_processed:294
instantaneous_ops_per_sec:0
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
evicted_keys:0
keyspace_hits:41
keyspace_misses:82
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:264

# Replication
role:master
connected_slaves:0
master_repl_offset:0
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:10.49
used_cpu_user:4.96
used_cpu_sys_children:0.00
used_cpu_user_children:0.01

# Keyspace
db0:keys=94,expires=1,avg_ttl=41638810
db1:keys=1,expires=0,avg_ttl=0
db3:keys=1,expires=0,avg_ttl=0
```