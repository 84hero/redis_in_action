# 数据安全

---

### 防火墙设置

通过防火墙ACL限制网络请求对于Redis实例的访问连接

### 修改连接配置

* **IP地址**

修改redis的配置文件**redis.conf**，将服务器绑定IP设置为私有或者特定IP地址

```Redis
bind 127.0.0.1
或者
bind 192.168.10.200
```

* **端口号**

修改默认端口号

```Redis
port 6379
改成
port 7001
```

### 

### 验证功能

* ##### Auth验证

修改redis.conf配置requirepass项，开启Redis密码访问

* ##### 密码复杂度

由于Redis查询提供查询时速度非常快，无法避免暴力破解的困扰，所以需要设置一个足够复杂的密码，来延长暴力破解所需时间

### 

### 禁用特定命令

* **重命名**

对于比较危险的服务器命令，比如FLUSHDB，FLUSHALL等清空数据库的危险命令，建议进行重命名处理

```
修改redis.conf

rename-command FLUSHDB 7ac01af7cb91864c1f1d87cda38b5de9

将FLUSHDB命令重命名为7ac01af7cb91864c1f1d87cda38b5de
```

* **禁用命令**

还可以将命令直接禁用

```
实际上也是重命名

rename-command FLUSHDB ""

将FLUSHDB命令重命名为空字符串
```



