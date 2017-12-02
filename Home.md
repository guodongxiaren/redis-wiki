## 基本概念
### 名称由来
**Redis** 是**RE**mote **DI**ctionary **S**erver（远程字典服务器）的缩写
### 端口号
默认端口6379。也可以在启动服务器的时候通过选项`--port`指定端口号：

    redis-server --port 6666
>默认端口6379是手机键盘上MERZ对应的数字,MERZ 是一名意大利歌女的名字

### 命令
Redis支持一百多种[[命令|http://redis.io/commands]]，但常用的只有十几种[[命令|命令]]。这些命令用于客户端（resis-cli），且不区分大小写。
## 组成部分
Redis注意由以下6个部分（可执行文件）组成。

|名称|描述
|----|----
|redis-server|Redis服务器
|redis-cli|Redis命令行接口（客户端）
|redis-benchmark|Redis性能测试工具
|redis-check-aof|AOF文件修复工具
|redis-check-dump|RDB文件检查工具

## 数据类型
- string
- hash
- list
- set
- zset(sorted set)

