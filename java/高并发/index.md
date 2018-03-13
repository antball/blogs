

大型网站技术架构：核心原理与案例分析
构建高性能Web站点




###负载均衡

* HTTP重定向实现负载均衡

* DNS负载均衡

* IP负载均衡

* 反向代理负载均衡


    http://blog.csdn.net/guchuanyun111/article/details/52056474

    http://aokunsang.iteye.com/blog/2053719

    https://www.cnblogs.com/zxf330301/p/5958269.html


### 分布式事务

https://www.cnblogs.com/taiyonghai/p/6094350.html
https://www.cnblogs.com/savorboard/p/distributed-system-transaction-consistency.html
https://segmentfault.com/a/1190000012762869
[阿里RocketMQ](https://www.cnblogs.com/antain/p/rocketmq.html)
[RocketMQ原理解析](http://blog.csdn.net/column/details/learningrocketmq.html?&page=1)
http://blog.csdn.net/chunlongyu/article/category/6638499
[什么是分布式系统中的幂等性](https://www.cnblogs.com/leechenxiang/p/6626629.html)

### 柔性事务
柔性事务是对分布式事务说的，说白了就是利用可以利用的业务弹性，打开脑洞让事务最终一致，分布式事务天然就不能一蹴而就，柔性事务是一种思想，
就是利用业务上对于事务过程中不一致的容忍度，找到让事务最终一致的方法，寻求一种技术能力和业务诉求平衡的办法。3
举个实际的例子，比如转账，
A账号的钱减少、B账号的钱增加，刚性事务是要求这两个增加和减少是同时发生的，柔性事务的思想则是先减少A的钱，然后再增加B的钱，分布式环境下，
难以保证同时增加和减少，但是只要保证A的钱减少之后，在B能接受的时间范围内，最终给B加上去，也就是最终一致，这就是柔性事务的思想。
单数据库事务完全遵循ACID规范，属于刚性事务，分布式事务要完全遵循ACID规范比较困难, 分布式事务属于柔性事务，满足BASE理论；

BASE描述： BA（Basic Availability 基本业务可用性）、S（Soft state 柔性状态）、E（Eventual consistency 最终一致性）；
柔性事务对ACID的支持：

1、原子性：严格遵循；
2、一致性：事务完成后的一致性严格遵循，事务中的一致性可适当放宽；
3、隔离性：并行事务间不可影响；事务中间结果可见性允许安全放宽；
4、持久性：严格遵循；为了可用性、性能的需要，
柔性事务降低了一致性(C)与隔离性(I) 的要求，即“基本可用，最终一致”；

柔性事务分为：两阶段型、补偿型、异步确保型、最大努力通知型；

1、两阶段型就是分布式事务两阶段提交，对应技术上的XA、JTA/JTS，这是分布式环境下事务处理的典型模式。
2、补偿型TCC型事务（Try/Confirm/Cancel）可以归为补偿型；TCC思路是:尽早释放锁；在Try成功的情况下，如果事务要回滚，
Cancel将作为一个补偿机制，回滚Try操作；TCC各操作事务本地化，且尽早提交 (放弃两阶段约束)；当全局事务要求回滚时，
通过另一个本地事务实现“补偿”行为；TCC是将资源层的两阶段提交协议转换到业务层，成为业务模型中的一部分；
3、异步确保型将一些同步阻塞的事务操作变为异步的操作，避免对数据库事务的争用；比如消息事务机制；
4、最大努力通知型通过通知服务器(消息通知)进行，允许失败，有补充机制；