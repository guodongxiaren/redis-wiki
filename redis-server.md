## redis-server
依赖的可执行文件（REDIS_SERVER_OBJ）
- adlist.o |数据类型list
- quicklist.o 
- ae.o 
- anet.o 
- dict.o 
- redis.o 
- sds.o 
- zmalloc.o 
- lzf_c.o 
- lzf_d.o 
- pqsort.o 
- zipmap.o 
- sha1.o 
- ziplist.o 
- release.o 
- networking.o 
- util.o 
- object.o 
- db.o 
- replication.o 
- rdb.o 
- t_string.o 
- t_list.o 
- t_set.o 
- t_zset.o 
- t_hash.o 
- config.o 
- aof.o 
- pubsub.o 
- multi.o 
- debug.o 
- sort.o 
- intset.o 
- syncio.o 
- cluster.o 
- crc16.o 
- endianconv.o 
- slowlog.o 
- scripting.o 
- bio.o 
- rio.o 
- rand.o 
- memtest.o 
- crc64.o 
- bitops.o 
- sentinel.o 
- notify.o 
- setproctitle.o 
- blocked.o 
- hyperloglog.o 
- latency.o 
- sparkline.o 
- redis-check-rdb.o

## adlist
额外包含的头文件zmalloc.h
## zmalloc.c
config.h
## config.c
- redis.h
- cluster.h

## redis.o
redis.h
- ae.h
- sds.h
- dict.h
- adlist.h
- zmalloc.h
- anet.h
- ziplist.h
- intset.h
- version.h
- util.h
- latency.h
- sparkline.h
- quicklist.h

redis.c
- cluster.h
- slowlog.h
- bio.h

