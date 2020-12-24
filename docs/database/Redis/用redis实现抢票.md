第三个问题是，我们能否用 Redis 中的 DECR 实现多用户抢票问题？

当然是可以的，在专栏文章中我使用了 WATCH+MULTI 的乐观锁方式，主要是讲解这种乐观锁的实现方式。我们也可以使用 Redis 中的 DECR 命令，对相应的 KEY 值进行减 1，操作是原子性的，然后我们判断下 DECR 之后的数值即可，当减 1 之后大于等于 0 证明抢票成功，否则小于 0 则说明抢票失败。

```
# 抢票模拟，使用 DECR 原子操作
import redis
import threading
# 创建连接池
pool = redis.ConnectionPool(host = '127.0.0.1', port=6379, db=0)
# 初始化 redis
r = redis.StrictRedis(connection_pool = pool)
 
# 设置 KEY
KEY="ticket_count"
# 模拟第 i 个用户进行抢购
def sell(i):
    # 使用 decr 对 KEY 减 1
    temp = r.decr(KEY)
    if temp >= 0:
        print('用户 {} 抢票成功，当前票数 {}'.format(i, temp))
    else:
        print('用户 {} 抢票失败，票卖完了'.format(i))
 
if __name__ == "__main__":
    # 初始化 5 张票
    r.set(KEY, 5)  
    # 设置 8 个人抢票
    for i in range(8):
        t = threading.Thread(target=sell, args=(i,))
        t.start()
```