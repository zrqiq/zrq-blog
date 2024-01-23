# learn C

### 练习1

```
touch ex1.c

vim ex1.c（CFLAGS="-Wall" make ex1）

make ex1

./ex1
```

> make ex1的含义
>
> 文件ex1存在吗？
> 没有。好的，有没有其他文件以ex1开头？
> 有，叫做ex1.c。我知道如何构建.c文件吗？
> 是的，我会运行命令cc ex1.c -o ex1来构建它。
> 我将使用cc从ex1.c文件来为你构建ex1。

```
int main(int argc, char *argv[])
{
    puts("Hello world.");

    return 0;
}
```

我发现练习1使用puts 和printf 都可以，都会在屏幕上打印相应的内容

但是会有警告，因为缺少头文件（可能是我之前弄过练习2，然后编译器就会给出详细警告），但是依旧可以执行



### 练习2

首先，创建文件并写入以下内容：

```
CFLAGS=-Wall -g

clean:
    rm -f ex1(注意是TAB键，不是空格)
```

将文件在你的当前文件夹上保存为Makefile

确保它和的ex1.c文件在相同的目录中，之后运行以下命令：

```
$ make clean
$ make ex1
```

然后编译器就会给出警告（缺少头文件）

### 练习4

> Valgrind

> Valgrind是一个运行你的程序的程序，并且随后会报告所有你犯下的可怕错误



我们该如何下载呢

```
1) #Download it (use wget if you don't have curl)

curl -O http://valgrind.org/downloads/valgrind-3.6.1.tar.bz2

use md5sum to make sure it matches the one on the site

md5sum valgrind-3.6.1.tar.bz2

2) #Unpack it.

tar -xjvf valgrind-3.6.1.tar.bz2

cd into the newly created directory

cd valgrind-3.6.1

3) #configure it

./configure

4) #make it

make

5) #install it (need root)

sudo make install
```

这个工具我自己下载过很多遍，删了下，下了删，反反复复，但是总是会在第二步失败，我也不知道为什么，今天又下载了一遍，还是和之前一样只成功了第一步，但是我完全可以使用这个工具，他也会像电子书里面的教程一样，完全是一个好工具，Valgrind会明确地告诉你程序中的每个错误都在哪儿

### 练习6

1、格式化输出整型
d 格式，用来输出十进制整数。

%d：按整型数据的实际长度输出；
%md：m为指定的输出宽度。如果数据的位数小于m，则左端补空格；若大于m，则按实际位数输出；
%0md：同上，但这里如果数据的位数小于m，则左端补0；若大于m，则按实际位数输出。

2、格式化输出浮点型
f 格式，用来输出小数。

%f：整数部分全部输出，并输出6位小数；
%.nf：整数部分全部输出，并输出n位小数；
%m.nf：输出共占m列，n位小数，若数值宽度小于m则左端补空格。

3、格式化输出字符串
s 格式，用来输出字符串。

%s：输入全部字符串；
%ms：输出的字符串共占m列，若字符串本身的长度小于m，则左补空格；若字符串本身的长度大于m，则全部输出。

```

a, A	#以十六进制形式输出浮点数(C99 新增）
d		#以十进制形式输出带符号整数(正数不输出符号)
o		#以八进制形式输出无符号整数(不输出前缀0)
x,X		#以十六进制形式输出无符号整数(不输出前缀Ox)
u		#以十进制形式输出无符号整数
f		#以小数形式输出单、双精度实数
e,E		#以指数形式输出单、双精度实数
g,G		#以%f或%e中较短的输出宽度输出单、双精度实数
c		#输出单个字符
s		#输出字符串
p		#输出指针地址
lu		#32位无符号整数
llu		#64位无符号整数
```

### 练习7

unsigned

```
unsigned意为“没有标记过的”，在C语言中表示无符号的，与关键字signed对应

这个关键字在很多头文件的变量定义中还是很常见的，一般用在整数类型的符号说明处

unsigned的作用是：声明无符号的整数类型。
unsigned的使用和signed类似，unsigned一般加在int等整数类型名称前：

/* unsigned可以修饰的几种类型 */
unsigned int a;             /* 无符号整型 */
unsigned short b; 			/* 无符号短整型 */
unsigned long c; 			/* 无符号长整型 */
unsigned long long d;	    /* 无符号long long类型 */
```



为什么char 和int 可以相乘？

> 字符就是整数
> 字符和整数没有本质的区别。可以给 char变量一个字符，也可以给它一个整数；反过来，可以给 int变量一个整数，也可以给它一个字符。
>
> char 变量在内存中存储的是字符对应的 ASCII 码值。如果以 %c 输出，会根据 ASCII码表转换成对应的字符，如果以 %d 输出，那么还是整数。
>
> int 变量在内存中存储的是整数本身，如果以 %c 输出时，也会根据 ASCII码表转换成对应的字符。
>
> 也就是说，ASCII 码表将整数和字符关联起来了



### 练习8

将full_name最后的'\0'去掉，并重新运行它，在valgrind下再运行一遍,此时会在屏幕上显示一大串我看不懂的东西。

![去除\0](/home/zrq/.config/Typora/typora-user-images/image-20240123134559452.png "去除\0")

### 练习9

字符串后面必须有"\0",否则程序就会崩溃

### 练习10

```
for循环的格式是这样的：

for(INITIALIZER; TEST; INCREMENTER) {
    CODE;
}
```

NULL在C语言中是什么东西？

> 大多数人的回答是："NULL就是系统定义特殊的0,把你初始化的指针指向它，可以防止“野指针”的恶果。"

关于NULL,我查到一篇有关[NULL习题](https://blog.csdn.net/fovwin/article/details/8057854)的文章，我觉得挺好的

### 练习11

> 在C语言中，实际上没有真正的“布尔”类型，而是用一个整数来代替，0代表false，其它值代表true。
>
> ```
> 在C语言中，实际上没有真正的“布尔”类型，而是用一个整数来代替，0代表false，其它值代表true。
> 
> 你可以看到while循环的语法更加简单：
> 
> while(TEST) {
>     CODE;
> }
> 只要TEST为true（非0），就会一直运行CODE中的代码。这意味着如果要达到和for循环同样的效果，我们需要自己写初始化语句，以及自己来使i增加。
> 
> ```
