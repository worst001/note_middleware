<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![Stargazers][stars-shield]][stars-url]
<!-- [![LinkedIn][linkedin-shield]][linkedin-url] -->

<!-- PROJECT LOGO -->

# 中间件

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

----------------------

## Kafka

### 参考文档

[笔记摘要](Kafka/Kafka.md)

[Kafka 简介](Kafka/notes/Kafka简介.md)

[基于 Zookeeper 搭建 Kafka 高可用集群](Kafka/notes/基于Zookeeper搭建Kafka高可用集群.md)

[Kafka 生产者详解](Kafka/notes/Kafka生产者详解.md)

[Kafka 消费者详解](Kafka/notes/Kafka消费者详解.md)

[深入理解 Kafka 副本机制](Kafka/notes/Kafka深入理解分区副本机制.md)

[Kafka 课件资料](Kafka/Direction.md)

### 基本介绍

Kafka 是一个分布式流处理平台和消息队列系统，由Apache软件基金会开发并开源。它设计用于高吞吐量、低延迟的数据流处理，以及构建实时数据流应用程序。

#### 特点和概念

+ 消息传递：Kafka 是一个消息传递系统，通过将消息从生产者发送到主题（Topic），再由消费者订阅主题来实现消息的传递。每个消息都包含一个键值对（Key-Value）的结构，可以根据需要进行扩展和利用。

+ 分布式架构：Kafka 采用分布式架构，允许将数据分片和复制到多个服务器上。这种分布式设计使得 Kafka 具有高可靠性、可扩展性和容错性，能够处理大规模的数据流和负载。

+ 主题和分区：消息被组织成主题（Topic），而每个主题又被分为多个分区（Partition）。分区允许数据在多个服务器上并行存储和处理，从而提高了吞吐量和并发性能。

+ 生产者和消费者：生产者（Producer）负责向主题发布消息，而消费者（Consumer）则订阅主题并接收消息。Kafka 支持多个生产者和消费者同时读写和处理数据。

+ 消费者组：多个消费者可以组成一个消费者组（Consumer Group），每个分区只能由同一消费者组内的一个消费者进行消费。这种机制实现了负载均衡和水平扩展，使得多个消费者可以并行处理消息。

+ 持久化存储：Kafka 使用持久化存储来保证消息的持久性和可靠性。它将消息以日志（Log）的形式追加写入磁盘，并支持数据的复制和备份，确保即使出现故障也不会丢失数据。

+ 流处理：除了作为消息队列系统，Kafka 还提供了流处理功能，允许开发人员以实时方式对数据流进行处理和转换。通过 Kafka Streams API，可以构建复杂的实时数据流应用程序。

## Nginx

### 参考文档

[课堂笔记与拓展](Nginx/Nginx.md)

[KeepAlive案例](Nginx/KeepAlive.md)

[Nginx简介](Nginx/笔记/Nginx_01.md)

[服务器配置](Nginx/笔记/Nginx_02.md)

[Rewrite功能](Nginx/笔记/Nginx_03.md)

[负载均衡](Nginx/笔记/Nginx_04.md)

[集群搭建](Nginx/笔记/Nginx_05.md)

[Nginx 课件资料](Nginx/Direction.md)


### 基本介绍
Nginx（发音为"engine-x"）是一个开源的高性能、轻量级的 Web 服务器和反向代理服务器，由Igor Sysoev创建并于2004年首次发布。它以其卓越的性能、高度可扩展性和低内存消耗而受到广泛关注和使用。

#### 特点和用途

+ 高性能：Nginx 是为处理大量并发连接和高负载而设计的。它采用事件驱动的异步架构，可以有效地处理并发请求，提供快速的响应时间和较低的延迟。

+ 反向代理：Nginx 可以作为反向代理服务器，将客户端的请求转发给后端的多个服务器。通过负载均衡和缓存策略，Nginx 可以提高网站的性能、可靠性和安全性。

+ 静态文件服务：Nginx 可以直接提供静态文件的访问，无需借助其他服务器或应用程序。这使得它非常适合用作静态资源服务器，如图片、CSS 和 JavaScript 文件等。

+ HTTP/2 和 HTTPS 支持：Nginx 支持最新的 HTTP/2 协议，提供更快的页面加载速度和更好的性能优化。此外，它还支持 HTTPS，可以进行安全的加密通信，保护网站和用户的数据安全。

