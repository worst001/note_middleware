# ZooKeeper

-----------------------
## 参考资料

[尚硅谷_随堂笔记](/ZooKeeper/笔记/随堂笔记.pdf)

[尚硅谷_Zookeeper_01](/ZooKeeper/笔记/08_尚硅谷技术之ZookeeperV3.3.pdf)

[尚硅谷_Zookeeper_02](/ZooKeeper/笔记/08_尚硅谷技术之Zookeeper（源码解析）V3.3.pdf)

[Zookeeper M1](https://zhuanlan.zhihu.com/p/367159436)

---
## 一、结构理解

### 1、内存里的数据结构
`观察者模式` `常驻内存`

+ 树状数据
+ 每个节点(ZNode)拥有版本信息
+ 节点可以被监控
    + 一旦被修改会通知监控的客户端
    + 节点的所有子节点都会被通知

### 2、节点的分类
+ 持久节点(P)
+ 持久顺序节点(PS)
    + 每创建一个子节点时创建时序
+ 零时节点(E)
    + 基于Session的节点
    + Session结束时节点被释放
+ 零时顺序节点(ES)


---
## 二、配置

### 1、配置文件

+ `tickTime`
> 心跳间隔
+ `initLimit`
> 初始化集群时的心跳限制
+ `syncLimit`
> 同步数据时的心跳限制
+ `maxClientCnxns`
> 最大并发连接数
+ `autopurge.snapRetainCount`
> 限制多少个快照自动产生合并
+ `autopurge.purgeInterval`
> 自动合并的间隔(单位:小时)
> 大于上诉限制时就会合并

### 2、集群配置

1、在zkData目录下创建一个`myid`的文件：touch `myid`

2、在`myid`中添加对应的编号 ： 1

3、剩下的服务器按照上面的顺序搭， 不过另外两台服务器的myid内容为 2 、 3

4、进入`zoo.cfg`文件，修改dataDir路径，以及添加如下配置

```bash
server.1=第一台服务器的主机名:2888:3888
server.2=第二台服务器的主机名:2888:3888
server.3=第三台服务器的主机名:2888:3888
```

