# java学习路线

## 第一轮：单体应用，快速上手项目

项目比较简单。不要钻牛角尖，注重熟练度，一定要多从零开始搭建项目。

**Java基础**：语法基础、流程调度、集合、多线程、设计模式、网络通讯...

**前端**：html、css、js、ajax...

**开发工具**：Eclipse、IDEA、VSCode...

​        tomcat、postman、git、maven、gradle、svn、jenkins...

​        各种博客、CSDN、github、语雀、石墨、ProcessOn...

**开发框架**：

​     **前端**：Vue、React、Angular

​     **后端框架**：SSM->Spring、SpringMVC->SpringBoot、Mybatis->MybatisPlus->JOOQ、Spring Data、JPA、Hibernate

​     **权限认证**：RBAC、Shiro、SpringSecurity->OAuth2.0

​     **定时任务**：Timer、Quartz、Elastic-job、XXL-job

## 第二轮：分布式架构

项目会开始逐渐的复杂起来，注重理解，注重横向对比。

**前端**：Nginx、lvs、CDN

**后端框架**：SpringCloud->Eureka、Fiegn+ribbon、Gateway、hytrix...

​        SpringCloudAlibaba->Nacos、Dubbo、RocketMQ、Sentinel、Seata...

**分布式协调框架**：Zookeeper、Redis、Mongodb、MQ（kafka、RabbitMQ 、RocketMQ）->SpringBoot-->SpringCloudStream

**数据库**：分库分表：shardingSphere、MyCat

**分布式数据库产品**：NewSQL：PostGreSQL、VoltDB、TiDB...

**项目部署**：Docker、K8s

**大数据体系**：（用到了就学，注重理解）Hadoop(Hdfs+MapReduce)、Hive、Hbase、Spark、ES->ELK、Storm、Flink、Kafka Stream

## 第三轮：高并发性能调优

阶段目标：注重实战、运维开发一体化、多发现问题。注重交流，一定不要闷头学习。

**操作系统**：计算机基础、计算机网络、Linux系统（shell脚本）

**JVM**：底层原理：类加载、内存模型、锁、多线程、JVM参数调优->JVM问题排查（Arhtas、JVM Tools）->性能调优、数据结构和算法、网络编程->BIO\NIO\AIO Netty

**各种框架**：底层原理、高级特性->读源码->手写调优->贡献开源代码（文档）

**分布式理论**：CAP->数据一致性算法：paxos、zab、Raft；分布式事务；RPC远程调用->Netty；分布式存储->hdfs、fastdfs；分布式ID；缓存->缓存雪崩、缓存击穿、缓存穿透、缓存一致性...

**细化的解决方案**：

​     分布式日志：->Skywalking、kafka、ELK(FileBeat、LogStash、ElasticSearch、Kibana)、Prometheus、Grafana

​     开放时权限认证：->OAuth2.0、SSO、多端登录...

​     大数据计算（用到就学）：->用户画像、大数据风控->机器学习、深度学习

​     虚拟化：Docker、Swarm、k8s->云原生

**项目实战**：精准问题、精准分析

​     例如：电商秒杀、微信红包、千亿级日志搜索。

## 第四轮：架构思维，掌控全局

技术反哺业务，找准封口，引领潮流。阶段目标：业务精准、技术敏感、结构思维、影响力。

**业务体系设计**：

​     Serverless；中台战略；云原生架构

**保持技术敏感**：

​     Fintech;业务驱动、技术落地、开发管理->Dev Ops，迭代开发、敏捷开发、自助式运维体系...；3D打印

**培养自己的影响力**：

​     团队影响力->公司影响力->行业影响力