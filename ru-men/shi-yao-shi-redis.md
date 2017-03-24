Redis通常被称为_数据结构_服务器。这意味着Redis通过一组命令提供对可变数据结构的访问，这些命令使用具有TCP套接字和简单协议的_服务器 - 客户端_模型发送。所以不同的进程可以以共享的方式查询和修改相同的数据结构。

Redis中实现的数据结构有一些特殊属性：

* Redis最终将它们存储在磁盘上，即使它们始终在服务器内存中读取、修改。这意味着Redis很快，但也是非易失性的。
* 数据结构的实现强调内存效率，因此与使用高级编程语言建模的相同数据结构相比，Redis内部的数据结构可能会使用更少的内存。
* Redis提供了许多在数据库中自然找到的功能，如复制，可调节级别的耐用性，集群，高可用性。

另一个很好的例子是将Redis视为一个更复杂的memcached版本，其中的操作不仅仅是SET和GET，而是使用复杂数据类型（如列表，集合，有序数据结构等）的操作。

如果你想了解更多，这是一个选定的起点列表：

* Redis数据类型简介
  [http://redis.io/topics/data-types-intro](http://redis.io/topics/data-types-intro)
* 直接在浏览器中试用Redis。
  [http://try.redis.io](http://try.redis.io/)
* Redis命令的完整列表。
  [http://redis.io/commands](http://redis.io/commands)
* Redis官方文档中还有更多的内容。
  [http://redis.io/documentation](http://redis.io/documentation)





Redis是一个开源（BSD许可），内存**数据结构存储**，用作**数据库**，**缓存**和**消息代理**。它支持数据结构，例如[字符串](https://redis.io/topics/data-types-intro#strings)\(string\)，[散列](https://redis.io/topics/data-types-intro#hashes)\(hashes\)，[列表](https://redis.io/topics/data-types-intro#lists)\(lists\)，[集合](https://redis.io/topics/data-types-intro#sets)\(sets\)，具有范围查询的[排序集](https://redis.io/topics/data-types-intro#sorted-sets)\(sorted sets\)，[位图](https://redis.io/topics/data-types-intro#bitmaps)\(bitmaps\)，[超文本](https://redis.io/topics/data-types-intro#hyperloglogs)\(HyperLogLogs\)和具有半径查询的[地理空间索引](https://redis.io/commands/geoadd)\(Geo\)。Redis内置[复制](https://redis.io/topics/replication)，[Lua脚本](https://redis.io/commands/eval)，[LRU驱逐](https://redis.io/topics/lru-cache)，[事务处理](https://redis.io/topics/transactions)和不同级别的[磁盘持久性](https://redis.io/topics/persistence)，

您可以对这些类型运行**原子操作**，例如[附加到字符串](https://redis.io/commands/append);[在哈希中增加值](https://redis.io/commands/hincrby);[将元素推送到列表中](https://redis.io/commands/lpush);[计算集交集](https://redis.io/commands/sinter)，[联合](https://redis.io/commands/sunion)与[差异](https://redis.io/commands/sdiff);或者[在排序集中获得最高排名的成员](https://redis.io/commands/zrangebyscore)。

为了实现其出色的性能，Redis使用**内存中的数据集**。根据您的用例，您可以通过将数据集一次性[转储到磁盘](https://redis.io/topics/persistence#snapshotting)\(**snapshotting**\)，或通过[将每个命令附加到日志](https://redis.io/topics/persistence#append-only-file)\(**append-only-file**\)来持久化。如果您只需要功能丰富的网络内存缓存，则可以选择禁用持久性。

Redis还支持简单到设置的[主从异步复制](https://redis.io/topics/replication)，非常快速的非阻塞第一次同步，自动重新连接，在网络分割上部分重新同步。

其他功能包括：

* [交易](https://redis.io/topics/transactions)
* [Pub / Sub](https://redis.io/topics/pubsub)
* [Lua脚本](https://redis.io/commands/eval)
* [钥匙具有有限的生存时间](https://redis.io/commands/expire)
* [LRU驱逐钥匙](https://redis.io/topics/lru-cache)
* [自动故障切换](https://redis.io/topics/sentinel)

您可以使用[大多数编程语言的](https://redis.io/clients)Redis。

Redis以**ANSI C**编写，适用于大多数POSIX系统，如Linux，\* BSD，OS X，无需外部依赖。Linux和OS X是Redis开发和测试的两个操作系统，我们**建议您使用Linux进行部署**。Redis可能在Solaris系统（如SmartOS）中工作，但支持是_尽力而为_。没有Windows平台的官方支持，但是微软开发并维护了RedisWin-64端。

