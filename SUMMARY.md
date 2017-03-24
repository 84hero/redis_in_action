# Summary

## Redis In Action

* [简介](README.md)

## 认识Redis

* [什么是Redis?](ru-men/shi-yao-shi-redis.md)
* [Redis有什么优势?](ru-men/redisyou-shi-yao-you-shi.md)

## Redis基础

* [基本命令](ru-men/ji-ben-ming-ling.md)
  * [Key](ru-men/ji-ben-ming-ling/key.md)
  * [Server](ru-men/ji-ben-ming-ling/s.md)
* 数据类类型
  * [字符串](zi-fu-chuan.md)
  * [哈希表](ha-xi-biao.md)
  * [列表](lian-biao.md)
  * [集合](ji-he.md)
  * [有序集合](you-xu-ji-he.md)
  * [地理位置](di-li-wei-zhi.md)
  * [HyperLogLog](hyperloglog.md)

## 特性

* 键值通知
* [发布订阅](te-xing/fa-bu-ding-yue.md)
* 事务
* 持久化
* 脚本执行
* 主从
* 集群
* Sentinel

## 应用场景

* 内容管理-CMS
  * 点赞
  * Top10
  * 排序
  * 分页
  * 独立IP
* 电商-SHOP
  * [锁](#)
  * [秒杀](ying-yong-chang-jing/miao-sha.md)
  * 抢红包
* 社交应用-SNS
  * 快速登录
  * 活跃度
  * 好友关系
  * 消息订阅
* 地理位置-LBS
  * [周边商家](sheng-huo-fu-wu.md)
  * 摇一摇

## 开发规范

* [Key命名](kai-fa-gui-fan/keyming-ming.md)
* [超时时间](kai-fa-gui-fan/chao-shi-shi-jian.md)
* 内存考虑
* 缓存穿透
* 性能考虑
* 数据安全
  * 访问密码
  * 危险命令

