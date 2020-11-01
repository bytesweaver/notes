## 索引

：b-tree， hash， gist, gin, sp-gist

注意事项：

1. 正常创建索引时会阻塞除查询以外的其他操作
2. 使用并行concurrently选项后， 可以允许同时对表DML操作，对于频繁DML的表，创建索引的时间非常长
3. 某些索引不记录WAL