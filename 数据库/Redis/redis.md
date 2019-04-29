[命令参考](<http://redisdoc.com/hash/index.html#>)

[Redis Command Reference](http://redis.io/commands) 

 [Redis Documentation](http://redis.io/documentation) 

## Basic

redis 支持的数据结构

String:

hash, 

List

list在Redis存储为有序的字符串序列，其实就是每个子元素都是string类型的双向链表。最大长度为2^32

Set

 是一个字符串序列，set 内部使用hash表保持唯一性。用来做交集、并集、补集方便

Zset

set基础上加了一个顺序属性。Zset中每个成员都有一个score关联，通过score来为集合中的成员从大到小排

## 分布式锁

[参考]（<https://www.cnblogs.com/linjiqin/p/8003838.html>）​ :star:

![1556493281120](..\image\1556493281120.png)

备注：这个作者的文章应该不错

## 自动过期

EXPIRE, PERSIST

## 事务

MULTI, EXEC, DISCARD, WATCH