util.c/h用到的自定义头文件有：
- **sha1.h**
- **sds.h**
- fmacros.h

##函数（12个）
###stringmatchlen
Glob风格的模式匹配函数
###stringmatch
调用了stringmatchlen函数。  
比stringmatchlen少两个参数：用strlen(pattern)，strlen(string)来指明模式串和待匹配串的长度。