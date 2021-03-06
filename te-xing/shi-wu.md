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

EXEC 命令的回复是一个数组， 数组中的每个元素都是执行事务中的命令所产生的回复。 其中， 回复元素的先后顺序和命令发送的先后顺序一致。

当客户端处于事务状态时， 所有传入的命令都会返回一个内容为 QUEUED 的状态回复（status reply）， 这些被入队的命令将在 EXEC 命令被调用时执行。

## 事务中的错误

使用事务时可能会遇上以下两种错误：

* 事务在执行 EXEC 之前，入队的命令可能会出错。比如说，命令可能会产生语法错误（参数数量错误，参数名错误，等等），或者其他更严重的错误，比如内存不足（如果服务器使用 maxmemory 设置了最大内存限制的话）。
* 命令可能在 EXEC 调用之后失败。举个例子，事务中的命令可能处理了错误类型的键，比如将列表命令用在了字符串键上面，诸如此类。

对于发生在 EXEC 执行之前的错误，客户端以前的做法是检查命令入队所得的返回值：如果命令入队时返回 QUEUED ，那么入队成功；否则，就是入队失败。如果有命令在入队时失败，那么大部分客户端都会停止并取消这个事务。

不过，从 Redis 2.6.5 开始，服务器会对命令入队失败的情况进行记录，并在客户端调用 EXEC 命令时，拒绝执行并自动放弃这个事务。

在 Redis 2.6.5 以前， Redis 只执行事务中那些入队成功的命令，而忽略那些入队失败的命令。 而新的处理方式则使得在流水线（pipeline）中包含事务变得简单，因为发送事务和读取事务的回复都只需要和服务器进行一次通讯。

至于那些在 EXEC 命令执行之后所产生的错误， 并没有对它们进行特别处理： 即使事务中有某个/某些命令在执行时产生了错误， 事务中的其他命令仍然会继续执行。

从协议的角度来看这个问题，会更容易理解一些。 以下例子中， LPOP 命令的执行将出错， 尽管调用它的语法是正确的：

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.

MULTI
+OK

SET a 3
abc

+QUEUED
LPOP a

+QUEUED
EXEC

*2
+OK
-ERR Operation against a key holding the wrong kind of value
```

[EXEC](http://redisdoc.com/transaction/exec.html#exec)返回两条批量回复（bulk reply）： 第一条是`OK`，而第二条是`-ERR`。 至于怎样用合适的方法来表示事务中的错误， 则是由客户端自己决定的。

最重要的是记住这样一条， 即使事务中有某条/某些命令执行失败了， 事务队列中的其他命令仍然会继续执行 —— Redis 不会停止执行事务中的命令。

以下例子展示的是另一种情况， 当命令在入队时产生错误， 错误会立即被返回给客户端：

```
MULTI
+OK

INCR a b c
-ERR wrong number of arguments for 'incr' command

```
因为调用 INCR 命令的参数格式不正确， 所以这个 INCR 命令入队失败。


