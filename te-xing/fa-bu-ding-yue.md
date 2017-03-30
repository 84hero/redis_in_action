# 发布订阅

SUBSCRIBE 、 UNSUBSCRIBE 和 PUBLISH 三个命令实现了发布与订阅信息泛型（Publish/Subscribe messaging paradigm）， 在这个实现中， 发送者（发送信息的客户端）不是将信息直接发送给特定的接收者（接收信息的客户端）， 而是将信息发送给频道（channel）， 然后由频道将信息转发给所有对这个频道感兴趣的订阅者。

发送者无须知道任何关于订阅者的信息， 而订阅者也无须知道是那个客户端给它发送信息， 它只要关注自己感兴趣的频道即可。

对发布者和订阅者进行解构（decoupling）， 可以极大地提高系统的扩展性（scalability）， 并得到一个更动态的网络拓扑（network topology）。

比如说， 要订阅频道 foo 和 bar ， 客户端可以使用频道名字作为参数来调用 SUBSCRIBE 命令：
```
redis> SUBSCRIBE foo bar
```
当有客户端发送信息到这些频道时， Redis 会将传入的信息推送到所有订阅这些频道的客户端里面。

正在订阅频道的客户端不应该发送除 SUBSCRIBE 和 UNSUBSCRIBE 之外的其他命令。 其中， SUBSCRIBE 可以用于订阅更多频道， 而 UNSUBSCRIBE 则可以用于退订已订阅的一个或多个频道。

SUBSCRIBE 和 UNSUBSCRIBE 的执行结果会以信息的形式返回， 客户端可以通过分析所接收信息的第一个元素， 从而判断所收到的内容是一条真正的信息， 还是 SUBSCRIBE 或 UNSUBSCRIBE 命令的操作结果。