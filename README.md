# 中间件

整理了一些常用的中间件相关资料、笔记与操作手册

公网资料、笔记地址请访问这里 


<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
<!-- [![LinkedIn][linkedin-shield]][linkedin-url] -->

<!-- PROJECT LOGO -->

--------------------

## 什么是中间件

存在于两个系统之间的，起到连接的设备。
+ 为什么是设备？ 硬件和软件在一定程度上可以互用，中间件既可以是硬件，也可以是软件，所以我说是设备，而不定义为，硬件或者软件的一种。
+ 起到连接作用怎么理解？中间件可以在两个软件之间起到连接（iis服务）。可以在客户机/服务系统之间起到功能（例如web代理服务器）。

### 通信处理（消息）中间件
首先要修好马路，安装红绿灯，设立交通管理机构，制定出交通规则，也就是我们要建网和制定出通信协议，
能在不同平台之间通信，实现分布式系统中可靠的、高效的、实时的跨平台数据传输
(如TongLINK、BEA eLink 、IBM的MQSeries等)，称为消息中间件。这是中间件中唯一不可缺少的，是需求量最大的中间件产品
目前在Windows 2000操作系统中已包含了其部分功能

### 事务处理（交易）中间件
在分布式事务处理系统中要处理大量事务，常常在系统中要同时进行上万笔事务。
例如在北京市就要设置各种运载汽车，完成日常的运载，同时要随时监视汽车运行，
出现故障时，要有排除措施，发生堵塞时要进行调度。在联机事务处理系统(OLTP)中，
每笔事务常常要多台服务器上的程序顺序地协调完成，一旦中间发生某种故障时，不但要完成恢复工作
而且要自动切换系统，达到系统永不停机，实现高可靠性运行；
同时要使大量事务在多台应用服务器能实时并发运行，并进行负载平衡地调度，
实现昂贵的可靠性机和大型计算机系统同等的功能。
为了实现这个目标，要求系统具有监视和调度整个系统的功能。
BEA的 Tuxedo由此而著名，它成为增长率最高的厂商。一个事务处理平台，
根据X/OPEN的参数模型规定，应由事务处理中间件、
通信处理中间件以及数据存取管理中间件三部分组成。
东方通科技公司的TongLINK 和TongEASY实现了这个参考模型规定

### 数据存取管理中间件
在分布式系统中，重要的数据都集中存放在数据服务器中，它们可以是关系型的、复合文档型、
具有各种存放格式的多媒体型，或者是经过加密或压缩存放的，该中间件将为在网络上虚拟缓存、格式转换、解压等带来方便。

### Web服务器中间
浏览器图形用户界面已成为公认规范，然而它的会话能力差、不能作数据写入、
受HTTP协议的限制等，就必需进行修改和扩充，形成了 Web服务器中间件，
如 SilverStream公司的产品。

### 安全中间件
一些军事、政府和商务部门上网的最大障碍是安全保密问题，
而且不能使用国外提供的安全措施(如防火墙、加密、认证等)，必需用国产的产品。
产生不安全因素是由操作系统引起的，但必需要用中间件去解决，以适应灵活多变的要求。

### 跨平台和构架的中间件
当前开发大型应用软件通常采用基于构架和构件技术，在分布系统中，还需要集成各节点上的不同系统平台上的构件或新老版本的构件，
由此产生了构架中间件，功能最强的是CORBA，可以跨任意平台，但是太庞大；JavaBeans较灵活简单，很适合于做浏览器，
但运行效率差;DCOM模型主要适合 Windows平台，已广泛使用。实际上国内新建系统主要是UNIX(包括LINUX)和 Windows，
因此针对这两个平台建立相应的中间件要实用得多。

### 专用平台中间件
为特定应用领域设计参考模式，建立相应构架，配置相应的构件库和中间件，
为应用服务器开发和运行特定领域的关键任务(如电子商务、网站等)。

### 网络中间件
它包括网管、接入、网络测试、虚拟社区、虚拟缓冲等，也是当前最热门的研发项目。

--------------------

## 目录

[目录](index.md)

## Kafka

### 参考文档

[Kafka](Kafka/Kafka.md)

## Nginx

### 参考文档

[课堂笔记与拓展](Nginx/Nginx.md)

[KeepAlive案例](Nginx/KeepAlive.md)

[Nginx简介](Nginx/笔记/Nginx_01.md)

