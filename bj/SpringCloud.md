# SpringCloud

```JAVA
三层架构+ MVC
    
框架:

 	Spring IOC AOP
	SprintBoot，新一代的JavaEE开发标准，自动装配

	模块化~  a11 in one
	
    模块化的开发===a11 in one，代码没变化~
   
微服务架构4个核心问题?
	1.服务很多，客户端该怎么访问?
	2.这么多服务? 服务之间如何通信?
	3.这么多服务? 如何治理?
	4.服务挂了怎么办?
解决方案:
	Spring c1oud 生态! SpringBoot~

        
    1. Spring cloud NetF1ix- 站式解决方案!
		api网关，zuu1组件
		Feign ---HttpClinet ---- Http通信方式，同步，阻塞服务注册发现:
		Eureka
        熔断机制: Hystrix
		。。。。
            
            
	2. Apache Dubbo Zookeeper半自动，需要整合别人的! 
		API:没有，找第三方组件，或者自己实现
		Dubbo 
        Zookeepe 
		没有:借助Hystrix
		
        Dubbo这个方案并不完善~

   
     3. Spring c1oud Alibaba-站式解决方案 !

            
新概念:服务网格~ Server Mesh 
    istio
    
万变不离其宗
    1. API
    2. HTTP，RPC
    3.注册和发现
    4.熔断机制
           
网络不可靠!
```



## 1、常见面试题

**1.1、 什么是微服务?**
**1.2、微服务之间是如何独立通讯的?**
**1.3、SpringCloud 和Dubbo有哪些区别?**
**1.4、SpringBoot和SpringCloud,请你谈谈对他们的理解**
**1.5、什么是服务熔断?什么是服务降级**
**1.6、 微服务的优缺点是分别是什么?说下你在项目开发中遇到的坑**
**1.7、你所知道的微服务技术栈有哪些?请列举一二**
**1.8、eureka和zookeeper都可以提供服务注册与发现的功能，请说说两个的区别?**





## 2、微服务概述

### 2.1、什么是微服务

**什么是微服务?**  微服务(Microservice Architecture)  是近几年流行的一-种架构思想，关于它的概念很难一言以蔽之

究竟什么是微服务呢?我们在此引用ThoughtWorks公司的首席科学家Martin Fowler于2014年提出的一段话:

<img src="C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325205400.png" style="zoom: 80%;" />

原文: https://martinfowler.com/articles/microservices.html

汉化: https://www.cnblogs.com/liuning8023/p/4493156.html



* 就目前而言，对于微服务，业界并没有-个统一的,标准的定义
* 但通常而言，微服务架构是一 种架构模式,或者说是一 种架构风格，**它提倡将单一的应用程序划分成一组小的服务**，每个服务运行在其独立的自己的进程内，服务之间互相协调，互相配置，为用户提供最终价值。服务之间采用轻量级的通信机制互相沟通，每个服务都围绕着具体的业务进行构建，并且能够被独立的部署到生产环境中，另外，应尽量避免统一的，集中式的服务管理机制，对具体的一一个服务而言，应根据业务上下文,选择合适的语言，工具对其进行构建,可以有-一个非常轻量级的集中式管理来协调这些服务，可以使用不同的语言来编写服务,也可以使用不同的数据存储;



**可能有的人觉得官方的话太过生涩，我们从技术维度来理解下:**

* 微服务化的核心就是将传统的一站式应用，根据业务拆分成一 个一个的服务，彻底地去耦合，每一个微服务提供单个业务功能的服务，-个服务做-件事情，从技术角度看就是一种小而独立的处理过程, 类似进程的概念，能够自行单独启动或销毁,拥有自己独立的数据库。



### 2.2、微服务与微服务架构

**微服务**

强调的是服务的大小，他关注的是某一个点, 是具体解决某一个问题提供落地对应服务的一个服务应用，狭义的看，可以看做是IDEA中的一个个微服务工程，或者Moudel

```
IDEA工具里面使用Maven开发的一个个独立的小Moudle，它具体是使用springboot开发的一个小模块，专业的事情交给专业的模块来做，一个模块就做着一件事情
强调的是一个个的个体， 每个个体完成一个具体的任务或者功能!
```



**微服务架构**

一种新的架构形式，Martin Fowler, 2014提出


