### 与**Memcached对比**

|  | Memcached | Redis |
| :---: | :---: | :---: |
| **类型** | 内存数据库 | 内存数据库 |
| **多线程** | 支持 | 不支持 |
| **数据类型** | 单一键值 | 多种数据类型 |
| **持久化** | 不支持 | 支持 |
| **主从复制** | 不支持 | 支持 |
| **集群** | 不支持 | 支持 |

### 选择Memcached还是Redis？

在决定Memcached和Redis之间时，请考虑以下几个问题：

* 对象缓存是您的主要目标，例如数据库缓存？如果是这样，请使用**Memcached**。
* 您是否对尽可能简单的缓存模型感兴趣？如果是这样，请使用**Memcached**。
* 您是否计划运行大型缓存节点，并且需要利用多个内核的多线程性能？如果是这样，请使用**Memcached**。
* 您想要随着扩展水平扩展缓存的能力吗？如果是这样，请使用**Memcached**。
* 你的应用程序需要原子地增加或减少计数器吗？如果是，请使用**Redis**或**Memcached**。
* 您是否正在寻找更多高级数据类型，例如列表，散列和集合？如果是这样，请使用**Redis**。
* 在内存中排序和排序数据集是否可以帮助您，例如排行榜？如果是这样，请使用**Redis**。
* 是否发布和订阅（pub / sub）功能用于您的应用程序？如果是这样，请使用**Redis。**
* 您的密钥存储库的持久性是否重要？如果是这样，请使用**Redis**。

### 对比评测

* [Redis作者关于Redis与Memcached的对比](http://antirez.com/news/94)
* DB-Engines上的[Redis、Memcached、MongoDB系统属性对比](http://db-engines.com/en/system/Memcached%3BMongoDB%3BRedis)



