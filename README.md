<a name="readme-top"></a>
<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
<!-- [![LinkedIn][linkedin-shield]][linkedin-url] -->

<!-- PROJECT LOGO -->

<!-- 项目LOGO -->
<br />
<div align="center">
  <!-- <a href="http://note.grft.top"> -->
  <!--   <img src="https://xiyou-oss.oss-cn-shanghai.aliyuncs.com/mkdocs/logo.png" alt="Logo" width="480" height="270"> -->
  <!-- </a> -->

  <h3 align="center">中间件</h3>

  <p align="center">
    <br />
    <a href="http://note.grft.top/中间件/"><strong>探索文档 »</strong></a>
    <br />
  </p>
</div>

<!-- 目录 -->
<details>
  <summary>目录</summary>
  <ol>
    <li><a href="#关于项目">关于项目</a></li>
    <li><a href="#什么是中间件">什么是中间件</a></li>
    <li><a href="#技术目录">技术目录</a></li>
    <li><a href="#贡献">贡献</a></li>
    <li><a href="#许可证">许可证</a></li>
    <li><a href="#联系方式">联系方式</a></li>
    <li><a href="#鸣谢">鸣谢</a></li>
  </ol>
</details>

## 关于项目

整理了一些常用的中间件相关资料、笔记与操作手册

公网资料、笔记地址请访问这里