微服务架构是一种架构模式，它提倡将单- -应用程序划分成一组小的服务, 服务之间互相协调，互相配合，为用户
提供最终价值。每个服务运行在其独立的进程中，服务于服务间采用轻量级的通信机制互相协作，每个服务都围绕
着具体的业务进行构建,并且能够被独立的部署到生产环境中，另外，应尽量避免统一的, 集中式的服务管理机
制，对具体的一个服务而言,应根据业务上下文,选择合适的语言，工具对其进行构建。





### 2.3、微服务优缺点

**优点**

* 每个服务足够内聚,足够小,代码容易理解，这样能聚焦一 个指定的业务功能或业务需求;

* 开发简单,开发效率提高，一个服务可能就是专一的只干一件事;

* 微服务能够被小团队单独开发,这个小团队是2~5人的开发人员组成;
  微服务是松耦合的，是有功能意义的服务，无论是在开发阶段或部署阶段都是独立的。

* 微服务能使用不同的语言开发。
  ,易于和第三方集成，微服务允许容易且灵活的方式集成自动部署，通过持续集成工具，如jenkins, Hudson,
  bamboo

* 微服务易于被一个开发人员理解，修改和维护，这样小团队能够更关注自己的工作成果。无需通过合作才能体
  现价值。

* 微服务允许你利用融合最新技术。

* 微服务只是业务逻辑的代码，不会和HTML，CSS 或其他界面混合

* 每个微服务都有自己的存储能力，可以有自己的数据库，也可以有统一数据库



**缺点:**

* 开发人员要处理分布式系统的复杂性

* 多服务运维难度,随着服务的增加，运维的压力也在增大

* 系统部署依赖

* 服务间通信成本

* 数据一致性

* 系统集成测试

* 性能监控....



### 2.4、微服务技术栈有哪些?

| 微服务条目                              | 落地技术                                                     |
| --------------------------------------- | ------------------------------------------------------------ |
| 服务开发                                | SpringBoot,Spring,SpringMVC                                  |
| 服务配置与管理                          | Netflix公司的Archaius、阿里的Diamond等                       |
| 服务注册与发现                          | Eureka、Consul、 Zookeeper等                                 |
| 服务调用                                | Rest、RPC、 gRPC                                             |
| 服务熔断器                              | Hystrix、Envoy等                                             |
| 负载均衡                                | Ribbon、Nginx等                                              |
| 服务接口调用 (客户端调用服务的简化工具) | Feign等                                                      |
| 消息队列                                | Kafka、RabbitMQ、 ActiveMQ等                                 |
| 服务配置中心管理                        | SpringCloudConfig、Chef等                                    |
| 服务路由 (API网关)                      | Zuul等                                                       |
| 服务监控                                | Zabbix、Nagios、 Metrics、Specatator等                       |
| 全链路追踪                              | Zipkin、Brave、 Dapper等                                     |
| 服务部署                                | Docker、OpenStack. Kubernetes等                              |
| 数据流操作开发包                        | SpringCloud Stream(封装与Redis, Rabbit, Kafka等发送接收消息) |
| 事件消息总线                            | SpringCloud Bus                                              |



### 2.5、为什么选择SpringCloud作为微服务架构

#### 1、选型依据

* 整体解决方案和框架成熟度

* 社区热度

* 可维护性

* 学习曲线

#### 2、当前各大IT公司用的微服务架构有哪些?

* 阿里: dubbo+HFS

* 京东: JSF

* 新浪: Motan
* 当当网 DubboX

#### 3、各微服务框架对比

