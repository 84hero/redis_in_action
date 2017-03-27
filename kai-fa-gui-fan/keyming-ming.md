# 键命名

---

#### **不要太长**

> 虽然 Redis 的Key支持 2 ^ 31 字节长度，Redis 是个内存数据库，键越短你需要的空间就越少。理所当然，当数据库中拥有数百万或者数十亿键时，键名的长度将影响重大。在数据中查找这类键值的计算成本很高，所以不推荐使用很长的 Key 名称。
>
> * 建议
>
> ```
> user:1000:password
> ```

#### **不要太短**

> 这似乎跟前面的观点相矛盾，其实不然，由于 Redis 经常用于数据库场景，所以对于 Key 命名时，建议尽量提高 Key 的可读性及业务关联性。
> * 建议
>
> ```
> user:1000:password
> ```
> * 不建议
>
> ```
> u:1000:pwd
> ```



#### **推荐格式**

> 推荐使用 object\_type:id:field 这种格式
>
> * 关键字之间以:分号进行分隔，部分 Redis 的 GUI 管理工具，会根据键的 : 分号做分层显示
> * 名词、动作使用\_下划线连接

#### **加前缀**

>多个业务共同使用一个 Redis 数据库实例的时候，为避免键值冲突、覆盖，建议每个应用使用独立的 KEY 前缀
> ```
> user_token
> open:user_token
> server:user_token
> ```

#### Example：

> * 用户id为1000的密码
>
> ```Redis
> user:1000:password
> ```
>
> * 用户id为1000的用户信息
>
> ```Redis
> user:1000:info
> ```
>
> * 用户收到的信息
>
> ```Redis
> user:1000:message_receive
> ```
>
> * 用户发送信息
>
> ```
> user:1000:message_to
> ```
>
> * 用户Token集合
>
> ```
> user_token
>
> open:user_token
> server:user_token
> ```



