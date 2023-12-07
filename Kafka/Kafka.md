# 随堂笔记

## 一、概述

### 1、定义
+ 传统定义
    + 分布式  发布订阅   消息队列
    + 发布订阅：分为多种类型 订阅者根据需求 选择性订阅
+ 最新定义
    + 流平台（存储、计算）

### 2、消息队列应用场景
+ 缓存消峰
+ 解耦
+ 异步通信

### 3、两种模式
+ 点对点
    + 一个生产者 一个消费者 一个`topic`  会删除数据  不多
+ 发布订阅
    + 多个生产者  消费者多个  而且相互独立  多个`topic` 不会删除数据

### 4、架构
+ 生产者
    + 100T数据
+ `broker`
    + `broker`  服务器 hadoop102 103 104
    + `topic` 主题  对数据分类
    + 分区
    + 可靠性  副本
    + `leader`  `follower`
    + 生产者和消费者 只针对`leader`操作
+ 消费者
    + 消费者和消费者相互独立
    + 消费者组 （某个分区 只能由一个消费者消费）
+ zookeeper
    + broker.ids 0 1 2
    + `leader`

---
## 二、入门
### 1、安装
+ broker.id  必须全局唯一
+ broker.id、log.dirs zk/kafka
+ 启动停止  先停止kafka  再停zk
+ 脚本
```bash
#!/bin/bash

case $1 in
"start")
    for i in hadoop102 hadoop103 hadoop104
    do
        ssh $i "绝对路径"
    done
;;
"stop")

;;
esac
```

### 2、常用命令行
+ 主题 kafka-topic.sh
    + --bootstrap-server  hadoop102:9092,hadoop103:9092
    + --topic first
    + --create
    + --delete
    + --alter
    + --list
    + --describe
    + --partitions
    + --replication-factor

+ 生产者 kafka-console-producer.sh
    + --bootstrap-server  hadoop102:9092,hadoop103:9092
    + --topic first


+ 消费者 kafka-console-consumer.sh
    + --bootstrap-server  hadoop102:9092,hadoop103:9092
    + --topic first

--- 
## 生产者
### 1、原理

### 2、异步发送API
+ 配置
    + 连接  bootstrap-server
    + key value序列化
+ 创建生产者
    + KafkaProducer<String,String>()
+ 发送数据
    + `send`() send(,new Callback)
+ 关闭资源

### 3、同步发送
+ send() send(,new Callback).get()

### 4、分区
+ 好处
    + 存储
    + 计算
+ 默认分区规则
    + 指定分区 按分区走
    + `key`  key的`hashcode`值%分区数
    + 没有指定key  没有指定分区   粘性
    + 第一随机
+ 自定义分区
    + 定义类 实现`partitioner`接口

### 5、吞吐量提高
+ 批次大小  16k  32k
+ linger.ms  0  => 5-100ms
+ 压缩
+ 缓存大小  32m  => 64m

### 6、可靠性
+ `acks`
+ 0  丢失数据
+ 1   也可能会丢  传输普通日志
+ -1  完全可靠  + 副本大于等于2  isr >=2    => 数据重复

### 7、数据重复
+ 幂等性
    + <pid, 分区号，序列号>
    + 默认打开
+ 事务
    + 底层基于幂等性
    + 初始化
    + 启动
    + 消费者offset
    + 提交
    + 终止

### 8、数据有序
+ 单分区内有序（有条件）
+ 多分区有序怎么办？

### 9、乱序
+ inflight  =1
+ 没有幂等性 inflight  =1
+ 有幂等性

---
## 三、内部机制

### 1、broker

#### 1. zk存储了哪些信息
+ broker.ids
+ `leader`
+ 辅助选举  controller

#### 2. 工作流程

#### 3. 服役
+ 准备一台干净服务器 hadoop100
+ 对哪个主题操作
+ 形成计划
+ 执行计划
+ 验证计划

#### 4. 退役
+ 要退役的节点不让存储数据
+ 退出节点

