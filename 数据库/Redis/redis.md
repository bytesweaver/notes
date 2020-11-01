[命令参考](<http://redisdoc.com/hash/index.html#>)

[Redis Command Reference](http://redis.io/commands) 

 [Redis Documentation](http://redis.io/documentation) 

## Basic

redis 支持的数据结构

String:

hash, 

List

lis t基础上加了一个顺序属性。Zset中每个成员都有一个score关联，通过score来为集合中的成员从大到小排

## 分布式锁

[参考]（<https://www.cnblogs.com/linjiqin/p/8003838.html>）​ :star:

![1556493281120](..\image\1556493281120.png)

备注：这个作者的文章应该不错

## 自动过期

EXPIRE, PERSIST

## 事务

MULTI, EXEC, DISCARD, WATCH

## 持久化方式

### RDB和AOF

#### RDB

RDB:满足条件或者执行flushAll命令

dump文件放到redis启动文件，会自动扫描回复数据

使用场景：

适合大规模数据回复

对数据完整性不高

缺点：

需要一定的时间间隔

fork子进程会占用一定的内存空间

#### AOF

appendonly

默认不开启， 需要手动配置

如果AOF文件错误， redis无法启动，redis-check-aof工具进行修复

优点：每一次都修改，保证文件完整性

缺点：AOF远远大于RDB， 回复速度慢， AOF运行效率比较慢	

## Redis 和 Memcache比较

<https://blog.csdn.net/suifeng3051/article/details/23739295>

> 1.性能上：
>
> ​     性能上都很出色，具体到细节，由于Redis只使用单核，而Memcached可以使用多核，所以平均每一个核上Redis在存储小数据时比
>
> Memcached性能更高。而在100k以上的数据中，Memcached性能要高于Redis，虽然Redis最近也在存储大数据的性能上进行优化，但是比起 Memcached，还是稍有逊色。
>
> 2.内存空间和数据量大小：
>
> ​     MemCached可以修改最大内存，采用LRU算法。Redis增加了VM的特性，突破了物理内存的限制。
>
> 3.操作便利上：
>
> ​     MemCached数据结构单一，仅用来缓存数据，而Redis支持更加丰富的数据类型，也可以在服务器端直接对数据进行丰富的操作,这样可以减少网络IO次数和数据体积。 
>
> 4.可靠性上：
>
> ​     MemCached不支持数据持久化，断电或重启后数据消失，但其稳定性是有保证的。Redis支持数据持久化和数据恢复，允许单点故障，但是同时也会付出性能的代价。
>
> 5.应用场景：
>
> ​     Memcached：动态系统中减轻数据库负载，提升性能；做缓存，适合多读少写，大数据量的情况（如人人网大量查询用户信息、好友信息、文章信息等）。
>
> ​     Redis：适用于对读写效率要求都很高，数据处理业务复杂和对安全性要求较高的系统（如新浪微博的计数和微博发布部分系统，对数据安全性、读写要求都很高）

## 哨兵模式和集群模式

>  1、哨兵集群模式是基于主从模式的，所有主从的优点，哨兵模式同样具有。
>
>  2、主从可以切换，故障可以转移，系统可用性更好。
>
>  3、哨兵模式是主从模式的升级，系统更健壮，可用性更高。  

## spring-boot整合

jedis:采用直连，多线程不安全，避免不安全，使用jedis pool连接池， BIO

lettuce：采用netty，实例可以在多个线程中共享， 不存在线程不安全的情况， 可以减少线程数据

### jedis 为什么是非线程安全的

参考：https://www.jianshu.com/p/5e4a1f92c88f

jedis类中有RedisInputStream和RedisOutputStream两个属性，而发送命令和获取返回值都是使用这两个成员变量，显然，这很容易引发多线程问题

1. 共享socket引起的异常
2. 共享数据流引起的异常



> jedis本身不是多线程安全的，这并不是jedis的bug，而是jedis的设计与redis本身就是单线程相关，jedis实例抽象的是发送命令相关，一个jedis实例使用一个线程与使用100个线程去发送命令没有本质上的区别，所以没必要设置为线程安全的。但是如果需要用多线程方式访问redis服务器怎么做呢？那就使用多个jedis实例，每个线程对应一个jedis实例，而不是一个jedis实例多个线程共享。一个jedis关联一个Client，相当于一个客户端，Client继承了Connection，Connection维护了Socket连接，对于Socket这种昂贵的连接，一般都会做池化，jedis提供了JedisPool