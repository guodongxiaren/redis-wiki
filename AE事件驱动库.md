- [[ae.c|ae.c]]

ae事件库在不同平台依赖于不同的实现：
- ae_evport.c
- ae_kqueue.c
- ae_select.c
- [[ae_epoll.c|ae_epoll.c]]

## 使用流程
- aeCreateEventLoop
- aeSetBeforeSleepProc
- aeMain
- aeDeleteEventLoop

这四个文件提供了相同的API函数接口。（针对接口编程）
## 事件类型
- 文件事件
- 时间事件

## 时间事件
以id为时间标识。是一个链表结构。