+ 动态模块支持：Nginx 具有强大的模块化架构，可以通过动态加载模块扩展功能。这使得开发人员可以根据需要添加自定义模块，以满足特定的应用需求。

+ 热部署和平滑升级：Nginx 允许在不停机的情况下进行热部署和平滑升级。这意味着您可以在运行时更新配置文件、添加新的虚拟主机或模块，而不会影响现有的连接和请求。

+ 日志记录和监控：Nginx 提供详细的日志记录功能，可以记录访问日志、错误日志和性能统计信息。此外，Nginx 还与各种监控工具集成，如Prometheus、Grafana等，以便对服务器进行实时监控和性能分析。


## RabbitMQ

### 参考文档

[目录](RabbitMQ/RabbitMQ.md)

[消息队列介绍](RabbitMQ/01.消息队列介绍.md)

[安装](RabbitMQ/02.RabbitMQ-安装.md)

[简单案例](RabbitMQ/03.RabbitMQ-简单案例.md)

[发布确认](RabbitMQ/04.RabbitMQ-发布确认.md)

[交换机](RabbitMQ/05.RabbitMQ-交换机.md)

[死信队列](RabbitMQ/06.RabbitMQ-死信队列.md)

[延迟队列](RabbitMQ/07.RabbitMQ-延迟队列.md)

[发布确认高级](RabbitMQ/08.RabbitMQ-发布确认高级.md)

[幂等性、优先级、惰性](RabbitMQ/09.RabbitMQ-幂等性、优先级、惰性.md)

### 基本介绍

RabbitMQ 是一个开源的消息队列中间件，它实现了高效可靠的消息传递机制，帮助应用程序之间进行异步通信和解耦。

#### 特点和概念

+ 消息队列：RabbitMQ 使用消息队列模式来传递消息。生产者（Producer）将消息发送到队列（Queue），而消费者（Consumer）从队列中接收和处理消息。这种模式允许异步通信，使得生产者和消费者之间的耦合度降低。

+ 消息持久化：RabbitMQ 支持消息的持久化存储，即使在发生故障或重启后，也能保证消息不丢失。通过将消息保存到磁盘上的持久化队列，可以确保数据的可靠性和持久性。

+ 发布/订阅模式：除了点对点的消息传递，RabbitMQ 还支持发布/订阅模式。生产者将消息发送到交换机（Exchange），而多个消费者可以订阅该交换机并接收消息。这样可以实现一条消息被多个消费者同时接收的场景。

+ 路由和绑定：在 RabbitMQ 中，通过路由键（Routing Key）和绑定（Binding）来确定消息的路由方式。生产者将消息发布到特定的交换机，并根据路由键将消息发送到匹配的队列。

+ 队列和消费者确认：RabbitMQ 支持多个消费者同时订阅一个队列，并使用竞争机制来分发消息。每个消息只会被一个消费者接收，确保消息不会重复处理。消费者可以通过确认机制告知 RabbitMQ 已经成功接收并处理了消息。

+ 可靠性和高可用性：RabbitMQ 提供了可靠的消息传递机制，确保消息的可靠投递和顺序传递。它还支持集群和镜像队列等机制，提供高可用性和容错能力，以应对服务器故障或网络中断等情况。

+ 插件和扩展性：RabbitMQ 是一个可扩展的消息中间件，它支持各种插件和扩展，如插件管理、身份验证和授权、消息转换等。这使得 RabbitMQ 能够与其他系统集成，并满足不同场景下的需求。


## Redis

### 参考文档

[简要笔记](Redis/Redis.md)

[安装](Redis/详细笔记/redis-install.md)

[配置](Redis/详细笔记/redis-config.md)

[Redis5配置](Redis/详细笔记/redis5-config.md)

[安全设置](Redis/详细笔记/redis-safety.md)

[Lua接口实现](Redis/详细笔记/redis-lua.md)

[Redis 课件资料](Redis/Direction.md)


### 基本介绍

Redis（Remote Dictionary Server）是一个开源的内存数据存储系统，它提供了高性能、可扩展和灵活的键值对存储。Redis 以其快速读写速度和丰富的数据结构支持而受到广泛关注和使用。

#### 特点和概念

+ 内存存储：Redis 将数据存储在内存中，因此可以实现非常快速的读写操作。它还提供了持久化选项，可以将数据定期保存到磁盘上，以便在重启后恢复数据。

+ 键值对存储：Redis 使用键值对的方式存储数据，其中键是唯一的标识符，值可以是各种类型的数据，如字符串、列表、哈希表、集合等。这种简单的数据模型使得 Redis 非常适合缓存、会话存储、排行榜等应用场景。

