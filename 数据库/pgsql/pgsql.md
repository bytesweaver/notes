* where 和having的区别

`WHERE`在分组和聚集计算之前选取输入行（因此，它控制哪些行进入聚集计算）， 而`HAVING`在分组和聚集之后选取分组行。因此，`WHERE`子句不能包含聚集函数； 因为试图用聚集函数判断哪些行应输入给聚集运算是没有意义的。相反，`HAVING`子句总是包含聚集函数（严格说来，你可以写不使用聚集的`HAVING`子句， 但这样做很少有用。同样的条件用在`WHERE`阶段会更有效）

* left join, right join, innner join

left join(左联接) 返回包括左表中的所有记录和右表中联结字段相等的记录
right join(右联接) 返回包括右表中的所有记录和左表中联结字段相等的记录
inner join(等值连接) 只返回两个表中联结字段相等的行

* 执行计划

  表顺序扫描由于是立即可以获得第一行，所以启动时间一般都是0，而如果是排序操作，则需要处理完所有行后才能返回第一行，所以排序操作是需要启动时间的，下表列出了哪些操作是需要启动时间的，哪些操作不是需要的：

  执行计划运算类型		操作说明							是否有启动时间
  Seq Scan	   		扫描表							无启动时间
  Index Scan			索引扫描							无启动时间
  Bitmap Index Scan	索引扫描							有启动时间
  Bitmap Heap Scan	索引扫描							有启动时间
  Subquery Scan		子查询							无启动时间
  Tid Scan			ctid = …条件						无启动时间
  Function Scan		函数扫描							无启动时间
  Nested Loop			循环结合							无启动时间
  Merge Join			合并结合							有启动时间
  Hash Join			哈希结合							有启动时间
  Sort				排序，ORDER BY操作				有启动时间
  Hash				哈希运算							有启动时间
  Result				函数扫描，和具体的表无关			无启动时间
  Unique				DISTINCT，UNION操作				有启动时间
  Limit				LIMIT，OFFSET操作				有启动时间
  Aggregate			count, sum,avg, stddev集约函数	有启动时间
  Group				GROUP BY分组操作					有启动时间
  Append				UNION操作						无启动时间
  Materialize			子查询							有启动时间



* pg序列化

为了避免阻塞从同一个序列获取序号的并发事务，`nextval`操作从来不会被回滚。也就是说，一旦一个值被取出就视同被用掉并且不会被再次返回给调用者，即便调用该操作的外层事务后来中止或者调用查询后来没有使用取得的值也是这样。例如一个带有`ON CONFLICT`子句的`INSERT`会计算要被插入的元组，其中可能就包括调用`nextval`，然后才会检测到导致它转向`ON CONFLICT`规则的冲突。这种情况就会在已分配值的序列中留下未被使用的“空洞”。因此，PostgreSQL的序列对象***不能被用来得到“无间隙”的序列\***。

* pg日期

计算日期间隔

select age(timestamp '1994-05-13 00:13:42')

三种日期类型

select current_date,current_time, current_timestamp

计算时间间隔

select timestamp '2020-07-15 23:10:10' - timestamp '2020-08-16 22:10:5'

时间计算

select date '2020-07-15' + interval '20 hour'

* pgsql函数返回数据集

