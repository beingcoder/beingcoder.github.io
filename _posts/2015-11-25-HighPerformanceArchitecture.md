---
layout: post
title: 高性能架构设计拾摘
comments: false
keywords: 设计,高性能架构
category: 设计
---
#空间换时间: 
		多级缓存，静态化(反向代理缓存,应用端的缓存(memcache),内存数据库)
		索引:哈希、B树、倒排、bitmap
#并行与分布式计算:
		1,数据分解,  Map/reduce(利用局部性的原理将海量数据计算的问题分而治之。)
		2,基于问题分解的, 多进程、多线程并行执行
#多维度的可用
		1,负载均衡、容灾、备份
		2,读写分离
		3,依赖关系,低耦合的，能异步则异步; 确认机制,重发考虑幂等性
#伸缩
		 拆分(业务的拆分,数据拆分) e.g. 主域名和图片域名分离,减少读取cookie对图片服务器的压力
		 无状态
#优化资源利用
		考虑流量的控制，防止因意外攻击或者瞬时并发量的冲击导致系统崩溃。
		原子操作与并发控制,保证并发控制一些常用高性能手段有，乐观锁、Latch、mutex、写时复制、CAS等；多版本的并发控制MVCC通常是保证一致性的重要手段
		基于逻辑的不同，采取不一样的策略,e.g.针对IO型的，可以采取基于事件驱动的异步非阻塞的方式，单线程方式可以减少线程的切换引起的开销，或者在多线程的情况下采取自旋spin的方式，减少对线程的切换(比如oracle latch设计)；对于计算型的，充分利用多线程进行操作。
		容错隔离, 自治模块,暂时的失败,需要进行请求重试的考虑
		资源释放,e.g. 在设计通信的架构时，往往需要考虑超时的控制。
		
#剖析架构:
		CDN:
		负载均衡、反向代理缓存,4层(LVS+Keepalived/Heartbeat),7层Nginx,HAProxy,squid
		会话控制:反向代理或者负载均衡支持session sticky 或者 session的集中式存储
		业务服务: DDD,参考高内聚、接口收敛的原则;对外协议以NIO的RPC方式得道高并发，netty/mina
		数据库切分: Shard,   vertical/horizon/ master&slave
		HA:Heartbeat、keepalived,zookeeper
		消息Message:kafka/rabbitMQ,总体来讲，RabbitMQ用在实时的对可靠性要求比较高的消息传递上。kafka主要用于处理活跃的流式数据,大数据量的数据处理上
		Cache系统:redis比,memcache
		Buffer系统: producer/consumer,     blocking queue,  disruptor,  simple single thread batch.(batch size/fetch size on jdbc)
		搜索:lucene
		日志收集:
		数据同步:
		数据分析:
		实时计算:
		实时推送: comet
#管理与部署配置
		统一的配置库,部署平台
		监控、统计