| 功能点/<br>服务       框架 | Netflix/SpringCloud                                          | Motan                                                       | gRPC                      | Thrift   | Dubbo/DubboX                        |
| -------------------------- | :----------------------------------------------------------- | ----------------------------------------------------------- | ------------------------- | -------- | ----------------------------------- |
| 功能    定位               | 完整的微服务框架                                             | RPC框架，但整合了ZK或Consul,实现集群环境的基本服务注册/发现 | RPC框架                   | RPC框架  | 服务框架                            |
| 支持Rest                   | 是，Ribbon支持多种可插拔的序列化选择                         | 否                                                          | 否                        | 否       | 否                                  |
| 支持 RPC                   | 否                                                           | 是(Hession2)                                                | 是                        | 是       | 是                                  |
| 支持    多语言             | 是(Rest形式) ?                                               | 否                                                          | 是                        | 是       | 否                                  |
| 负载     均衡              | 是(服务端zuul+客户端Ribbon)，zuul-服务， 动态路由，云端负载均衡Eureka (针对中间层服务器) | 是(客户端)                                                  | 否                        | 否       | 是(客户端)                          |
| 配置    服务               | Netfix Archaius, SpringCloud Config Server集中配置           | 是(zookeeper提供)                                           | 否                        | 否       | 否                                  |
| 服务    调用    链监    控 | 是. (zuul)，zuul提供边缘服务，API网关                        | 否                                                          | 否                        | 否       | 否                                  |
| 高可       用/       容错  | 是(服务端Hystrix+客户端Ribbon)                               | 是(客户端)                                                  | 否                        | 否       | 是(客户端)                          |
| 典型    应用    案例       | Netflix                                                      | Sina                                                        | Google                    | Facebook |                                     |
| 社区    活跃    程度       | 高                                                           | 一般                                                        | 高                        | 一般     | 2017年后重新开始维护，之前中断了5年 |
| 学习    难度               | 中断                                                         |                                                             | 高                        | 高       | 低                                  |
| 文档    丰富    程度       | 高                                                           | 一般                                                        | 一般                      | 一般     | 高                                  |
| 其他                       | Spring Cloud Bus为我们的应用程序带来了更多管理端点           | 支持降级                                                    | Netflix内部在开发集成gRPC | IDL定义  | 实践的公司比较多                    |







### 3、SpringCloud入门概述

#### 3.1、SpringCloud是什么

Spring'官网:https://spring.io/

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325213810.png)

<img src="C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325213853.png"  />

------

SpringCloud,基于SpringBoot提供了一套微服务解决方案， 包括服务注册与发现，配置中心，全链路监控,服务网关，负载均衡，熔断器等组件,除了基于NetFlix的开源组件做高度抽象封装之外,还有一些选型中立的开源组件。

SpringCloud利用SpringBoot的开发便利性,巧妙地简化了分布式系统基础设施的开发，SpringCloud为开发人员 ，提供了快速构建分布式系统的一些工具，**包括配置管理，服务发现，断路器，路由，微代理，事件总线，全局锁，决策竞选，分布式会话等等,**他们都可以用SpringBoot的开发风格做到- -键启动和部署。

SpringBoot并没有重复造轮子，它只是将目前各家公司开发的比较成熟，经得起实际考研的服务框架组合起来,通过SpringBoot风格进行再封装，屏蔽掉了复杂的配置和实现原理，**最终给开发者留出了一套简单易懂，易部署和易维护的分布式系统开发工具包**

SpringCloud是分布式微服务架构下的一-站式解决方案，是各个微服务架构落地技术的集合体，俗称微服务全家
桶。



#### 3.2、SpringCloud和SpringBoot关系

* SpringBoot专注于快速方便的开发单个个体微服务。-Jar

* SpringCloud是关注全 局的微服务协调整理治理框架，它将SpringBoot开发的一 个个单体微服务整合并管理起来,为各个微服务之间提供:配置管理，服务发现，断路器，路由，微代理，事件总线，全局锁,决策竞选,分布式会话等等集成服务。

* SpringBoot可以离开SpringClooud独立使用， 开发项目，但是SpringCloud离不开SpringBoot, 属于依赖关系

* **SpringBoot专注于快速、方便的开发单个个体微服务，SpringCloud关注全局的服务治理框架**



#### 3.3、Dubbo 和SpringCloud技术选型

##### 1、分布式+服务治理Dubbo

目前成熟的互联网架构:应用服务化拆分+消息中间件



##### 2、Dubbo和SpringCloud对比

可以看一下社区活跃度
https://github.com/dubbo
https://github.com/spring-cloud

**结果:**

|              | Dubbo         | Spring                       |
| ------------ | ------------- | ---------------------------- |
| 服务注册中心 | Zookeeper     | Spring Cloud Netfilx Eureka  |
| 服务调用方式 | RPC           | REST API                     |
| 服务监控     | Dubbo-monitor | Spring Boot Admin            |
| 断路器       | 不完善        | Spring Cloud Netflix Hystrix |
| 服务网关     | 无            | Spring Cloud Netflix Zuul    |
| 分布式配置   | 无            | Spring Cloud Config          |
| 服务跟踪     | 无            | Spring Cloud Sleuth          |
| 消息总线     | 无            | Spring Cloud Bus             |
| 数据流       | 无            | Spring Cloud Stream          |
| 批量任务     | 无            | Spring Cloud Task            |

