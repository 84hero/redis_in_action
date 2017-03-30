# 事务

---

[MULTI](http://redisdoc.com/transaction/multi.html#multi)、[EXEC](http://redisdoc.com/transaction/exec.html#exec)、[DISCARD](http://redisdoc.com/transaction/discard.html#discard)和[WATCH](http://redisdoc.com/transaction/watch.html#watch)是 Redis 事务的基础。

事务可以一次执行多个命令， 并且带有以下两个重要的保证：

* 事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。

* 事务是一个原子操作：事务中的命令要么全部被执行，要么全部都不执行。

  [EXEC](http://redisdoc.com/transaction/exec.html#exec)命令负责触发并执行事务中的所有命令：

  * 如果客户端在使用
    [MULTI](http://redisdoc.com/transaction/multi.html#multi)
    开启了一个事务之后，却因为断线而没有成功执行
    [EXEC](http://redisdoc.com/transaction/exec.html#exec)
    ，那么事务中的所有命令都不会被执行。
  * 另一方面，如果客户端成功在开启事务之后执行
    [EXEC](http://redisdoc.com/transaction/exec.html#exec)
    ，那么事务中的所有命令都会被执行。

  当使用 AOF 方式做持久化的时候， Redis 会使用单个`write(2)`命令将事务写入到磁盘中。

  然而，如果 Redis 服务器因为某些原因被管理员杀死，或者遇上某种硬件故障，那么可能只有部分事务命令会被成功写入到磁盘中。

  如果 Redis 在重新启动时发现 AOF 文件出了这样的问题，那么它会退出，并汇报一个错误。

  使用`redis-check-aof`程序可以修复这一问题：它会移除 AOF 文件中不完整事务的信息，确保服务器可以顺利启动。

从 2.2 版本开始，Redis 还可以通过乐观锁（optimistic lock）实现 CAS （check-and-set）操作，具体信息请参考文档的后半部分。

## 用法

[MULTI](http://redisdoc.com/transaction/multi.html#multi)命令用于开启一个事务，它总是返回`OK`。

[MULTI](http://redisdoc.com/transaction/multi.html#multi)执行之后， 客户端可以继续向服务器发送任意多条命令， 这些命令不会立即被执行， 而是被放到一个队列中， 当[EXEC](http://redisdoc.com/transaction/exec.html#exec)命令被调用时， 所有队列中的命令才会被执行。

另一方面， 通过调用[DISCARD](http://redisdoc.com/transaction/discard.html#discard)， 客户端可以清空事务队列， 并放弃执行事务。

以下是一个事务例子， 它原子地增加了`foo`和`bar`两个键的值：

```
> MULTI
OK

> INCR foo
QUEUED

> INCR bar
QUEUED

> EXEC
1) (integer) 1
2) (integer) 1
```




