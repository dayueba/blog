## 意向锁

InnoDB 引擎实现了两种标准的行级锁
1. 共享行级锁，Shared Lock，简写为S Lock，可以理解为Read Lock（读锁）
2. 排他行级锁，Exclusive Lock，简写为X Lock，可以理解为Write Lock（写锁）

![](img/screenshot-20220115-114507.png)

两种行级锁的兼容性如上图所示，只有读锁和读锁之间不互斥