**最大区别: SpringCloud抛弃 了Dubbo的RPC通信,采用的是基于HTTP的REST方式。**
严格来说，这两种方式各有优劣。虽然从一定程度上来说，后者牺牲了服务调用的性能，但也避免了上面提到的原生RPC带来的问题。而且REST相比RPC更为灵活，服务提供方和调用方的依赖只依靠一纸契约, 不存在代码级别的强依赖，这在强调快速演化的微服务环境下，显得更加合适。

**品牌机与组装机的区别**
很明显，Spring Cloud的功能比DUBBO更加强大，涵盖面更广，而且作为Spring的拳头项目，它也能够与SpringFramework、Spring Boot、Spring Data、Spring Batch等其他Spring项目完美融合,这些对于微服务而言是至关重要的。使用Dubbo构建的微服务架构就像组装电脑，各环节我们的选择自由度很高，但是最终结果很有可能
因为一条内存质量不行就点不亮了，总是让人不怎么放心,但是如果你是一名高手,那这些都不是问题;而SpringCloud就像品牌机，在Spring Source的整合下，做了大量的兼容性测试,保证了机器拥有更高的稳定性，但是如果要在使用非原装组件外的东西，就需要对其基础有足够的了解。

**社区支持与更新力度**
最为重要的是，DUBBO停止了5年左右的更新，虽然2017.7重启了。 对于技术发展的新需求，需要由开发者自行
拓展升级(比如当当网弄出了DubboX)，这对于很多想要采用微服务架构的中小软件组织，显然是不太合适的,
中小公司没有这么强大的技术能力去修改Dubbo源码+周边的一整套解决方案,并不是每一个公司都有阿里的大牛+真实的线上生产环境测试过。

**设计模式+微服务拆分思想**

**总结:**
曾风靡国内的开源RPC服务框架Dubbo在重启维护后，令许多用户为之雀跃,但同时，也迎来了-些质疑的声音。互联网技术发展迅速, Dubbo是否还能跟上时代? Dubbo与Spring Cloud相比又有何优势和差异?是否会有相关举措保证Dubbo的后续更新频率?

人物: Dubbo重启维护开发的刘军，主要负责人之一

刘军，阿里巴巴中间件高级研发工程师，主导了Dubbo重启维护以后的几个发版计划，专注于高性能RPC框架和微服务相关领域。曾负责网易考拉RPC框架的研发及指导在内部使用，参与了服务治理平台、分布式跟踪系统、分布式-致性框架等从无到有的设计与开发过程。

**解决的问题域不-样: Dubbo的定位是一-款RPC框架， Spring Cloud的目标是微服务架构下的-站式解决方案**



#### 3.4、SpringCloud能干嘛

* Distributed/versioned configuration (分布式/版本控制配置)

* Service registration and discovery (服务注册与发现)

* Routing (路由)

* Service-to-service calls (服务到服务的调用)

* Load balancing (负载均衡配置)

* Circuit Breakers (断路器)

* Distributed messaging (分布式消息管理)

* ...

#### 3.5、SpringCloud在哪下

官网: http://projects.spring.io/spring-cloud/

这玩意的版本号有点特别

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325215322.png)

```xml
Spring cloud是一个由众多独立子项目组成的大型综合项目，每个子项目有不同的发行节奏，都维护着自己的发布版本号。Spring Cloud通过一个资源清单BOM (Bi11 of Materials) 来管理每个版本的子项目清单。为避免与子项目的发布号混淆，所以没有采用版本号的方式，而是通过命名的方式。
这些版本名称的命名方式采用了伦敦地铁站的名称，同时根据字母表的顺序来对应版本时间顺序，比如:最早的Release版本: Angel,第二个Release版本: Brixton, 然后是Camden、Dalston、 Edgware，目前最新的是Finch1ey版本。    
```

参考书:

* https://springcloud.cc/spring-cloud-netflix.html
* 中文API文档: https://springcloud.cc/spring-cloud-dalston.html
* SpringCloud中国社区http://springcloud.cn/
* SpringCloud中文网https://springcloud.cc



#### 4.1 总体介绍

* 我们会使用一-个Dept部| ]模块做一个微服务通用案Consumer消费者 (Client) 通过REST调 用Provider提供者(Server) 提供的服务。

* 回忆Spring, SpringMVC, MyBatis等以往学习的知识。 。。

* Maven的分包分模块架构复习

```java
一个简单的Maven模块结构是这样的:

app-parent:一个父项目(app-parent) 聚合很多子项目(app-uti1， app-dao，app-web... )
|-- pom. xm1
|
|-- app-core
||----pom. xm7
|
| -- app -web
| |----pom. xm7
......
```