+ 数据结构支持：Redis 提供了丰富的数据结构支持，如字符串（String）、列表（List）、哈希表（Hash）、集合（Set）、有序集合（Sorted Set）等。每种数据结构都有相应的操作命令，使得 Redis 可以灵活地处理不同类型的数据。

+ 发布/订阅模式：Redis 支持发布/订阅模式，其中生产者（Publisher）将消息发布到指定的频道（Channel），而订阅者（Subscriber）可以订阅一个或多个频道，并接收相应的消息。这种模式可用于实现实时消息传递和事件通知。

+ 事务支持：Redis 支持事务，允许一组操作原子地执行。通过 MULTI 和 EXEC 命令，可以将多个命令放在一个事务中，并确保它们按顺序执行，从而保证数据的一致性。

+ 分布式缓存：Redis 可以用作分布式缓存，通过将数据存储在内存中，提供快速访问和响应时间。它还支持集群和主从复制等机制，提供高可用性和可伸缩性。

+ Lua 脚本支持：Redis 支持使用 Lua 脚本进行自定义操作和批量操作。通过编写 Lua 脚本，可以在服务器端执行复杂的业务逻辑，减少网络传输开销并提高性能。


## Tomcat

### 参考文档

[入门摘要](Tomcat/Tomcat.md)

[详细笔记](Tomcat/笔记/Tomcat专题.md)

### 基本介绍

Tomcat（全名为Apache Tomcat）是一个开源的Java Servlet容器和Web服务器，由Apache软件基金会开发并维护。它提供了一个运行Java Web应用程序的环境，并支持Java Servlet、JavaServer Pages（JSP）和Java WebSocket等技术。

#### 特点和概念

+ Servlet容器：Tomcat 是一个Servlet容器，它可以运行基于Java Servlet规范的Web应用程序。它负责接收来自客户端的HTTP请求，并调用相应的Servlet进行处理和响应。

+ JSP支持：Tomcat 支持JavaServer Pages（JSP），这是一种动态网页技术，允许将Java代码嵌入到HTML页面中。通过Tomcat，JSP页面可以被编译成Servlet，并在Web应用程序中执行。

+ Web服务器功能：除了作为Servlet容器，Tomcat 也具备Web服务器的功能。它可以处理静态资源文件，如HTML、CSS、JavaScript等，并提供对这些文件的直接访问。

+ 配置管理：Tomcat 使用XML格式的配置文件来管理和配置应用程序。通过修改配置文件，您可以指定虚拟主机、连接池大小、端口号、安全性设置等参数。

+ 虚拟主机支持：Tomcat 支持多个虚拟主机，允许在同一台服务器上托管多个域名和网站。每个虚拟主机可以有自己独立的配置和Web应用程序。

+ 连接池管理：Tomcat 提供连接池来管理数据库连接、线程等资源。连接池可以提高性能和可伸缩性，避免每次请求都创建和销毁连接的开销。

+ 安全性支持：Tomcat 提供了各种安全功能，如SSL/TLS支持、访问控制、身份验证和授权机制等。这些功能可以保护Web应用程序和服务器免受恶意攻击和未经授权的访问。

+ 扩展性和插件支持：Tomcat 是一个可扩展的容器，可以通过添加插件和扩展组件来增强其功能。例如，可以添加JDBC驱动程序、连接池实现、日志记录工具等。


## Zookeeper

### 参考文档

[Zookeeper 简介及核心概念](ZooKeeper/notes/Zookeeper简介及核心概念.md)

[Zookeeper 单机环境和集群环境搭建](ZooKeeper/notes/Zookeeper单机环境和集群环境搭建.md)

[Zookeeper 常用 Shell 命令](ZooKeeper/notes/Zookeeper常用Shell命令.md)

[Zookeeper Java 客户端 —— Apache Curator](ZooKeeper/notes/Zookeeper_Java客户端Curator.md)

[Zookeeper ACL 权限控制](ZooKeeper/notes/Zookeeper_ACL权限控制.md)

[Zookeeper 课件资料](ZooKeeper/Direction.md)

### 基本介绍

ZooKeeper 是一个开源的分布式协调服务，由Apache软件基金会开发并维护。它提供了高可用性和一致性的数据管理和协调功能，用于构建分布式系统和应用程序。

#### 特点和概念

