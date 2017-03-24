# 不要太长

---

虽然Redis的Key支持2 ^ 31字节长度，但是Key长度也消耗内存，在数据中查找这类键值的计算成本很高，司仪不推荐使用很长的Key名称。

# 不要太短

---

这似乎跟前面的观点相矛盾，其实不然，由于Redis经常用于数据库场景，所以对于Key命名时，建议尽量提高KEY用途的可读性，避免使用“u:1000:pwd”来代替”user:1000:password

# 推荐格式

---

推荐使用 **object-type:id:field** 这种格式

* 关键字之间以:分号进行分隔，部分GUI的Redis管理工具，会根据键的:分号做分层显示
* 名词、动作使用\_下划线连接

例如：

* 用户id为1000的密码

```Redis
user:1000:password
```

* 用户id为1000的用户信息

```Redis
user:1000:info
```

* 用户收到的信息

```Redis
user:1000:message_receive
```

* 用户发送信息

```
user:1000:message_to
```

* 用户Token集合

```
user_token
```

# 加前缀

---

多个独立应用共同使用一个Redis数据库实例的时候，为避免键值冲突、覆盖，建议每个应用使用独立的KEY前缀

例如：

```
open:user_token
server:user_token
```



