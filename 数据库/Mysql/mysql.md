
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