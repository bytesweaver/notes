
```sql
-- 优化器评估查询成本
show status like 'Last_query_cost'
```
派生表 是从SELECT语句返回的虚拟表。派生表类似于临时表，但是在SELECT语句中使用派生表比临时表简单得多，因为它不需要创建临时表的步骤。术语:\*派生表\*和子查询通常可互换使用。当SELECT语句的FROM子句中使用独立子查询时，我们将其称为派生表

FROM 子句 中的 子 查询 是 派生 表” 这一 表述 是对 的， 但“ 派生 表 是 FROM 子句 中的 子 查询” 则 不对， 术语“ 派生 表” 在 SQL 中 含义 很 宽泛。



Spring 事务

https://www.ibm.com/developerworks/cn/education/opensource/os-cn-spring-trans/index.html



如何查找Mysql中查询慢的SQL语句

```
1，slow_query_log

这个参数设置为ON，可以捕获执行时间超过一定数值的SQL语句。

2，long_query_time

当SQL语句执行时间超过此数值时，就会被记录到日志中，建议设置为1或者更短。

3，slow_query_log_file

记录日志的文件名。
4，log_queries_not_using_indexes

这个参数设置为ON，可以捕获到所有未使用索引的SQL语句，尽管这个SQL语句有可能执行得挺快
```



如何查找慢查询：

mysql联合索引存储方式：

 ![](E:\notes\notes\数据库\mysql联合索引存储方式.png) 

## Mysql关联查询

### 什么是驱动表

驱动表定义：

1. 当连接查询没有where条件时，左连接查询时，前面的表是驱动表，后面的表是被驱动表，右连接查询时相反，内连接查询时，哪张表的数据较少，哪张表就是驱动表
2. 当连接查询有where条件时，带where条件的表是驱动表，否则是被驱动表

### 连接查询算法

##### Simple Nested-Loop Join Algorithms （简单嵌套循环连接算法）

```
for (row1 : 驱动表) {
    for (row2 : 被驱动表){
        if (conidtion == true){
            send client
        }
    }
}
```



##### Index Nested-Loop Join Algorithms （索引嵌套循环连接算法）

```
for (row1 : 驱动表) {
    索引在被驱动表中命中，不用再遍历被驱动表了
}
```



##### Block Nested-Loop Join Algorithm(基于块的连接嵌套循环算法)

块嵌套循环（BNL）嵌套算法使用对在外部循环中读取的行进行缓冲，以减少必须读取内部循环中的表的次数。例如，如果将10行读入缓冲区并将缓冲区传递到下一个内部循环，则可以将内部循环中读取的每一行与缓冲区中的所有10行进行比较。这将内部表必须读取的次数减少了一个数量级。

**优先级：**

第一种算法忽略，MySQL不会采用这种的，当我们对被驱动表创建了索引，那么MySQL一定使用的第二种算法，当我们没有创建索引或者对驱动表创建了索引，那么MySQL一定使用第三种算法

## Mysql Update语句执行过程

参考：https://www.jb51.net/article/183349.htm