#### 5. 副本
+ 副本的好处   提高可靠性
+ 生产环境中通常2个  默认1个
+ 有`leader` `follower`
+ isr
+ controller  isr[0  2 3 ] 存活  ar [0  1 2 3]
+ Leader 挂了
+ `follower` 挂了
+ 副本分配 默认
+ 手动副本分配  制定计划  执行计划   验证计划
+ `leader` `partition`的负载均衡  10%
+ 手动增加副本因子

#### 6. 存储机制
+ `broker`  `topic`  `partition` log segment 1g   稀疏索引  4kb

#### 7. 删除数据
+ 默认7天   3天  7小时
+ 两种  删除  压缩
+ 删除：
+ 压缩：

#### 8. 高效读写
+ 集群  采用分区
+ 稀疏索引
+ 顺序读写
+ 零拷贝 和页缓存

### 2、消费者
#### 1. 总体流程
#### 2. 消费者组
#### 3. 按照主题消费
+ 配置信息
    + 连接
    + 反序列化
    + 组id
+ 创建消费者
+ 订阅主题
+ 消费数据

#### 4. 按照分区
#### 5. 消费者组案例
+ 组id
#### 6. 分区分配策略  再平衡
+ 7个分区  3个消费者
+ range
    ```txt
    0  1 2 x
    3 4
    5 6
    ```
+ roundrobin
	+ 轮询
        ```txt
        0  3  6
        1  4
        2  5
        ```
	+ 粘性  2 2 3
        ```txt
        0  3 4
        2  6
        1 5
        ```
#### 7. offset
+ 默认存储在系统主题
+ 自动提交  5s   默认
+ 手动提交  同步  异步
+ 指定offset消费  seek ()
+ 按照时间消费
+ 漏消费  重复消费

#### 8. 事务
+ 生产端  =》 集群
+ 集群 =》 消费者
+ 消费者 =》 框架

#### 9. 数据积压
+ 增加分区 增加消费者个数
+ 生产  =》 集群  4个参数
+ 消费端  两个参数  50m   500条

---
## 四、调优与测试

### 生产调优
1. 硬件选择
>
    100万日活 * 没人每天产生日志100条  =  1亿条 （中型公司）
    处理日志速度  1亿条 / (24 * 3600s ) = 1150条/s
    1条日志 （0.5k - 2k 1k）
    1150条 * 1k /s  =  1m/s
    高峰值 （中午小高峰 8 -12 ）： 1m/s  * 20倍 =  20m/s  -40m/s

2. 购买多少台服务器
>
    服务器台数= 2 * （生产者峰值生产速率 * 副本数 / 100） + 1
               =  2  * （20m/s * 2 /100） + 1
               = 3 台

3. 磁盘选择
>
    kafka 按照顺序读写   机械硬盘和固态硬盘 顺序读写速度差不多
    1亿条  *  1k = 100g
    100g * 2个副本 * 3天 / 0.7 = 1t
    建议三台服务器总的磁盘大小  大于1t

4. 内存选择
>
    kafka  内存 = 堆内存（kafka 内部配置） + 页缓存（服务器内存）
    1）堆内存 10 -15g
    2）页缓存  segment (1g )  （分区数Leader（10） * 1g * 25%）/ 3 = 1g
    一台服务器 10g + 1g

5. CPU选择
>
    32cpu
6. 网络选择

### 测试
```txt
1、batch.size=16384 linger.ms=0      9.76 MB/sec
2、batch.size=32768 linger.ms=0     9.76 MB/sec
3、batch.size=4096 linger.ms=0      3.81 MB/sec
4、batch.size=4096 linger.ms=50	  3.83 MB/sec
5、batch.size=4096 linger.ms=50 compression.type=snappy   3.77 MB/sec
6、batch.size=4096 linger.ms=50 compression.type=zstd     5.68 MB/sec
7、batch.size=4096 linger.ms=50 compression.type=gzip      5.90 MB/sec
8、batch.size=4096 linger.ms=50 compression.type=lz4       3.72 MB/sec
9、batch.size=4096 linger.ms=50 buffer.memory=67108864   3.76 MB/sec

消费者  一次处理500条   81.2066m/s
消费者  一次处理2000条  138.0992m/s
消费者  一次处理2000条  fetch.max.bytes=104857600   145.2033m/s

```