一个父工程带着多个子Module子模块

MicroServiceCloud父工程(Project) 下初次带着3个子模块 (Module)

* microservicecloud-api [封装的整体entity/接口/公共配置等 ]

* microservicecloud-provider-dept-8001 [服务提供者]
* microservicecloud-consumer-dept-80 [服务消费者]



#### 4.2、创建父工程

* 新建父工程项目microservicecloud, 切记Packageing是pom模式

* 主要是定义POM文件,将后续各个子模块公用的jar包等统一 提取出来,类似一个抽象父类

**pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.kuang</groupId>
    <artifactId>springcloud</artifactId>
    <version>1.0-SNAPSHOT</version>

    <packaging>pom</packaging>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <junit.version>4.12</junit.version>
        <log4j.version>1.2.17</log4j.version>
        <lombok.version>1.18.12</lombok.version>
    </properties>


    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>0.2.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--EUREKA-->
            <!--https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-eureka -->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-starter-eureka</artifactId>
                <version>1.4.6.RELEASE</version>
            </dependency>
            <!--springCloud的依赖-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Greenwich.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--SpringBoot-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.1.4.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--数据库-->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>8.0.19</version>
            </dependency>
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>1.1.10</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>2.1.1</version>
            </dependency>
            <!--SpringBoot 启动器-->
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>2.1.1</version>
            </dependency>
            <!--日志测试~-->
            <dependency>
                <groupId>ch.qos.logback</groupId>
                <artifactId>logback-core</artifactId>
                <version>1.2.3</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.12</version>
            </dependency>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.17</version>
            </dependency>
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>1.18.12</version>
            </dependency>

        </dependencies>

    </dependencyManagement>

</project>
```



### 5、Eureka服务注册与发现

#### 5.1、什么是Eureka

* Netflix 在设计Eureka时，遵循的就是AP原则

* Eureka是Netflix的一 个子模块，也是核心模块之一。Eureka是一 个基于REST的服务，用于定位服务，以实现云端中间层服务发现和故障转移,服务注册与发现对于微服务来说是非常重要的，有了服务发现与注册，只需要使用服务的标识符，就可以访问到服务，而不需要修改服务调用的配置文件了，功能类似于Dubbo的注册中心，比如Zookeeper;

#### 5.2、原理讲解

* Eureka的基本架构
  * SpringCloud 封装了NetFlix公司开发的Eureka模块来实现服务注册和发现(对比Zookeeper)
  * Eureka采用了C-S的架构设计，EurekaServer 作为服务注册功能的服务器，他是服务注册中心
  * 而系统中的其他微服务。使用Eureka的客户端连接到EurekaServer并维持心跳连接。 这样系统的维护人员就可以通过EurekaServer来监控系统中各个微服务是否正常运行，SpringCloud的一些其他模块(比如Zuul)就可以通过EurekaServer来发现系统中的其他微服务，并执行相关的逻辑;

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325221154.png)

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325221218.png)

* Eureka 包含两个组件: Eureka Server和Eureka Client。
* Eureka Server提供服务注册服务，各个节点启动后，会在EurekaServer中进行注册，这样Eureka Server中的服务注册表中将会村粗所有可用服务节点的信息，服务节点的信息可以在界面中直观的看到。
* Eureka Client是一个Java客户端， 用于简化EurekaServer的交互，客户端同时也具备一个内置的，使用轮
  询负载算法的负载均衡器。在应用启动后，将会向EurekaServer发送心跳(默认周期为30秒)。如果
  Eureka Server在多个心跳周期内没有接收到某个节点的心跳，EurekaServer将 会从服务注册表中把这个
  服务节点移除掉(默认周期为90秒)



* 三大角色
  * Eureka Server:提供服务的注册于发现。
  * Service Provider:将自身服务注册到Eureka中，从而使消费方能够找到。
  * Service Consumer:服务消费方从Eureka中获取注册服务列表，从而找到消费服务。

#### 5.3、构建步骤

##### 1、eureka-server

1. springcloud-eureka-7001模块建立
2. pom.xml配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>springcloud</artifactId>
        <groupId>com.kuang</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>springcloud-eureka-7001</artifactId>

    <!--导包-->
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
            <version>2.2.1.RELEASE</version>
        </dependency>
        <!--热部署工具-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

    </dependencies>

</project>

```

**自我保护机制:好死不如赖活着**
一句话总结:某时刻某一一个微服务不可以用了，eureka不会 立刻清理，依旧会对该微服务的信息进行保存!