[服务器配置](Nginx/笔记/Nginx_02.md)

[Rewrite功能](Nginx/笔记/Nginx_03.md)

[负载均衡](Nginx/笔记/Nginx_04.md)

[集群搭建](Nginx/笔记/Nginx_05.md)

## RabbitMQ

### 参考文档

[目录](RabbitMQ/RabbitMQ.md)

[消息队列介绍](RabbitMQ/01.消息队列介绍.md)

[安装](RabbitMQ/02.RabbitMQ - 安装.md)

[简单案例](RabbitMQ/03.RabbitMQ - 简单案例.md)

[发布确认](RabbitMQ/04.RabbitMQ - 发布确认.md)

[交换机](RabbitMQ/05.RabbitMQ - 交换机.md)

[死信队列](RabbitMQ/06.RabbitMQ - 死信队列.md)

[延迟队列](RabbitMQ/07.RabbitMQ - 延迟队列.md)

[发布确认高级](RabbitMQ/08.RabbitMQ - 发布确认高级.md)

[幂等性、优先级、惰性](RabbitMQ/09.RabbitMQ - 幂等性、优先级、惰性.md)

## Redis

### 参考文档

[简要笔记](Redis/Redis.md)

[安装](Redis/详细笔记/redis-install.md)

[配置](Redis/详细笔记/redis-config.md)

[Redis5配置](Redis/详细笔记/redis5-config.md)

[安全设置](Redis/详细笔记/redis-safety.md)

[Lua接口实现](Redis/详细笔记/redis-lua.md)

## Tomcat

### 参考文档

[随堂笔记](Tomcat/Tomcat.md)

[详细笔记](Tomcat/笔记/Tomcat专题.md)

## Zookeeper

### 参考文档

[Zookeeper](ZooKeeper/ZooKeeper.md)

## ElasticSearch

### 参考文档

[学习笔记](ElasticSearch/ElasticSearch.md)

[课程笔记](ElasticSearch/课程笔记.md)


## 贡献者

请阅读**CONTRIBUTING.md** 查阅为该项目做出贡献的开发者。

#### 如何参与开源项目

贡献使开源社区成为一个学习、激励和创造的绝佳场所。你所作的任何贡献都是**非常感谢**的。


1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


## 版本控制

该项目使用Git进行版本管理。您可以在repository参看当前可用版本。

## 作者

[小昊子](https://github.com/worst001)

制做不易，如果有帮到你就请作者喝杯咖啡吧!

![支付宝加微信](https://xiyou-oss.oss-cn-shanghai.aliyuncs.com/%E5%85%AC%E4%BC%97%E5%8F%B7%E4%B8%8E%E6%94%AF%E4%BB%98/%E6%94%AF%E4%BB%98%E5%AE%9D%E5%8A%A0%E5%BE%AE%E4%BF%A1.jpg)

作者无聊时做的测试游戏，完全免费哦！

![公众号](https://xiyou-oss.oss-cn-shanghai.aliyuncs.com/%E5%85%AC%E4%BC%97%E5%8F%B7%E4%B8%8E%E6%94%AF%E4%BB%98/%E5%85%AC%E4%BC%97%E5%8F%B7%E5%B0%8F.jpg)


<!-- links -->
[your-project-path]:shaojintian/Best_README_template
[contributors-shield]: https://img.shields.io/github/contributors/worst001/mkdocs_middleware.svg?style=flat-square
[contributors-url]: https://github.com/worst001/mkdocs_middleware/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/worst001/mkdocs_middleware.svg?style=flat-square
[forks-url]: https://github.com/worst001/mkdocs_middleware/network/members
[stars-shield]: https://img.shields.io/github/stars/worst001/mkdocs_middleware.svg?style=flat-square
[stars-url]: https://github.com/worst001/mkdocs_middleware/stargazers
[issues-shield]: https://img.shields.io/github/issues/worst001/mkdocs_middleware.svg?style=flat-square
[issues-url]: https://img.shields.io/github/issues/worst001/mkdocs_middleware.svg
[license-shield]: https://img.shields.io/github/license/worst001/mkdocs_middleware.svg?style=flat-square
[license-url]: https://github.com/worst001/mkdocs_middleware/blob/main/LICENSE.txt
<!-- [linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555 -->
<!-- [linkedin-url]: https://linkedin.com/in/shaojintian -->
