# Redis HyperLogLog

Redis 在 2.8.9 版本添加了 HyperLogLog 结构。

Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定 的、并且是很小的。

在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。

* 工作日

```Redis
> PFADD weekday Monday Tuesday Wednesday Thursday Friday
(integer) 1
```

* 周末

```
> PFADD weekend Saturday Sunday
(integer) 1
```

* 工作日天数

```Redis
> PFCOUNT weekday
(integer) 5
```

* 周末天数

```Redis
> PFCOUNT weekend
(integer) 2
```

* 一周总天数

```Redis
> PFCOUNT weekday weekend
(integer) 7
```

* 合并工作日和周末

```Redis
> PFMERGE weeks weekend weekday
OK
```

* 计算一周天数

```Redis
> PFCOUNT weeks
(integer) 7
```



