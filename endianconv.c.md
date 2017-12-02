提供16、32、64位数据的字节序转换，即大小端的转换，该文件中的函数不会被直接调用，只会以宏定义（endianconv.h）的形式来间接使用。如果目标主机的CPU架构是小端模式，则不采取任何操作，如果是大端则转换成小端。
##函数
|函数|参数|返回值|说明
|---|---|---|---
|**memrev16**|void *p|void|内存中16位字节的字节序序逆置
|**memrev32**|void *p|void|内存中32位字节的字节序序逆置
|**memrev64**|void *p|void|内存中64位字节的字节序序逆置
|**intrev16**|unit16_t|uint16_t|调用memrev16()，将16位整型的字节序逆置
|**intrev32**|unit32_t|uint32_t|调用memrev32()，将32位整型的字节序逆置
|**intrev64**|unit64_t|uint64_t|调用memrev64()，将64位整型的字节序逆置

###区别
memrev前缀的函数和intrev前缀的函数其本质区别是：
- memrev函数会改变实参的字节序
- intrev函数，只是将实参逆置后的数据返回，并不改变实参的字节序

##宏
|宏名|说明
|----|----
|**memrev16ifbe(p)**|如果目标主机是小端则不变，大端就定义成memrev16(p)
|**memrev32ifbe(p)**|如果目标主机是小端则不变，大端就定义成memrev32(p)
|**memrev64ifbe(p)**|如果目标主机是小端则不变，大端就定义成memrev64(p)
|**intrev16ifbe(p)**|如果目标主机是小端则不变，大端就定义成intrev16(p)
|**intrev32ifbe(p)**|如果目标主机是小端则不变，大端就定义成intrev32(p)
|**intrev64ifbe(p)**|如果目标主机是小端则不变，大端就定义成intrev64(p)

在头文件`endianconv.h`中定义