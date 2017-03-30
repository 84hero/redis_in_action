# 脚本

从 Redis 2.6.0 版本开始，通过内置的 Lua 解释器，可以使用 EVAL 命令对 Lua 脚本进行求值。

```
EVAL script numkeys key [key ...] arg [arg ...]
```
script 参数是一段 Lua 5.1 脚本程序，它会被运行在 Redis 服务器上下文中，这段脚本不必(也不应该)定义为一个 Lua 函数。

numkeys 参数用于指定键名参数的个数。

键名参数 key [key ...] 从 EVAL 的第三个参数开始算起，表示在脚本中所用到的那些 Redis 键(key)，这些键名参数可以在 Lua 中通过全局变量 KEYS 数组，用 1 为基址的形式访问( KEYS[1] ， KEYS[2] ，以此类推)。

在命令的最后，那些不是键名参数的附加参数 arg [arg ...] ，可以在 Lua 中通过全局变量 ARGV 数组访问，访问的形式和 KEYS 变量类似( ARGV[1] 、 ARGV[2] ，诸如此类)。

上面这几段长长的说明可以用一个简单的例子来概括：

```
eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"

```

其中 "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 是被求值的 Lua 脚本，数字 2 指定了键名参数的数量， key1 和 key2 是键名参数，分别使用 KEYS[1] 和 KEYS[2] 访问，而最后的 first 和 second 则是附加参数，可以通过 ARGV[1] 和 ARGV[2] 访问它们。

在 Lua 脚本中，可以使用两个不同函数来执行 Redis 命令，它们分别是：

* redis.call()
* redis.pcall()

这两个函数的唯一区别在于它们使用不同的方式处理执行命令所产生的错误，在后面的『错误处理』部分会讲到这一点。

redis.call() 和 redis.pcall() 两个函数的参数可以是任何格式良好(well formed)的 Redis 命令：

```
eval "return redis.call('set','foo','bar')" 0
OK

```

需要注意的是，上面这段脚本的确实现了将键 foo 的值设为 bar 的目的，但是，它违反了 EVAL 命令的语义，因为脚本里使用的所有键都应该由 KEYS 数组来传递，就像这样：

```
eval "return redis.call('set',KEYS[1],'bar')" 1 foo
OK

```

要求使用正确的形式来传递键(key)是有原因的，因为不仅仅是 EVAL 这个命令，所有的 Redis 命令，在执行之前都会被分析，籍此来确定命令会对哪些键进行操作。

因此，对于 EVAL 命令来说，必须使用正确的形式来传递键，才能确保分析工作正确地执行。除此之外，使用正确的形式来传递键还有很多其他好处，它的一个特别重要的用途就是确保 Redis 集群可以将你的请求发送到正确的集群节点。(对 Redis 集群的工作还在进行当中，但是脚本功能被设计成可以与集群功能保持兼容。)不过，这条规矩并不是强制性的，从而使得用户有机会滥用(abuse) Redis 单实例配置(single instance configuration)，代价是这样写出的脚本不能被 Redis 集群所兼容。


## 更多脚本文档

[http://redisdoc.com/script/eval.html](http://redisdoc.com/script/eval.html)