- 文档地址: [http://note.grft.top/中间件/](http://note.grft.top/中间件/)

其他相关技术可以访问我的博客，主页地址请访问这里

- 访问入口：[http://note.grft.top](http://note.grft.top)

<p align="right">(<a href="#readme-top">回到顶部</a>)</p>

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

<p align="right">(<a href="#readme-top">回到顶部</a>)</p>

## 技术目录

[目录与大纲](index.md)

### Kafka

+ [笔记摘要](Kafka/Kafka.md)
+ [Kafka 简介](Kafka/notes/Kafka简介.md)
+ [基于 Zookeeper 搭建 Kafka 高可用集群](Kafka/notes/基于Zookeeper搭建Kafka高可用集群.md)
+ [Kafka 生产者详解](Kafka/notes/Kafka生产者详解.md)
+ [Kafka 消费者详解](Kafka/notes/Kafka消费者详解.md)
+ [深入理解 Kafka 副本机制](Kafka/notes/Kafka深入理解分区副本机制.md)

#### Kafka 课件资料
+ [Kafka（入门与概述）](Kafka/笔记/01_尚硅谷大数据技术之Kafka.pdf)
+ [Kafka（外部系统集成）](Kafka/笔记/02_尚硅谷大数据技术之Kafka（外部系统集成）V3.3.pdf)
+ [Kafka（生产调优手册）](Kafka/笔记/03_尚硅谷大数据技术之Kafka（生产调优手册）V3.3.pdf)
+ [Kafka（源码解析）](Kafka/笔记/04_尚硅谷大数据技术之Kafka（源码解析）V3.3.pdf)


### Nginx

+ [课堂笔记与拓展](Nginx/Nginx.md)
+ [KeepAlive案例](Nginx/KeepAlive.md)
+ [Nginx简介](Nginx/笔记/Nginx_01.md)
+ [服务器配置](Nginx/笔记/Nginx_02.md)
+ [Rewrite功能](Nginx/笔记/Nginx_03.md)
+ [负载均衡](Nginx/笔记/Nginx_04.md)
+ [集群搭建](Nginx/笔记/Nginx_05.md)
+ [Nginx 课件资料](Nginx/nginx课件v1.0.pdf)


### RabbitMQ

+ [目录](RabbitMQ/RabbitMQ.md)
+ [消息队列介绍](RabbitMQ/01.消息队列介绍.md)
+ [安装](RabbitMQ/02.RabbitMQ-安装.md)
+ [简单案例](RabbitMQ/03.RabbitMQ-简单案例.md)
+ [发布确认](RabbitMQ/04.RabbitMQ-发布确认.md)
+ [交换机](RabbitMQ/05.RabbitMQ-交换机.md)
+ [死信队列](RabbitMQ/06.RabbitMQ-死信队列.md)
+ [延迟队列](RabbitMQ/07.RabbitMQ-延迟队列.md)
+ [发布确认高级](RabbitMQ/08.RabbitMQ-发布确认高级.md)
+ [幂等性、优先级、惰性](RabbitMQ/09.RabbitMQ-幂等性、优先级、惰性.md)

### Redis

+ [简要笔记](Redis/Redis.md)
+ [安装](Redis/详细笔记/redis-install.md)
+ [配置](Redis/详细笔记/redis-config.md)
+ [Redis5配置](Redis/详细笔记/redis5-config.md)
+ [安全设置](Redis/详细笔记/redis-safety.md)
+ [Lua接口实现](Redis/详细笔记/redis-lua.md)
+ [Redis 课件资料](Redis/尚硅谷_Redis6课件.pdf)

### Tomcat

+ [入门摘要](Tomcat/Tomcat.md)
+ [详细笔记](Tomcat/笔记/Tomcat专题.md)

### Zookeeper

+ [Zookeeper 简介及核心概念](Zookeeper/notes/Zookeeper简介及核心概念.md)
+ [Zookeeper 单机环境和集群环境搭建](Zookeeper/notes/Zookeeper单机环境和集群环境搭建.md)
+ [Zookeeper 常用 Shell 命令](Zookeeper/notes/Zookeeper常用Shell命令.md)
+ [Zookeeper Java 客户端 —— Apache Curator](Zookeeper/notes/Zookeeper_Java客户端Curator.md)
+ [Zookeeper ACL 权限控制](Zookeeper/notes/Zookeeper_ACL权限控制.md)

#### Zookeeper 课件资料

+ [Zookeeper 入门](Zookeeper/笔记/08_尚硅谷技术之ZookeeperV3.3.pdf)
+ [Zookeeper 源码解析](Zookeeper/笔记/08_尚硅谷技术之Zookeeper（源码解析）V3.3.pdf)


### ElasticSearch

+ [课程笔记](ElasticSearch/课程笔记.md)
+ [ElasticSearch 课件资料](ElasticSearch/ELK课程教案.pdf)

<p align="right">(<a href="#readme-top">回到顶部</a>)</p>

<!-- 贡献 -->

## 贡献

贡献是使开源社区成为一个如此令人惊叹的地方，以学习、激励和创造。您所做的任何贡献都将非常感谢。

如果您对使这个项目变得更好有建议，请 fork 该仓库并创建 pull request。您也可以打开一个带有“enhancement”标签的问题。不要忘记给这个项目点个星！再次感谢！

<p align="right">(<a href="#readme-top">返回顶部</a>)</p>


<!-- 许可证 -->
## 许可证

根据 MIT 许可证进行分发。更多信息请参见 [LICENSE.txt](LICENSE)。

<p align="right">(<a href="#readme-top">返回顶部</a>)</p>

<!-- 联系方式 -->
## 联系方式

关注我: [小昊子](https://github.com/worst001)

博客地址: [http://note.grft.top](http://note.grft.top)

项目链接: [https://github.com/worst001/note_middleware](https://github.com/worst001/note_middleware)

<p align="right">(<a href="#readme-top">返回顶部</a>)</p>

## 鸣谢

因为仓库与文档的数量比较大，有些借鉴资料忘了在`参考文档`部分提及原作者与原仓库，若有疏漏请告诉，我及时补上。

所有引用的原资料都确认是开源认证，若有侵权请告知。

[尚硅谷系列教程资料](http://www.atguigu.com/opensource.shtml)

[https://github.com/Tinywan/lua-nginx-redis](https://github.com/Tinywan/lua-nginx-redis)

[https://www.kuangstudy.com/bbs/1354069127022583809](https://www.kuangstudy.com/bbs/1354069127022583809)

[https://github.com/heibaiying/BigData-Notes](https://github.com/heibaiying/BigData-Notes)

[https://openai.com/chatgpt](https://openai.com/chatgpt)


<p align="right">(<a href="#readme-top">返回顶部</a>)</p>

<!-- links -->
[your-project-path]:shaojintian/Best_README_template
[contributors-shield]: https://img.shields.io/github/contributors/worst001/note_middleware.svg?style=flat-square
[contributors-url]: https://github.com/worst001/note_middleware/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/worst001/note_middleware.svg?style=flat-square
[forks-url]: https://github.com/worst001/note_middleware/network/members
[stars-shield]: https://img.shields.io/github/stars/worst001/note_middleware.svg?style=flat-square
[stars-url]: https://github.com/worst001/note_middleware/stargazers
[issues-shield]: https://img.shields.io/github/issues/worst001/note_middleware.svg?style=flat-square
[issues-url]: https://img.shields.io/github/issues/worst001/note_middleware.svg
[license-shield]: https://img.shields.io/github/license/worst001/note_middleware.svg?style=flat-square
[license-url]: https://github.com/worst001/note_middleware/blob/main/LICENSE.txt
<!-- [linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555 -->
<!-- [linkedin-url]: https://linkedin.com/in/shaojintian -->
