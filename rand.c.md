用于替换默认的Lua实现的math.random()算法生成PRNG（伪随机数）
>作者编写这个文件的目的是用于替换Lua中实现的math.random()函数。作者认为Lua随机数生成算法的默认实现中使用了libc的rand()函数，而libc的rand()并不能保证在设置了相同种子的情况下，不同平台能生成相同的随机数序列。因此作者重写这一文件，保证跨平台性。

##宏
|宏名|说明
|:---|---
|N|16
|MASK|掩码。N=16时，MASK=65535（16个二进制1）
|LOW(x)|求x的低位的两个字节
|HIGH(x)|求x的高位两个字节
|MUL(x,y,z)|乘法：z[0]保存`LOW(x*y)`,z[1]保存`HIGH(x*y)`
|CARRY(x,y)|进位标识：x+y的和是否超过两个字节大小（65535）
|ADDEQU(x,y,z)|`z = CARRY(x, (y)), x = LOW(x + (y))`
|X0|0x330E
|X1|0xABCD
|X2|0x1234
|A0|0xE66D
|A1|0xDEEC
|A2|0x5
|C|0xB
|SET3(x,x0,x1,x2)|将x0，x1，x2赋值给数组x的前三个元素
|SETLOW(x,y,n)|`SET3(x, LOW((y)[n]), LOW((y)[(n)+1]), LOW((y)[(n)+2]))`
|SEED(x0,x1,x2)|`SET3(x, x0, x1, x2), SET3(a, A0, A1, A2), c = C`
|REST(v)|`for (i = 0; i < 3; i++) { xsubi[i] = x[i]; x[i] = temp[i]; } \return (v);`
|HI_BIT|2^31。1后面31个0（long型）

##全局变量
变量都是static类型的

|变量名|类型|初始化值
|---|---|---
|x|uint32_t []|{X0,X1,X2}
|a|uint32_t []|{A0,A1,A2}
|c|uint32_t|C

##函数
|函数名|说明
|----|----
|redisLrand48|调用next()，返回随机数（int32_t类型）
|redisSrand48|设置随机数种子(改变数组x的默认值，a、c是恒定的)
|next|**static**函数，为redisLrand48()服务。比较复杂。

对外的接口是前两个函数。其功能与头文件`stdlib.h`中的lrand48()、srand48()基本一致（同样种子，返回值相同）。不过lrand()返回的是long int型，而redisLrand48()返回的是int类型。不过Redis随机数算法的内部实现更精简，效率更高（丢弃了跨平台特性）