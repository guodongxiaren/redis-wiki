数据结构之list。list是一个双向链表（非循环链表）
##文件
- adlist.h
- adlist.c

##结构体
###list结点
```c
typedef struct listNode {
    struct listNode *prev;
    struct listNode *next;
    void *value;
} listNode;
```
###list迭代器
```c
typedef struct listIter {
    listNode *next;
    int direction;
} listIter;
```
###list结构
```c
typedef struct list {
    listNode *head; // 头部
    listNode *tail; // 尾部
    void *(*dup)(void *ptr); // 函数指针：复制函数
    void (*free)(void *ptr); // 函数指针：清除内存函数
    int (*match)(void *ptr, void *key); // 函数指针：比较是否相等
    unsigned long len; // 结点个数
} list;
```
##函数
|函数名(15个)|描述
|-----|----
|listCreate|创建并初始化list
|**listRealease**|删除list分配的空间
|listAddNodeHead|将指定值的结点插入到list头部
|listAddNodeTail|将指定值的结点插入到list尾部
|**listInsertNode**|将指定值的结点插入到指定的结点后面（after参数不明所以）
|listDelNode|删除指定结点
|listGetIterator|获得指定方向的迭代器
|listNext|迭代器后移
|**listReleaseIterator**|删除迭代器（分配的空间）
|**listDup**|复制一个list
|listSearchKey|在list中搜索指定的值（参数为指针类型）
|**listIndex**|根据索引（从0数起）返回对应的结点
|listRewind|将迭代器置于list的头部
|listRewindTail|将迭代器置于list的尾部
|listRotate|将尾部元素插入到头部之前成为新的头部

```c
list *listCreate(void);
void listRelease(list *list);
list *listAddNodeHead(list *list, void *value);
list *listAddNodeTail(list *list, void *value);
list *listInsertNode(list *list, listNode *old_node, void *value, int after);
void listDelNode(list *list, listNode *node);
listIter *listGetIterator(list *list, int direction);
listNode *listNext(listIter *iter);
void listReleaseIterator(listIter *iter);
list *listDup(list *orig);
listNode *listSearchKey(list *list, void *key);
listNode *listIndex(list *list, long index);
void listRewind(list *list, listIter *li);
void listRewindTail(list *list, listIter *li);
void listRotate(list *list);
```