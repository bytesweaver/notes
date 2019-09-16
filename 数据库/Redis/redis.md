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

RDB和AOF

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

