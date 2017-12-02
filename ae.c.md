## 函数调用结构
aeMain
- aeProcessEvents
  - aeSearchNearestTimer
  - aeGetTime
  - `aeApiPoll`<kbd>ae_epoll</kbd>
  - processTimeEvents

# aeEventLoop
|成员|类型|说明
|---|----|----
|maxfd|int|当前注册的最大fd
|setsize|int|监视的fd的最大数量
|timeEventNextId|long long|下一个时间事件的ID
|lastTime|time_t|
|events|[aeFileEvent](#aefileevent) *|已注册事件
|fired|[aeFiredEvent](#aefiredevent) *|就绪的事件（已达到注册时的可读或可写状态）
|timeEventHead|[aeTimeEvent](#aetimeevent)|时间事件链表头
|stop|int|是否停止（0：否；1：是）
|apidata|void *|polling API指定数据
|beforesleep|aeBeforeSleepProc *|函数指针

- fired：存储epoll_wait的出参返回的信息（就绪fd及其就绪事件）。fired数组（有效）下标与就绪事件的个数对应。
- events：从fired处获取信息，本身不存储就绪fd，但events的下标即就绪的fd（**HASH**策略）。此外存储针对读写事件的回调函数。

|函数|说明
|----|---
|**aeCreateEventLoop**|初始化一个事件循环结构体（eventLoop）
|aeGetSetSize|返回当前setsize的值
|**aeResizeSetSize**|改变setsize的值（空间重新分配）
|aeDeleteEventLoop|删除事件循环eventLoop（释放内存空间）
|aeStop|**停止事件循环**，即stop值设为1
|**aeProcessEvents**|事件处理逻辑
|aeMain|**启动事件循环**，事件循环的入口
|aeSetBeforeSleepProc|注册回调函数，即每次主循环在休眠（等待fd准备就绪）之前被调用的函数

# aeFileEvent
在aeEventLoop中存在aeFileEvent数组（指针）。hash策略，fd上的事件，对应[fd]位置元素。  
本身是由epoll_wait返回就绪事件之后（得出就绪fd及其mask）再装配完成一个文件事件结构体。然后再由该处已注册的读/写处理回调函数依据mask来相应处理。
```cpp
    if (fe->mask & mask & AE_READABLE) { // 什么鬼，这两个mask
```

|成员|类型|说明
|---|----|----
|mask|int|AE_READABLE；AE_WRITABLE 之一
|rfileProc|aeFileProc *|函数指针，处理读事件
|wfileProc|aeFileProc *|函数指针，处理写事件
|clientData|void *|读写事件处理函数所需的数据

|函数|说明|备注
|----|---|-----
|**aeCreateFileEvent**|创建文件事件|绑定fd与读写回调函数
|**aeDeleteFileEvent**|删除文件事件|
|aeGetFileEvents|返回指定fd对应的mask|

# aeTimeEvent

|成员|类型|说明
|---|----|----
|id|long long|时间事件标识符
|when_sec|long|秒数
|when_ms|long|毫秒
|timeProc|aeTimeProc *|回调函数
|cliend|void *|回调函数要处理的数据
|next|struct aeTimeEvent *|下一个时间事件

|函数|说明|备注
|----|---|----
|**aeCreateTimeEvent**|创建时间事件|
|**aeDeleteTimeEvent**|删除时间事件|
|aeGetTime|返回当前时间到两个参数中（秒，毫秒）|静态函数
|aeAddMillisecondsToNow|给指定的时间加上某个毫秒数|静态函数
|aeSearchNearestTimer|检索即将要发生的时间事件|静态函数
|**processTimeEvents**|处理时间事件|静态函数

# aeFiredEvent

|成员|类型|说明
|---|----|----
|fd|int|就绪fd
|mask|int|就绪事件类型掩码

# 独立函数

|函数|说明|备注
|---|---|---
|aeGetApiName|返回API的名称，比如`epoll`
|aeWait|在指定时间内，等待fd就绪|**poll()**实现
