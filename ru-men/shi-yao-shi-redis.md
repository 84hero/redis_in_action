Redis是一个开源的**内存数据结构存储**，用作**数据库**，**缓存**和**消息代理**。它支持丰富的数据结构，例如[字符串](https://redis.io/topics/data-types-intro#strings)\(string\)，[散列](https://redis.io/topics/data-types-intro#hashes)\(hashes\)，[列表](https://redis.io/topics/data-types-intro#lists)\(lists\)，[集合](https://redis.io/topics/data-types-intro#sets)\(sets\)，具有范围查询的[排序集](https://redis.io/topics/data-types-intro#sorted-sets)\(sorted sets\)，[位图](https://redis.io/topics/data-types-intro#bitmaps)\(bitmaps\)，[超文本](https://redis.io/topics/data-types-intro#hyperloglogs)\(HyperLogLogs\)和具有半径查询的[地理空间索引](https://redis.io/commands/geoadd)\(Geo\)。

Redis内置**主从复制**，[Lua脚本](https://redis.io/commands/eval)，[LRU驱逐](https://redis.io/topics/lru-cache)，[事务处理](https://redis.io/topics/transactions)和不同级别的[磁盘持久性](https://redis.io/topics/persistence)，

您可以对这些类型运行**原子操作**，例如**附加到字符串，**在**哈希中增加值，**将**元素推送到列表中，**计算集**交集、唯一、差异，**在**排序集中获得最高排名的成员**。

为了实现其出色的性能，Redis使用**内存中的数据集**。根据应用场景，可以通过将数据集一次性[转储到磁盘](https://redis.io/topics/persistence#snapshotting)\(**snapshotting**\)，或通过[将每个命令附加到日志](https://redis.io/topics/persistence#append-only-file)\(**append-only-file**\)来持久化。如果您只需要功能丰富的网络内存缓存，则可以选择禁用持久性。

Redis还支持简单到设置的[主从异步复制](https://redis.io/topics/replication)，非常快速的非阻塞第一次同步，在网络断开后，自动重新连接，并进行增量同步。

其他功能包括：

* [交易](https://redis.io/topics/transactions)
* [Pub / Sub](https://redis.io/topics/pubsub)
* [Lua脚本](https://redis.io/commands/eval)
* [钥匙具有有限的生存时间](https://redis.io/commands/expire)
* [LRU驱逐钥匙](https://redis.io/topics/lru-cache)
* [自动故障切换](https://redis.io/topics/sentinel)

您可以使用[大多数编程语言的](https://redis.io/clients)Redis。

Redis以**ANSI C**编写，适用于大多数POSIX系统，如Linux，\* BSD，OS X，无需外部依赖。Linux和OS X是Redis开发和测试的两个操作系统，我们**建议您使用Linux进行部署**。Redis可能在Solaris系统（如SmartOS）中工作，但支持是_尽力而为_。没有Windows平台的官方支持，但是微软开发并维护了RedisWin-64端。

如果你想了解更多，这是一个选定的起点列表：

* Redis数据类型简介
  [http://redis.io/topics/data-types-intro](http://redis.io/topics/data-types-intro)
* 直接在浏览器中试用Redis。
  [http://try.redis.io](http://try.redis.io/)
* Redis命令的完整列表。
  [http://redis.io/commands](http://redis.io/commands)
* Redis官方文档中还有更多的内容。
  [http://redis.io/documentation](http://redis.io/documentation)