* 默认情况下，如果EurekaServer在一 定时间内没有接收到某个微服务实例的心跳，EurekaServer将会注销该实例(默认90秒)。但是当网络分区故障发生时，微服务与Eureka之间无法正常通行，以上行为可能变得非常危险了-因为微服务本身其实是健康的，此时本不应该注销这个服务。Eureka通过 自我保护机制来解决这个问题--当EurekaServer节点在短时间内丢失过多客户端时(可能发生了网络分区故障),那么这个节 点就会进入自我保护模式。一旦进入该模式，EurekaServer就会保护服务注册表中的信息，不再删除服务注册表中的数据(也就是不会注销任何微服务)。当网络故障恢复后，该EurekaServer节 点会自动退出自我保护模式。

* 在自我保护模式中，EurekaServer会保护服务注册表中的信息，不再注销任何服务实例。当它收到的心跳数重新恢复到阈值以上时，该EurekaServer节 点就会自动退出自我保护模式。它的设计哲学就是宁可保留错误的服务注册信息，也不盲目注销任何可能健康的服务实例。-句话:好死不如赖活着

* 综上，自我保护模式是- -种应对网络异常的安全保护措施。它的架构哲学是宁可同时保留所有微服务(健康的微服务和不健康的微服务都会保留)，也不盲目注销任何健康的微服务。使用自我保护模式，可以让Eureka集群更加的健壮和稳定

* 在SpringCloud中，可以使用eureka. server . enab1e-self-preservation = false 禁用自我保护模式
  [不推荐关闭自我保护机制]



#### 5.4、对比Zookeeper

**回顾CAP原则**
RDBMS   (Mysql、 Oracle、 sqlServer) ===>ACID
NoSQL   (redis、 mongdb) ===> CAP

**ACID是什么?**

* A (Atomicity) 原子性

* C(Consistency)- 致性

* | (Isolation) 隔离性

* D (Durability) 持久性

**CAP是什么?**

* C (Consistency) 强一致性

* A (Availability) 可用性

* P (Partition tolerance) 分区容错性

CAP的三进二: CA、AP、CP 

CAP理论的核心

* 一个分布式系统不可能同时很好的满足一 致性，可用性和分区容错性这三个需求

* 根据CAP原理,将NoSQL数据库分成了满足CA原则，满足CP原则和满足AP原则三大类:
  * CA:单点集群，满足一致性，可用性的系统，通常可扩展性较差
  * CP:满足一 致性，分区容错性的系统,通常性能不是特别高
  * AP:满足可用性，分区容错性的系统，通常可能对一致性要求低一些



#### 作为服务注册中心，Eureka比kZookeeper好在哪里?

著名的CAP理论指出，-一个分布式系统不可能同时满足C (- 致性)、A (可用性)、P (容错性)。
由于分区容错性P在分布式系统中是必须要保证的，因此我们只能在A和C之间进行权衡。

* Zookeeper保证的是CP;

* Eureka保证的是AP;

**Zookeeper保证的是CP**
     当向注册中心查询服务列表时,我们可以容忍注册中心返回的是几分钟以前的注册信息，但不能接受服务直接down掉不可用。也就是说，服务注册功能对可用性的要求要高于一致性。 但是zk会出现这样一-种情况， 当master节点因为网络故障与其他节点失去联系时,剩余节点会重新进行leader选举。问题在于，选举leader的时间太长,
30~120s，且选举期间整个zk集群都是不可用的，这就导致在选举期间注册服务瘫痪。在云部署的环境下，因为网络问题使得zk集群失去master'节点是较大概率会发生的事件，虽然服务最终能够恢复，但是漫长的选举时间导致的注册长期不可用是不能容忍的。



**Eureka保证的是AP**

​		Eureka看明白了这一-点，因此在设计时就优先保证可用性。Eureka各个节 点都是平等的，几个节点挂掉不会影响正常节点的工作，剩余的节点依然可以提供注册和查询服务。而Eureka的客户端在向某个Eureka注册时，如果发现连接失败,则会自动切换至其他节点，只要有-台Eureka还在,就能保住注册服务的可用性,只不过查到的
信息可能不是最新的，除此之外，Eureka还有-种自我保护机制，如果在15分钟内超过85%的节点都没有正常的心跳，那么Eureka就认为客户端与注册中心出现了网络故障,此时会出现以下几种情况:

1. Eureka不再从注册列表中移除因为长时间没收到心跳而应该过期的服务
2. Eureka仍然能够接受新服务的注册和查询请求,但是不会被同步到其他节点上( 即保证当前节点依然可用)
3. 当网络稳定时，当前实例新的注册信息会被同步到其他节点中



因此，Eureka可以很好的应对因网络故障导致部分节点失去联系的情况，而不会像zookeeper那样使整个注册服务瘫痪



**ribbon是什么?**

* Spring Cloud Ribbon是基于Netflix Ribbon实现的一 套客户端负载均衡的工具。
* 简单的说，Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法，将NetFlix的中间层服务连接在一起。Ribbon的客 户端组件提供一系列完整的配置项如: 连接超时、重试等等。 简单的说，就是在配置文件中列出LoadBalancer (简称LB:负载均衡)后面所有的机器，Ribbon会 自动的帮助你基于某种规则(如简单轮询，随机连接等等)去连接这些机器。我们也很容易使用Ribbon实现自定义的负载均衡算法!

**ribbon能干嘛?**

* LB,即负载均衡(Load Balance) ，在微服务或分布式集群中经常用的一种应用。

* 负载均衡简单的说就是将用户的请求平摊的分配到多个服务上，从而达到系统的HA (高可用)。

* 常见的负载均衡软件有Nginx, Lvs等等

* dubbo、 SpringCloud中均给我们提供 了负载均衡，SpringCloud的负载均衡算法可以自定义

* 负载均衡简单分类:

  * 集中式LB .

    * 即在服务的消费方和提供方之间使用独立的LB设施，如Nginx, 由该设施负责把访问请求通过某种策略转发至服务的提供方! 

  * 进程式LB

    * 将LB逻辑集成到消费方,消费方从服务注册中心获知有哪些地址可用，然后自己再从这些地址中选出一个合适的服务器。

    * Ribbon就属于进程内LB，它只是一个类库，集成于消费方进程，消费方通过它来获取到服务提供方的地址



### 7、Feign负载均衡

#### 7.1、简介

feign是声明式的web service客户端，它让微服务之间的调用变得更简单了，类似controller调用service。 SpringCloud集成了Ribbon和Eureka,可在使用Feign时提供负载均衡的http客户端。

只需要创建一个接口，然后添加注解即可!

feign，主要是社区,大家都习惯面向接口编程。这个是很多开发人员的规范。调用微服务访问两种方法
	1.微服务名字[ribbon]
	2.接口和注解[feign ]



**Feign能干什么?**

* Feign旨在使编写Java Http客户端变得更容易

* 前面在使用Ribbon + RestTemplate时, 利用RestTemplate对Http请求的封装处理，形成了- 套模板化的调用方法。但是在实际开发中，由于对服务依赖的调用可能不止一-处, 往往一个接口会被多处调用，所以通常都会针对每个微服务自行封装一些客户端类来包装这些依赖服务的调用。所以，Feign在此基础 上做了进一步封装，由他来帮助我们定义和实现依赖服务接口的定义，在Feign的实现下，我们只需要创建一一个接口并使用注解的方式来配置它(类似于以前Dao接口上标注Mapper注解，现在是一一个微服务接口 上面标注一个Feign注解即可。)即可完成对服务提供方的接口绑定，简化了使用Spring Cloud Ribbon时,自动封装服务调用客户端的开发量。



**Feign集成了Ribbon**

* 利用Ribbon维护了MicroServiceCloud-Dept的服务列表信息，并且通过轮询实现了客户端的负载均衡，而与Ribbon不同的是，通过Feign只需要定义服务绑定接口且以声明式的方法，优雅而且简单的实现了服务调用。



**分布式系统面临的问题**

​	复杂分布式体系结构中的应用程序有数-十个依赖关系，每个依赖关系在某些时候将不可避免的失败!
服务雪崩多个微服务之间调用的时候，假设微服务A调用微服务B和微服务C,微服务B和微服务C又调用其他的微服务,这就是所谓的“扇出"、如果扇出的链路上某个微服务的调用响应时间过长或者不可用，对微服务A的调用就会占用越来越多的系统资源，进而引|起系统崩溃，所谓的“雪崩效应"。

​	对于高流量的应用来说，单一-的后端依赖可能会导致所有服务器上的所有资源都在几秒中内饱和。比失败更糟糕的是，这些应用程序还可能导致服务之间的延迟增加，备份队列，线程和其他系统资源紧张，导致整个系统发生更多的级联故障，这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败,不能取消整个应用程序或系统。
​	