+ 分布式协调：ZooKeeper 旨在解决分布式系统中的一致性和协调问题。它提供了分布式锁、分布式队列、选举算法等原语，用于协调和同步分布式节点之间的操作和状态。

+ 层次化命名空间：ZooKeeper 使用层次化的命名空间结构，类似于文件系统的目录结构。每个节点都可以存储数据和子节点，形成一个有序的树状结构。

+ 数据发布/订阅：ZooKeeper 支持数据的发布和订阅机制。客户端可以监视节点的数据变化，并在数据发生改变时接收通知。

+ 高可用性和容错性：ZooKeeper 提供了高可用性和容错性的机制。它使用多台服务器来共同提供服务，通过选举算法选出领导者（Leader）服务器，并能够在领导者故障时自动进行切换。

+ 快速的读写操作：ZooKeeper 将数据存储在内存中，以提供快速的读写操作。它使用了类似于Paxos算法的ZAB（ZooKeeper Atomic Broadcast）协议，确保数据的一致性和可靠性。

+ ACID 事务支持：ZooKeeper 提供了原子性、一致性、隔离性和持久性（ACID）的事务支持。多个操作可以组成一个事务单元，并要么全部成功执行，要么全部回滚。

+ 轻量级和简单性：ZooKeeper 是一个轻量级的分布式协调服务，具有简单的API和易于部署的特点。它适用于构建大规模分布式系统和应用程序。


## ElasticSearch

### 参考文档

[课程笔记](ElasticSearch/课程笔记.md)

[ElasticSearch 课件资料](ElasticSearch/Direction.md)

### 基本介绍

Elasticsearch 是一个开源的分布式搜索和分析引擎，由Elastic公司开发并维护。它构建在Apache Lucene搜索库之上，并提供了简单易用的RESTful API，用于实时搜索、分析和存储大规模数据。

#### 特点和概念

+ 分布式搜索：Elasticsearch 使用分布式架构来处理大规模数据集。它将数据分片和复制到多个节点上，从而实现数据的高可用性、容错性和并行处理能力。

+ 实时搜索：Elasticsearch 提供了实时搜索功能，可以在几乎没有延迟的情况下快速检索数据。当新的文档添加到索引中时，它们几乎立即就可以被搜索到。

+ 强大的查询语言：Elasticsearch 使用结构化查询语句（Query DSL）来构建复杂的查询请求。通过 Query DSL，您可以执行全文搜索、过滤、聚合、排序等各种查询操作。

+ 多种数据类型支持：Elasticsearch 支持多种数据类型，如文本、数字、日期、地理位置等。它还提供了丰富的分词器和分析器，用于处理不同语言和特定领域的数据。

+ 分布式聚合与分析：Elasticsearch 具有强大的聚合和分析功能，可用于从大规模数据中提取有价值的洞察力。它支持各种聚合操作，如求和、平均、最小/最大值、分组等。

+ 文档存储和索引：Elasticsearch 使用文档导向的数据模型来存储和管理数据。每个文档都是一个自包含的JSON对象，并且可以通过唯一标识符进行索引和检索。

+ 可扩展性和插件生态系统：Elasticsearch 具有良好的可扩展性，并支持水平扩展和集群部署。此外，它还拥有丰富的插件生态系统，使开发人员能够根据需求添加功能和扩展。

+ 日志分析和监控：由于其快速的搜索和聚合能力，Elasticsearch 在日志分析和实时监控方面非常流行。它可以用于处理和分析大量的日志数据，并通过可视化工具（如Kibana）提供实时的数据可视化和仪表板。


<!-- links -->
[your-project-path]:shaojintian/Best_README_template
[contributors-shield]: https://img.shields.io/github/contributors/worst001/note_middleware.svg?style=flat-square
[contributors-url]: https://github.com/worst001/note_middleware/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/worst001/note_middleware.svg?style=flat-square
[forks-url]: https://github.com/worst001/note_middleware/network/members
[stars-shield]: https://img.shields.io/github/stars/worst001/note_middleware.svg?style=social
[stars-url]: https://github.com/worst001/note_middleware/stargazers
[issues-shield]: https://img.shields.io/github/issues/worst001/note_middleware.svg?style=flat-square
[issues-url]: https://img.shields.io/github/issues/worst001/note_middleware.svg
[license-shield]: https://img.shields.io/github/license/worst001/note_middleware.svg?style=flat-square
[license-url]: https://github.com/worst001/note_middleware/blob/main/LICENSE.txt
