##全局变量
|名称|类型|说明
|----|----|----
|used_memory|static size_t|Redis已用内存空间的大小
|zmalloc_thread_safe|static int|标识是否线程安全
|used_memory_mutex|pthread_mutex_t|修改变量used_memory时的互斥锁
|zmalloc_oom_handler|static void (*)(size_t)|函数指针指向内存不足时调用的函数

##函数
###主要函数
|名称|说明
|----|----
|zmalloc|分配内存空间
|zfree|释放zmalloc分配的空间
|zcalloc|分配内存空间并初始化为0
|zrealloc|重新分配空间的大小
|zstrdup|字符串复制
|zlibc_free|同free()

###其他函数
|名称|说明
|----|----
|zmalloc_enable_thread_safeness|设置线程安全标识（zmalloc_thread_safe置1）
|zmalloc_get_fragmentation_ratio|内存使用率：RSS/used_memory
|`zmalloc_get_memory_size`|返回系统物理内存的大小（单位：字节）
|zmalloc_get_private_dirty|查询`/proc/self/smaps`中"Private Dirty"的大小
|zmalloc_get_rss|通过查询`/proc/<pid>/stat`文件获得**RSS**的值
|zmalloc_get_smap_bytes_by_field|查询`/proc/self/smaps`的指定字段的大小
|zmalloc_set_oom_handler|设置oom（内存不足）函数指针的值
|zmalloc_size|查询系统实际分配的内存空间的大小
|zmalloc_used_memory|查询已用空间（used_memory）的大小
>RSS（Resident Set Size）表示当前进程驻留在内存物理地址空间中的大小，即不包含被交换（swap）出去的大小。    
>`zmalloc_get_memory_size()`该函数在最新的Redis发布版中还未被包含。仅在目前（2015/04）的github开发版中。

##宏
###宏函数
|名称|说明
|----|----
|update_zamlloc_stat_alloc|分配内存空间后更新used_memory的值
|update_zamlloc_stat_free|释放内存空间后更新used_memory的值
|update_zamlloc_stat_add|线程安全地used_memory增加操作
|update_zamlloc_stat_sub|线程安全地used_memory减少操作

###自定义宏
|名称|说明
|----|----
|PREFIX_SIZE|内存分配时比需求多分配的空间大小 
|HAVE_MALLOC_SIZE|若使用tc_malloc、jemalloc或Mac系统则定义此宏

###检测宏
|名称|说明
|----|----
|__ATOMIC_RELAXED|原子操作宏（GCC定义）
|HAVE_ATOMIC|原子操作宏（config.h中声明）