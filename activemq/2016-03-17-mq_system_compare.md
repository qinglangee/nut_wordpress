# mq 软件比较

[消息中间件的技术选型心得－RabbitMQ、ActiveMQ和ZeroMQ](http://www.oschina.net/question/991956_227911?sort=time)  
RabbitMQ、ActiveMQ和ZeroMQ都是极好的消息中间件，但是我们在项目中该选择哪个更适合呢？很多开发者面临这个烦恼。下面我会对这三个消息中间件做一个比较，看了后你们就心中有数了。

RabbitMQ是AMQP协议领先的一个实现，它实现了代理(Broker)架构，意味着消息在发送到客户端之前可以在中央节点上排队。此特性使得RabbitMQ易于使用和部署，适宜于很多场景如路由、负载均衡或消息持久化等，用消息队列只需几行代码即可搞定。但是，这使得它的可扩展性差，速度较慢，因为中央节点增加了延迟，消息封装后也比较大。


ZeroMQ是一个非常轻量级的消息系统，专门为高吞吐量/低延迟的场景开发，在金融界的应用中经常可以发现它。与RabbitMQ相比，ZeroMQ支持许多高级消息场景，但是你必须实现ZeroMQ框架中的各个块（比如Socket或Device等）。ZeroMQ非常灵活，但是你必须学习它的80页的手册（如果你要写一个分布式系统，一定要阅读它）。


ActiveMQ居于两者之间，类似于ZemoMQ，它可以部署于代理模式和P2P模式。类似于RabbitMQ，它易于实现高级场景，而且只需付出低消耗。它被誉为消息中间件的“瑞士军刀”。

要注意一点，*ActiveMQ的下一代产品为Apollo*。


最终，这三个产品：
1. 都有客户端API且支持多种编程语言；
2. 都有大量的文档；
3. 都提供了积极的支持。

[RocketMQ，队列选型](http://www.zmannotes.com/index.php/2016/01/17/rocketmq/)  
Q：单机broker性能？

A：RocketMQ > RabbitMQ > ActiveMQ。对于一般业务，性能不会是瓶颈，也不是选型的核心指标，没必要花费较多时间在上面。单机4000、5000的qps，足够了，不够建集群。