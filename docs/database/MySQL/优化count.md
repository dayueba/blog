> 新建测试表
> ```
> CREATE TABLE `t6` (
>  `id` int(11) NOT NULL AUTO_INCREMENT,
>  `a` int(11) DEFAULT NULL,
>  `b` int(11) NOT NULL,
>  `c` int(11) DEFAULT NULL,
>  `d` int(11) DEFAULT NULL,
>  PRIMARY KEY (`id`),
>  KEY `idx_a` (`a`),
>  KEY `idx_b` (`b`)
>) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4;
>
>drop procedure if exists insert_t6; /* 如果存在存储过程insert_t6，则>>删除 */
>delimiter ;;
>create procedure insert_t6() /* 创建存储过程insert_t6 */
>begin
>declare i int; /* 声明变量i */
>set i=1; /* 设置i的初始值为1 */
>while(i<=10000)do /* 对满足i<=10000的值进行while循环 */
>insert into t6(a,b,c,d) values(i,i,i,i); /* 写入表t6中a、b两个字段，值都为i当前的值 */
>set i=i+1; /* 将i加1 */
>end while;
>end;;
>delimiter ; /* 创建批量写入10000条数据到表t6的存储过程insert_t6 */
>call insert_t6(); /* 运行存储过程insert_t6 */
>
>insert into t6(a,b,c,d) values (null,10001,10001,10001),(10002,10002,10002,10002);
>
>drop table if exists t7; /* 如果表t7存在则删除表t7 */
>create table t7 like t6; /* 创建表t7，表结构与t6一致 */
>alter table t7 engine =myisam; /* 把t7表改为MyISAM存储引擎 */
>insert into t7 select * from t6;  /* 把t6表的数据转到t7表 */
>
>CREATE TABLE `t8` (
>  `id` int(11) NOT NULL AUTO_INCREMENT,
>  `a` int(11) DEFAULT NULL,
>  `b` int(11) NOT NULL,
>  `c` int(11) DEFAULT NULL,
>  `d` int(11) DEFAULT NULL,
>  PRIMARY KEY (`id`)
>) ENGINE=InnoDB  CHARSET=utf8mb4;
> insert into t8 select * from t6;  /* 把t6表的数据转到t8表 */
>```
## 重新认识count

### count(a)和count(*)的区别

- 当 count() 统计某一列时，比如 count(a)，a 表示列名，是不统计 null 的。
- 而 count(*) 无论是否包含空值，都会统计。

如果希望知道结果集的行数，最好使用 count(*)。

### MyISAM引擎和InnoDB引擎count(*)的区别
对于 MyISAM 引擎，如果没有 where 子句，也没检索其它列，那么 count(*) 将会非常快。因为 MyISAM 引擎会把表的总行数存在磁盘上

首先我们看下对 t7 表（存储引擎为 MyISAM）不带 where 子句做 count(*) 的执行计划：

```
mysql> explain select count(*) from t7;
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+------------------------------+
| id | select_type | table | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra                        |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+------------------------------+
|  1 | SIMPLE      | NULL  | NULL       | NULL | NULL          | NULL | NULL    | NULL | NULL |     NULL | Select tables optimized away |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+------------------------------+
1 row in set, 1 warning (0.01 sec)
```
在 Extra 字段发现 “Select tables optimized away” 关键字，表示是从 MyISAM 引擎维护的准确行数上获取到的统计值。

而 InnoDB 并不会保留表中的行数，因为并发事务可能同时读取到不同的行数。所以执行 count(*) 时都是临时去计算的，会比 MyISAM 引擎慢很多。

我们看下对 t6 表（存储引擎为 InnoDB）执行 count(*) 的执行计划：
```
mysql> explain select count(*) from t6;
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | t6    | NULL       | index | NULL          | idx_b | 4       | NULL | 10107 |   100.00 | Using index |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
1 row in set, 1 warning (0.00 sec)
```

发现使用的是 b 字段的索引 idx_b，并且扫描行数是10109，表示会遍历 b 字段的索引树去计算表的总量。

对比 MyISAM 引擎和 InnoDB 引擎 count(*) 的区别，可以知道：

- MyISAM 会维护表的总行数，放在磁盘中，如果有 count(*) 的需求，直接返回这个数据
- 但是 InnoDB 就会去遍历普通索引树，计算表数据总量

在上面这个例子，InnoDB 表 t1 在执行 count(*) 时，为什么会走 b 字段的索引而不是走主键索引呢？下面我们分析下：

### MySQL5.7.18前后count(*)的区别
在 MySQL 5.7.18 之前，InnoDB 通过扫描聚簇索引来处理 count(*) 语句。

从 MySQL 5.7.18 开始，通过遍历最小的可用二级索引来处理 count(*) 语句。如果不存在二级索引，则扫描聚簇索引。但是，如果索引记录不完全在缓存池中的话，处理 count(*) 也是比较久的。

