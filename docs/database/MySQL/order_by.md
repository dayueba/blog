## order by 原理
### 排序原理
按照排序原理分，mysql中排序方式有两种
- 通过有序索引直接返回有序数据
- 通过 Filesort 进行的排序

**Q：如何确定某条排序的 SQL 所使用的排序方式？**

A：使用explain来查看sql的执行计划中的Extra字段
- Using index：则表示是通过有序索引直接返回有序数据。
- Using filesort，则表示该 SQL 是通过 filesort 进行的排序

### filesort
一般情况下，我们只能把数据加载到内存中，再用一些排序算法把数据在内存中排序。有时候查询的结果集太大以至于无法在内存中进行排序，此时就需要借助磁盘的空间来存放中间结果，在排序操作完成后再把排好的结果集返回给客户端。

**Q：filesort是在内存中还是磁盘中排序的？？**

A：内存排序还是磁盘排序取决于排序的数据大小和 sort_buffer_size 配置的大小。
- 如果 “排序的数据大小” < sort_buffer_size: 内存排序
- 如果 “排序的数据大小” > sort_buffer_size: 磁盘排序

```sql
mysql> show variables like 'sort_buffer_size';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| sort_buffer_size | 262144 |
+------------------+--------+
1 row in set (0.06 sec)
```

**Q: 怎么确定使用 Filesort 排序的 SQL 是在内存还是在磁盘中进行的排序操作**



## order by 优化

