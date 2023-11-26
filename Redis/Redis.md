# Redis

--------------------
## 参考资料
[尚硅谷_Redis6_课件](/Redis/尚硅谷_Redis6课件.pdf)

---

## 一、基础知识

### NoSql 分类
+ KV 键值对
    + Redis
    + MemoryCache
+ 文档类型
    + MongoDB
+ 列存储
    + Hadoop
    + Hive
+ 图
    + Neo4j

### CAS 的补充
弱一致性模型
先满足AP后最终规整时保持一致性

1. 基本可用(Basically Avaliable)
2. 软状态(Soft state)
3. 最终一致(Eventually consistent)

### 基础命令
`redis-benchmark`
查看当前服务器性能

### 客户端命令(常用)
SELECT   : 选择库
DBSIZE   : 查看 key 的数量
KEYS a?  : 查询a开头两位的key
    > 只过期不删除的数据疑似缓存击穿
#### 1. String 类型
+ SET GET DEL APPEND STRLEN SETNX
+ INCR DECR
+ GETRANGE SETRANGE
+ MSET MGET MSETNX
+ MSETNX   : 批量设置没有保存过的 key value
           (如果有一个不成功都不成功)

#### 2. List 类型
+ LPUSH RPUSH LRANGE LPOP RPOP
+ LINDEX LLEN LREM LTRIM
+ LREM    : 从左开始删除多个同样的值
+ LTRIM   : 从左开始截取子 List
+ RPOPLPUSH LSET LINSERT
+ LINSERT : 从左开始找到第一个匹配值插入

#### 3. Set 类型
+ SADD SMEMBERS SISMEMBER SCARD
+ SREM SRANDMEMBER SPOP SMOVE
+ SRANDMEMBER : 随机从里面出数 但是不删除
+ SPOP        : 随机从里面出数
+ SMOVE       : 从某个一个集合中出数到另一个集合
+ SDIFF SINTER SUNION

#### 4. Hash 类型
+ HSET HGET HMSET HGETALL HDEL
+ HLEN HEXISTS HKEY HVALS
+ HINCRBY HINCRBYFLOAT HSETNX

#### 5. Zset 类型
+ ZADD ZRANGE ZRANGEBYSCORE ZREMT
+ ZRANGEBYSCORE : 根据数字范围获取 可以通过 limit 截取
+ ZCARD ZCOUNT ZRANK ZSCORE
+ ZCOUNT        : 根据数字范围统计数量
+ ZRANK         : 获取下标
+ ZSCORE        : 获取数字

### 配置文件
+ `daemonize`: 守护线程
+ `tcp-backlog`:连接队列总和
    + 由于redis单线程的特性，连接和数据处理都在同一个线程里，慢查询会导致tcp连接超时，未连接队列中的连接会一直处于syn_RECV状态，新进连接会一直处于syn_SEND状态等待服务器的ACK应答
+ `bind`: 绑定IP
+ `tcp-keepalive`: 心跳机制
+ Memory Policy(缓存策略)
    + volatile-lru:最近不常用的移出
    + noeviction:永不过期

---
## 二、集群与持久化

### 1、RDB
+ fork 一个子进程对内存数据进行快照
+ 替换原来的RDB是覆盖操作 可能丢失数据
+ 一致性不高
+ 策略
    + 满足以上任意1个条件
```redis.conf
#       时间   改动条数
save    3600   1
save    300    100
save    60     10000
```
+ FLUSHALL、SHUTDOWN 会提交 commit 到 RDB
    + 容灾备份的 RDB 应该放到远程服务器并且增加点策略才行
+ stop-write-on-bgsave-error: 出错时是否停止备份

### 2、AOF
+ 类似binlog记录每一次操作
+ appendonly yes: 开启aof模式
+ redis-check-aof --fix:删除故障引起的错误的操作语法
+ appendfsync:多久同步一次
+ auto-aof-rewrite-min-size:多大的文件触发重写机制
    + 重写后会压缩冗余的命令