新版本为什么会使用二级索引来处理 count(*) 语句呢？

原因是 InnoDB 二级索引树的叶子节点上存放的是主键，而主键索引树的叶子节点上存放的是整行数据，所以二级索引树比主键索引树小。因此优化器基于成本的考虑，优先选择的是二级索引。所以 count(主键) 其实没 count (*) 快。

### count(1)比count(*)快吗？
在前面我们知道 count(*) 无论是否包含空值，所有结果都会统计。

而 count(1)中的 1 是恒真表达式，因此也会统计所有结果。

所以 count(1) 和 count(*) 统计结果没差别。

我们来对比 count(1) 和 count(* ) 的执行计划：

```
mysql> explain select count(*) from t6;
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | t6    | NULL       | index | NULL          | idx_b | 4       | NULL | 10107 |   100.00 | Using index |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
1 row in set, 1 warning (0.00 sec)

mysql> explain select count(1) from t6;
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | t6    | NULL       | index | NULL          | idx_b | 4       | NULL | 10107 |   100.00 | Using index |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
1 row in set, 1 warning (0.00 sec)
```
执行计划一样，所以 count(1) 并不比 count(*) 快。

## 如何优化count()

### show table status

有时，我们只需要知道某张表的大概数据量，这种情况就可以使用 show table status，具体用法如下：

```
mysql> show table status like 't6'\G;
*************************** 1. row ***************************
           Name: t6
         Engine: InnoDB
        Version: 10
     Row_format: Dynamic
           Rows: 10107
 Avg_row_length: 45
    Data_length: 458752
Max_data_length: 0
   Index_length: 344064
      Data_free: 0
 Auto_increment: 10006
    Create_time: 2020-11-02 01:43:21
    Update_time: 2020-11-02 01:43:46
     Check_time: NULL
      Collation: utf8mb4_general_ci
       Checksum: NULL
 Create_options: 
        Comment: 
1 row in set (0.00 sec)
```

Rows 这列就表示这张表的行数。这种方式获取 InnoDB 表的行数非常快。

但是，**这个值是个估算值，可能与实际值相差 40% 到 50%**。（对于 Rows 这个字段更详细的解释，可以参考官方手册：https://dev.mysql.com/doc/refman/5.7/en/show-table-status.html ）

所以，如果需要比较精确的表记录总数，此方法就行不通了。

### 用Redis做计数器
在有些业务场景，对于某一张表，count() 可能会频繁用到，直接执行 count(*) 可能会比较慢，并且影响数据库性能；使用 show table status 又不准确，此时可以考虑结合 Redis 做计数器。用法大致如下：
1. 初始化时记录准确的行数
2. 在mysql中插入或者删除的时候，修改redis中的值
3. 获取数据时直接从redis中获取 

通过 Redis 计数的方式，获取表的数据量比 show table status 准确，并且速度也比较快。

但是这种方法还是有缺点的。试想，在表 t1 写入数据到 Redis ，再到把 t1_count 加 1，总会存在一个时间差，如果这中间另外一个 session 去读取 Redis 中 t1_count 的值，此时 t1_count 的值没增加，但是表的实际数据行已经增加了，是不是结果就不准确了呢？我们在看下有没有更好的办法？

### 增加计数表
既然可以把数据放到redis中，那么也可以放到mysql中。

我们用 MySQL 中一张 InnoDB 表来代替。而数据写入操作和计数操作都放在一个事务中，就可以避免数据存放在redis中由于时间差出现计数不准确的情况。

## 问题
我们如果按照下面这条 SQL 统计表的总数据量，得到的值会准确吗？

```
select count(*) from t6 force index (idx_a);
```
注意，a 字段存在 null。

下面我们来实际执行一下
```
mysql> select count(*) from t6 force index (idx_a);
+----------+
| count(*) |
+----------+
|    10002 |
+----------+
1 row in set (0.00 sec)

mysql> select count(*) from t6;
+----------+
| count(*) |
+----------+
|    10002 |
+----------+
1 row in set (0.01 sec)
```
我们可以发现值是一样的，所以证明利用count(*)统计数据时，和使用哪个索引无关。

最后再看下explain执行计划
```
mysql> explain select count(*) from t6 force index (idx_a);
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | t6    | NULL       | index | NULL          | idx_a | 5       | NULL | 10107 |   100.00 | Using index |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
1 row in set, 1 warning (0.00 sec)

mysql> explain select count(*) from t6;
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key   | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | t6    | NULL       | index | NULL          | idx_b | 4       | NULL | 10107 |   100.00 | Using index |
+----+-------------+-------+------------+-------+---------------+-------+---------+------+-------+----------+-------------+
1 row in set, 1 warning (0.00 sec)
```