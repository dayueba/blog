死锁这个概念最早出现于操作系统中，指的是两个进程持有对方想要的资源，但是又都不会释放这些资源，那么，就只能无止境的等待。

在 MySQL 中，我们说的死锁是事务相关的，所以，不同的存储引擎死锁的产生条件和解决办法也是不相同的。由于我们基本只使用InnoDB存储引擎，所以我们也只关注在 InnoDB 中，死锁是怎么出现的，又怎样去避免和解决它。

## 死锁产生的必要条件
操作系统中死锁产生的必要条件是以下四个
- 互斥条件：某个资源在同一时刻只能被一个进程占有
- 不可剥夺条件：一个进程占有的资源，在没有使用完之前，不能被其他的进程抢占
- 请求与保持条件：一个进程因请求资源阻塞时，对自己占据的资源不释放
- 循环等待条件：若干个进程之间形成了一种头尾相接的循环等待资源关系
我们可以相应得出InnoDB 中，死锁产生的比较条件
- 至少存在两个并发事务
- 每个事务都持有锁资源，但是都不会释放
- 每个事务都在申请新的锁资源
- 事务之间形成了锁资源的循环等待

所谓必要条件，就是要同时满足，那么，我们也可以得到启发：打破死锁的关系，只需要让以上的四个条件不同时满足就可以了。

数据库死锁的影响是非常大的，在生产环境中，几乎是致命的，随时可能会导致系统崩溃。例如，某张表由于各种原因出现了死锁，那么，所有涉及这张表的操作都会被阻塞，不论读写。这就会使很多操作在队列里排队，占用宝贵的数据库连接。最终会导致数据库连接耗尽、各种操作超时等等，致使系统各项指标异常，进而引发系统崩溃。

我们在工作中遇到的死锁，绝大多数都是 “唯一键”（列值唯一）引起的。

## 模拟死锁产生的情况
```sql
-- “会话 A” 关闭自动提交
mysql> SET AUTOCOMMIT = off;
Query OK, 0 rows affected (0.00 sec)

-- “会话 A” 开启事务
mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

-- “会话 A” 更新 id = 1 的记录（更新什么不重要，重要的是这个更新事务）
mysql> UPDATE worker SET type = 'B' WHERE id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

-- “会话 B” 关闭自动提交
mysql> SET AUTOCOMMIT = off;
Query OK, 0 rows affected (0.00 sec)

-- “会话 B” 开启事务
mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

-- “会话 B” 更新 id = 2 的记录（更新什么同样是不重要的）
mysql> UPDATE worker SET type = 'A' WHERE id = 2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

-- “会话 A” 更新 id = 2 的记录（你会发现事务卡住了）
mysql> UPDATE worker SET type = 'A' WHERE id = 2;

-- “会话 B” 更新 id = 1 的记录（可以看到，出现了死锁，MySQL 报错了，并让我们尝试重启事务）
mysql> UPDATE worker SET type = 'B' WHERE id = 1;
ERROR 1213 (40001): Deadlock found when trying to get lock; try restarting transaction

-- 回到 “会话 A”（注意，我们此时并不做任何操作），看看发生了什么
mysql> UPDATE worker SET type = 'A' WHERE id = 2;
Query OK, 1 row affected (42.99 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
最后，你会发现，“会话 A” 更新 id = 2 的记录执行成功了（注意看执行语句耗时，这是在等待锁），这是因为 “会话 B” 出现了死锁被 MySQL KILL 掉了。所以，MySQL 才会建议我们重新开启事务。

## 共享锁与排他锁
之前学习的全局锁，表锁以及行锁是按照锁粒度大小划分的。我们还可以从数据库管理的角度对锁进行划分成共享锁和排他锁。
### 共享锁
共享锁也叫读锁或 S 锁，共享锁锁定的资源可以被其他用户读取，但不能修改。在进行SELECT的时候，会将对象进行共享锁锁定，当数据读取完毕之后，就会释放共享锁，这样就可以保证数据在读取时不被修改。
```sql
LOCK TABLE product_comment READ; // 给表加共享锁
UNLOCK TABLE; // 解锁表的共享锁
SELECT * FROM product_comment WHERE user_id = 912178 LOCK IN SHARE MODE; // 给某一行加上共享锁
```

### 排他锁
排它锁也叫独占锁、写锁或 X 锁。排它锁锁定的数据只允许进行锁定操作的事务使用，其他事务无法对已锁定的数据进行查询或修改。
```sql
LOCK TABLE product_comment WRITE; // 给表加排他锁

```