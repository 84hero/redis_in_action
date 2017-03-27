# ![](/assets/p1432653421.74.png)什么Redis?

> **Redis**是一个开源的**内存数据结构存储**，用作**数据库**，**缓存**和**消息代理**。
>
> 如果你接触过**Memcached，那么你**可以视**Redis**为一个更复杂的**Memcached**版本。它的操作不仅仅是**SET**和**GET**，而是使用复杂数据类型的操作。
>
> 它支持丰富的数据结构，例如[字符串](https://redis.io/topics/data-types-intro#strings)\(string\)，[散列](https://redis.io/topics/data-types-intro#hashes)\(hashes\)，[列表](https://redis.io/topics/data-types-intro#lists)\(lists\)，[集合](https://redis.io/topics/data-types-intro#sets)\(sets\)，具有范围查询的[排序集](https://redis.io/topics/data-types-intro#sorted-sets)\(sorted sets\)，[位图](https://redis.io/topics/data-types-intro#bitmaps)\(bitmaps\)，[超文本](https://redis.io/topics/data-types-intro#hyperloglogs)\(HyperLogLogs\)和具有半径查询的[地理空间索引](https://redis.io/commands/geoadd)\(Geo\)。
>
> Redis内置**主从复制**，[Lua脚本](https://redis.io/commands/eval)，[LRU驱逐](https://redis.io/topics/lru-cache)，[事务处理](https://redis.io/topics/transactions)和不同级别的[磁盘持久性](https://redis.io/topics/persistence)，
>
> 您可以对这些类型运行**原子操作**，例如**附加到字符串，**在**哈希中增加值，**将**元素推送到列表中，**计算集**交集、唯一、差异，**在**排序集中获得最高排名的成员**。
>
> 为了实现其出色的性能，Redis使用**内存中的数据集**。根据应用场景，可以通过将数据集一次性[转储到磁盘](https://redis.io/topics/persistence#snapshotting)\(**snapshotting**\)，或通过[将每个命令附加到日志](https://redis.io/topics/persistence#append-only-file)\(**append-only-file**\)来持久化。如果您只需要功能丰富的网络内存缓存，则可以选择禁用持久性。
>
> Redis还支持[主从异步复制](http://redis.io/topics/replication)，并且配置起来很简单，首次同步就能无阻塞、快速完成，在网络断开的时候还支持部分再同步的自动重连。
>
> 其他功能包括：
>
> * [事物](https://redis.io/topics/transactions)
> * [发布/](https://redis.io/topics/pubsub)订阅[ ](https://redis.io/topics/pubsub)
> * [Lua脚本](https://redis.io/commands/eval)
> * [KEY具有有限的生存时间](https://redis.io/commands/expire)
> * [LRU驱逐KEY](https://redis.io/topics/lru-cache)
> * [自动故障切换](https://redis.io/topics/sentinel)
>
> 您可以使用[大多数编程语言的](https://redis.io/clients)Redis。
>
> Redis以**ANSI C**编写，适用于大多数POSIX系统，如Linux，\* BSD，OS X，无需外部依赖。Linux和OS X是Redis开发和测试的两个操作系统，我们**建议您使用Linux进行部署**。Redis可能在Solaris系统（如SmartOS）中工作，但支持是_尽力而为_。没有Windows平台的官方支持，但是微软开发并维护了RedisWin-64端。

如果你想了解更多，这是一个选定的起点列表：

* Redis数据类型简介
  [http://redis.io/topics/data-types-intro](http://redis.io/topics/data-types-intro)
* 直接在浏览器中试用Redis。
  [http://try.redis.io](http://try.redis.io/)
* Redis命令的完整列表。
  [http://redis.io/commands](http://redis.io/commands)
* Redis官方文档中还有更多的内容。
  [http://redis.io/documentation](http://redis.io/documentation)

## Redis作者

> Redis作者[**Salvatore Sanfilippo**](http://invece.org/)，一名意大利程序员，大家更习惯称呼他[Antirez](http://antirez.com/)。
>
> Redis其实只是他的一个副业，以下链接为 Antirez 在 Redis 诞生六周年之际，特意撰写的一篇博文分享。
>
> [如何看待个人副业项目（side project）与主业项目（main project）之间的关系](http://www.jianshu.com/p/c5a28323d043)。

# 谁在用Redis?

使用Redis的知名公司名单

> * [推特](http://www.infoq.com/presentations/Real-Time-Delivery-Twitter)
> * [GitHub](https://github.com/blog/530-how-we-made-github-fast)
> * [微博](http://www.xdata.me/?p=353)
> * [Pinterest](http://engineering.pinterest.com/post/55272557617/building-a-follower-model-from-scratch)
> * [Snapchat](https://twitter.com/robustcloud/status/448503100056535040)
> * [Craigslist](http://blog.zawodny.com/2011/02/26/redis-sharding-at-craigslist/)
> * [掘客](http://nosql.mypopescu.com/post/3342598062/redis-at-digg-story-view-counts)
> * [StackOverflow](http://meta.stackoverflow.com/questions/69164/does-stackoverflow-use-caching-and-if-so-how/69172)
> * [Flickr](http://code.flickr.com/blog/2011/10/11/talk-real-time-updates-on-the-cheap-for-fun-and-profit/)

还有更多**！**[techstacks.io](http://techstacks.io/)维护着[使用Redis的热门网站](http://techstacks.io/tech/redis)列表。



