该文件在是`util/generate-command-help.rb`脚本自动生成的

包含一个静态字符串数组commandGroups和一个自定义的结构体数组commandHelp
##commandGroups
定义了命令的种类（分组）
```c
static char *commandGroups[] = {
    "generic",
    "string",
    "list",
    "set",
    "sorted_set",
    "hash",
    "pubsub",
    "transactions",
    "connection",
    "server",
    "scripting",
    "hyperloglog"
};
```
##commandHelp
这是结构体数组名，其类型名也为**commandHelp**，用于封装help命令的返回信息。  
>`HELP command`可以查询command命令的用法。  

该结构体的的成员有：

|成员|类型|说明
|----|---|----
|name|char *|命令名
|params|char *|命令后面的参数
|summary|char *|命令简介
|group|int|命令的种类（所属的分组）
|since|char *|第一次引入该命令的Redis版本号