​	我们需要.弃车保帅



**什么是Hystrix**

​	Hystrix是一个用于处理分布式系统的延迟和容错的开源库, 在分布式系统里，许多依赖不可避免的会调用失败，比如超时，异常等, Hystrix能够保证在一个依赖出问题的情况下， 不会导致整体服务失败,避免级联故障,以提高分布式系统的弹性。

​	“断路器”本身是一种开关装置， 当某个服务单元发生故障之后，通过断路器的故障监控(类似熔断保险丝)，**向调用方返回一个服务预期的，可处理的备选响应(FallBack) ，而不是长时间的等待或者抛出调用方法无法处理的异常,这样就可以保证了服务调用方的线程不会被长时间，**不必要的占用，从而避免了故障在分布式系统中的蔓延，乃至雪崩



**能干嘛**

* 服务降级

* 服务熔断

* 服务限流

* 接近实时的监控

* .... 

  

  **官网资料**
  https://github.com/Netflix/Hystrix/wiki



#### **服务熔断**



**是什么**

​	熔断机制是对应雪崩效应的一-种微服务链路保护机制。
​	

​	当扇出链路的某个微服务不可用或者响应时间太长时，会进行服务的降级,进而熔断该节点微服务的调用，快速返回错误的响应信息。当检测到该节点微服务调用响应正常后恢复调用链路。在SpringCloud框架里熔断机制通过Hystrix实现。Hystrix会监控微服务间调用的状况， 当失败的调用到一定阈值，缺省是5秒内20次调用失败就会启动熔断机制。熔断机制的注解是@HystrixCommand.



#### Zuul路由网关

**概述**
**什么是Zuul?**

​	Zuul包含了对请求的路由和过滤两个最主要的功能:

​	其中路由功能负责将外部请求转发到具体的微服务实例上，是实现外部访问统一-入口的基础， 而过滤器功能则负责对请求的处理过程进行干预，是实现请求校验，服务聚合等功能的基础。Zuul和Eureka进行整合， 将ZuuI自身注册为Eureka服务治理下的应用，同时从Eureka中获得 其他微服务的消息，也即以后的访问微服务都是通过Zuul跳转后获得。

​	注意: Zuu|服务最终还是会注册进Eureka

​	提供:代理+路由+过滤三大功能!

**Zuul能干嘛?**

* 路由

* 过滤

  

  官网文档: https://github.com/Netflix/zuul





#### SpringCloud config分布式配置

**概述**
**分布式系统面临的--配置文件的问题**

​	微服务意味着要将单体应用中的业务拆分成一个个子服务，每个服务的粒度相对较小，因此系统中会出现大量的服务，由于每个服务都需要必要的配置信息才能运行，所以-套集中式的， 动态的配置管理设施是必不可少的。SpringCloud提供了ConfigServer来解决这个问题，我们每一个微服务 自己带着一个application.yml, 那上百的的配置文件要修改起来，岂不是要发疯!



**什么是SpringCloud config分布式配置中心**

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200325224906.png)

​	Spring Cloud Config为微服务架构中的微服务提供集中化的外部配置支持，配置服务器为各个不同微服务应用的所有环节提供了一个中心化的外部配置。

​	Spring Cloud Config 分为服务端和客户端两部分;
​	

​	服务端也称为分布式配置中心，它是一 个独立的微服务应用，用来连接配置服务器并为客户端提供获取配置信加密，解密信息等访问接口。

​	客户端则是通过指定的配置中心来管理应用资源，以及与业务相关的配置内容，并在启动的时候从配置中心获取和加载配置信息。配置服务器默认采用git来存储配置信息，这样就有助于对环境配置进行版本管理。并且可以通过git客户端工具来方便的管理和访问配置内容。



**SpringCloud config分布式配置中心能干嘛**

* 集中管理配置文件

* 不同环境，不同配置，动态化的配置更新，分环境部署,比如/dev /test/ /prod /beta /release

* 运行期间动态调整配置, 不再需要在每个服务部署的机器上编写配置文件，服务会向配置中心统一 拉取配置自己的信息。

* 当配置发生变动时，服务不需要重启，即可感知到配置的变化，并应用新的配置

* 将配置信息以REST接口的形式暴露



**SpringCloud config分布式配置中心与github整合**
		由于Spring Cloud Config默认使用Git来存储配置文件(也有其他方式， 比如支持SVN和本地文件)，但是最推荐的还是Git，而且使用的是http / https访问的形式; .