### 3、事务(Redis 的事务叫批处理更合适)
+ MULTI: 开始事务(操作都会进入队列)
+ EXEC: 提交事务
+ DISCARD: 放弃事务
+ 源头债主: 语法正确时会执行队列里的命令，事务结束后出错的地方需要单独处理。
    + Redis 事务没有保证原子性
    + 没有做到CAID
    + 语法错误时全部提交失败有原子性
+ WATCH: 对接下来的操作做CAS乐观锁
    + 高并发情况下优先采用CAS方案

### 4、主从复制
配从不配主(一律认为新的配置是从库 逻辑上更清晰)

#### 1. 主从关系
+ 主机 Down 后从机待命 主机重新连上后 从机恢复与主机连接
    + 虽然主机重连后从机会恢复 但没有主机的时间段无法进行写操作
    + 集群中缺少主机 从机视为待机

+ 从机 Down 后重新启动丢失从机身份 要重新配置
    + 重启后从机未配置过(假主机) 也可视为待机


#### 2. Sentinel 哨兵模式
+ 代理了人为配置主从
    + 假设将人为的配置行为看成一个类
    + Sentinel 的分配行为是代理模式
+ 何时重新分配通过观察主机状态实现
    + 核心的哨兵功能是观察者模式
    + 主机状态down后哨兵选出新主机
    + 最后将决定推送到剩余从机

### 5、使用JedisPool
+ maxActive:连接池中有多少个实例
+ maxIdle:离池子撑满的空闲实例数
    + 防止撑满后 Redis 挂掉
+ maxWait:建立单个连接实例时的最大等待时间
+ testOnBorrow:获得实例时是否检查连接可用性

### 6、重启守护进程
```bash
vim /etc/systemd/system/redis.service

[Service]
ExecStop=/bin/kill -s TERM $MAINPID
ExecStartPost=/bin/sh -c "echo $MAINPID > /var/run/redis/redis.pid"

sudo systemctl daemon-reload
sudo systemctl enable redis-server
sudo systemctl restart redis.service
```

---
## 三、配置集群
```bash
## 必须配置的项

# 端口
port 6380
# 开启守护进程模式(日志在后台打印)
daemonize yes
# 设置 pid 路径
pidfile /var/run/redis/redis-server6380.pid
# 设置日志打印路径
logfile /var/log/redis/redis-server6380.log
# rdb
dbfilename dump6380.rdb
# (看情况rdb 比如分片时可换成aof)
appendonly yes
appendfilename "appendonly6380.aof"
# 哨兵配置sentinel.conf
sentinel monitor mymaster 127.0.0.1 6380 1

## 分片集群
cluster-enabled yes
cluster-config-file nodes6380.conf
cluster-node-timeout 5000
appendonly yes

## bash
redis-server redis6380.conf # master
redis-server redis6381.conf # slave
redis-server redis6382.conf # slave
redis-sentinel sentinel.conf

# cluster 模式下配置slave
redis-cli --cluster create --cluster-replicas 1 localhost:7001 localhost:7002 localhost:7003 localhost:7004 localhost:7005 localhost:7006

## cli

# 主从信息 初始状态为主
INFO REPLICATION
# 设为目标机器 ip 的从库
SLAVEOF IP PORT
# 当前从库变成主库
SLAVEOF NO ONE
# 关闭服务(避免使用kill pid方式)
SHUTDOWN

```

---
## 四、缓存穿透与击穿
[穿透与击穿](https://blog.csdn.net/kongtiao5/article/details/82771694)

### 1. 穿透
+ 缓存和数据库中均没有数据，大量请求打到数据库。
+ 解决思路：
    + 空值也记为缓存
    + 布隆过滤器

### 2. 击穿
+ 缓存过期，大量请求突然打进来。
+ 解决思路:
    + 设置热点永不过期
    + 加乐观锁

### 3. 雪崩
+ 缓存中数据大批量到过期时间，而查询数据量巨大，引发宕机。
+ 穿透和击穿没做好会引发雪崩
+ 解决思路:
    + redis哨兵模式保证可靠性
    + 利用哈希环和redis分槽均匀分布数据
