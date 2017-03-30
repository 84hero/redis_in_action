# 脚本

从 Redis 2.6.0 版本开始，通过内置的 Lua 解释器，可以使用 EVAL 命令对 Lua 脚本进行求值。

```
EVAL script numkeys key [key ...] arg [arg ...]
```

