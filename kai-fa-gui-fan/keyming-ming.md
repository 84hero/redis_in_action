# 键命名

---

#### **不要太长**

> 虽然 Redis 的Key支持 2 ^ 31 字节长度，但是 Key 长度也消耗内存，在数据中查找这类键值的计算成本很高，所以不推荐使用很长的 Key 名称。
>
> ```
> user:1000:password
> ```

#### **不要太短**

> 这似乎跟前面的观点相矛盾，其实不然，由于 Redis 经常用于数据库场景，所以对于 Key 命名时，建议尽量提高 Key 用途的可读性，避免使用 “u:1000:pwd” 来代替 ”user:1000:password“ 。
>
> ```
> user:1000:password
> ```

### 

#### **推荐格式**

推荐使用 object\_type:id:field 这种格式

* 关键字之间以:分号进行分隔，部分 Redis 的 GUI 管理工具，会根据键的 : 分号做分层显示
* 名词、动作使用\_下划线连接

#### 

#### **加前缀**

多个独立应用共同使用一个 Redis 数据库实例的时候，为避免键值冲突、覆盖，建议每个应用使用独立的 KEY 前缀

#### 

#### **使用不同数据库Id**

与加前缀一样，不同应用连接同一个Redis实例时，为避免避免键值冲突、覆盖等情况，建议使用不同数据库ID

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



