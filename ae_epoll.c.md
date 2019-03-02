Linux平台下事件模型的实现
========
## aeApiState
一个结构体

|成员|类型|说明
|---|---|----
|epfd|int|epoll事件的fd
|events|epoll_event *|epoll事件指针（表示数组）

## 函数
都是static的。除了aeApiName()以外，其他函数第一个参数都是`aeEventLoop *`。

|函数|说明
|---|----
|aeApiCreate|

-----------
该文件完全被ae.c调用。各函数调用关系如下(aeApi开头的都是`ae_epoll.c`中的函数)：

- ae.c
  - aeCreateEventLoop
    - aeApiCreate
  - aeResizeSetSize
    - aeApiResize
  - aeDeleteEventLoop
    - aeApiFree
  - aeCreateFileEvent
    - aeApiAddEvent
  - aeDeleteFileEvent
    - aeApiDelEvent
  - aeProcessEvent
    - aeApiPoll
  - aeGetApiName
    - aeApiName
