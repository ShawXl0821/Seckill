# Seckill  
高并发秒杀商城优化  
将商品和库存数据同步到redis中，所有的抢购操作都在redis中进行处理，通过Redis预减少库存减少数据库访问  
通过UUID生成唯一id作为Token，再将Token作为key、用户信息作为value模拟session存储到Redis，同时将Token存储到Cookie，保存登录状态  
使用消息队列 (RabbitMQ) 实现异步下单  
自定义全局异常拦截器：通过拦截所有异常，对各种异常进行相应的处理，当遇到异常就逐层上抛到专门负责异常处理的地方处理  
使用Guava提供的RateLimiter来实现限流，通过调整生成Token的速率来限制用户频繁访问秒杀页面  
使用JMeter完成压力测试，目前1000个线程循环10次同时访问，QPS能达到2641/s  
