# Learn C

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



### 练习12

```
#include <stdio.h>

int main(int argc, char *argv[])
{
    int i = 0;

    if(argc == 1) {
        printf("You only have one argument. You suck.\n");
    } else if(argc > 1 && argc < 4) {
        printf("Here's your arguments:\n");

        for(i = 0; i < argc; i++) {
            printf("%s ", argv[i]);
        }
        printf("\n");
    } else {
        printf("You have too many arguments. You suck.\n");
    }

    return 0;
}
```

这个程序的主要目的是根据用户提供的命令行参数数量来给出相应的提示。如果用户只提供一个参数（通常是程序名），它会说用户只有一个参数；如果用户提供了2到3个参数，它会列出这些参数；如果用户提供了超过3个参数，它会说用户有太多的参数。

```
if语句的格式为：

if(TEST) {
    CODE;
} else if(TEST) {
    CODE;
} else {
    CODE;
}
```

关于运算符，我找到一篇非常棒的[文章](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/boolean-logical-operators)，里面讲的非常清楚

### 练习13

```
#include <stdio.h>

int main(int argc, char *argv[])
{
    if(argc != 2) {
        printf("ERROR: You need one argument.\n");
        // this is how you abort a program
        return 1;
    }

    int i = 0;
    for(i = 0; argv[1][i] != '\0'; i++) {
        char letter = argv[1][i];

        switch(letter) {
            case 'a':
            case 'A':
                printf("%d: 'A'\n", i);
                break;

            case 'e':
            case 'E':
                printf("%d: 'E'\n", i);
                break;

            case 'i':
            case 'I':
                printf("%d: 'I'\n", i);
                break;

            case 'o':
            case 'O':
                printf("%d: 'O'\n", i);
                break;

            case 'u':
            case 'U':
                printf("%d: 'U'\n", i);
                break;

            case 'y':
            case 'Y':
                if(i > 2) {
                    // it's only sometimes Y
                    printf("%d: 'Y'\n", i);
                }
                break;

            default:
                printf("%d: %c is not a vowel\n", i, letter);
        }
    }

    return 0;
}
```

这段代码的主要功能是读取用户输入的字符串（作为命令行参数），并检查其中的每个字符是否为元音字母。如果是，它就输出该字符及其在字符串中的位置。

和我自己所想代码不一样，我感觉主要是这个地方“int argc, char *argv[]”

argc 是一个整数，表示命令行参数的数量；argv 是一个字符指针数组，包含所有的命令行参数。(这个地方是我之前学习c语言时候没见过的地方)

> 在C语言中，int argc, char *argv[] 是用来从命令行接收参数的一种方法。它们是 main 函数的参数。
>
> int argc：这是一个整数，表示传递给程序的命令行参数的数量。
> char *argv[]：这是一个字符指针数组，用来存储传递给程序的命令行参数。
> 当你在命令行上运行一个程序时，你可以传递一些参数给它。例如，如果你有一个名为 program 的程序，你可以这样运行它：
>
> bash
> ./program arg1 arg2 arg3
> 在这个例子中，argc 的值是4（包括程序名），而 argv 数组会包含这些字符串：
>
> c
> argv[0] = "./program"  
> argv[1] = "arg1"  
> argv[2] = "arg2"  
> argv[3] = "arg3"
> 在C语言中，你可以使用这些参数来执行各种任务，例如读取配置文件、指定输入/输出文件等。



```
swicth语句工作原理的一个深究，然而实际操作中你只需要记住下面几条简单的原则：

总是要包含一个default:分支，可以让你接住被忽略的输入。
不要允许“贯穿”执行，除非你真的想这么做，这种情况下最好添加一个//fallthrough的注释。
一定要先编写case和break，再编写其中的代码。
如果能够简化的话，用if语句代替。
```

> 破坏一个switch语句块太容易了。下面是一些方法，你可以挑一个来用：
>
> 忘记写break，程序就会运行两个或多个代码块，这些都是你不想运行的。
> 忘记写default，程序会在静默中忽略你所忘记的值。
> 无意中将一些带有预料之外的值的变量放入switch中，比如带有奇怪的值的int。
> 在switch中是否未初始化的值。(这些都是我们需要注意的点，作为初学者我们很容易忽视)



### 练习14

```
#include <stdio.h>
#include <ctype.h>

// forward declarations
int can_print_it(char ch);
void print_letters(char arg[]);

void print_arguments(int argc, char *argv[])
{
    int i = 0;

    for(i = 0; i < argc; i++) {
        print_letters(argv[i]);
    }
}

void print_letters(char arg[])
{
    int i = 0;

    for(i = 0; arg[i] != '\0'; i++) {
        char ch = arg[i];

        if(can_print_it(ch)) {
            printf("'%c' == %d ", ch, ch);
        }
    }

    printf("\n");
}

int can_print_it(char ch)
{
    return isalpha(ch) || isblank(ch);
}


int main(int argc, char *argv[])
{
    print_arguments(argc, argv);
    return 0;
}

```

include <ctype.h> 是C语言中的一个预处理指令。当使用这个指令时，它告诉编译器包含ctype.h这个标准库头文件。

ctype.h库提供了很多有用的函数，这些函数用于测试和操作C语言中的字符。例如：

isalpha()：检查字符是否是字母。
isdigit()：检查字符是否是数字。
isspace()：检查字符是否是空白字符（如空格、制表符、换行符等）。
isupper()：检查字符是否是大写字母。
islower()：检查字符是否是小写字母。
这些函数通常用于字符分类，即确定一个字符属于哪个类别（如字母、数字、标点符号等）。

定义了三个函数：can_print_it、print_letters 和 print_arguments。

can_print_it(char ch)：检查字符 ch 是否是字母或空白字符。如果是，返回非零值；否则，返回零。
print_letters(char arg[])：打印字符串 arg 中的所有字母和空白字符。
print_arguments(int argc, char *argv[])：遍历命令行参数，并对每个参数调用 print_letters 函数。

### 练习15

```
#include <stdio.h>

int main(int argc, char *argv[])
{
    // create two arrays we care about
    int ages[] = {23, 43, 12, 89, 2};
    char *names[] = {
        "Alan", "Frank",
        "Mary", "John", "Lisa"
    };

    // safely get the size of ages
    int count = sizeof(ages) / sizeof(int);
    int i = 0;

    // first way using indexing
    for(i = 0; i < count; i++) {
        printf("%s has %d years alive.\n",
                names[i], ages[i]);
    }

    printf("---\n");

    // setup the pointers to the start of the arrays
    int *cur_age = ages;
    char **cur_name = names;

    // second way using pointers
    for(i = 0; i < count; i++) {
        printf("%s is %d years old.\n",
                *(cur_name+i), *(cur_age+i));
    }

    printf("---\n");

    // third way, pointers are just arrays
    for(i = 0; i < count; i++) {
        printf("%s is %d years old again.\n",
                cur_name[i], cur_age[i]);
    }

    printf("---\n");

    // fourth way with pointers in a stupid complex way
    for(cur_name = names, cur_age = ages;
            (cur_age - ages) < count;
            cur_name++, cur_age++)
    {
        printf("%s lived %d years so far.\n",
                *cur_name, *cur_age);
    }

    return 0;
}
```

> ex15.c:48-49
>
> cur_name和cur_age的值现在指向了相应数组中的一个元素，我们我可以通过*cur_name和*cur_age来打印它们，这里的意思是“cur_name和cur_age指向的值”。



这段C语言代码主要演示了如何使用数组和指针来处理和访问数组中的数据。
获取数组的大小：count 是 ages 数组的大小，通过 sizeof(ages) / sizeof(int) 计算得到。

第一种方式：

使用索引访问数组：使用传统的for循环和索引访问数组中的每个元素。

第二种方式：

使用指针访问数组：cur_age 和 cur_name 是指向数组的指针。

使用指针通过解引用（*）来访问数组元素。

第三种方式：

直接使用指针访问：不需要额外的变量来存储指向数组的指针，可以直接使用 names[i] 和 ages[i] 来访问。

**第四种方式：**

**使用指针的复杂方法访问数组：使用指针进行循环，并通过解引用指针来访问元素。这种方式相对复杂，但也是一种可能的访问数组的方法。
最后，返回0表示程序正常结束。**

```
在这个方法中，我们使用了两个指针cur_name和cur_age，它们分别指向names和ages数组的起始位置。然后，我们在循环中不断更新这两个指针的位置，直到它们指向数组的末尾。具体来说，cur_name = names 和 cur_age = ages 分别将两个指针指向各自数组的起始位置。在每次循环中，cur_name++ 和 cur_age++ 将指针向前移动一个位置。当 (cur_age - ages) < count 这个条件不满足时，即当前指针位置超过或等于数组的长度时，循环结束。在每次循环中，通过解引用指针 *cur_name 和 *cur_age，我们可以获取到当前指针指向的元素值，即名字和年龄。然后，我们使用这些值来打印出相应的信息。这种方法虽然看起来比较复杂，但实际上它是在演示如何使用指针来遍历数组，这是C语言中一种常见的操作。通过这种方式，我们可以更加灵活地操作数组中的元素，而不仅仅是通过索引来访问它们。

在C语言中，数组名本质上是指向数组第一个元素的指针。所以，当我们声明一个数组时，例如char *names[]，names实际上是一个指向数组第一个元素的指针。

1.cur_name = names; 和 cur_age = ages;
这两行代码的意思是将cur_name和cur_age两个指针分别指向names和ages数组的第一个元素。在C语言中，这等同于将指针设置为数组的起始地址。

2. (cur_age - ages) < count;

这个条件判断当前cur_age指针是否还在ages数组的范围内。在C语言中，指针相减可以得到两个指针之间的元素个数。例如，如果cur_age和ages都指向同一个数组，那么cur_age - ages的结果就是当前指针位置在数组中的索引。所以，这个条件判断的意思是：当cur_age指向的元素还在ages数组内时，循环继续执行。

3. cur_name++, cur_age++

这两行代码的意思是在每次循环结束后，将cur_name和cur_age指针向前移动一个位置，指向下一个元素。这样，在下一次循环中，它们将访问数组中的下一个元素。
```



> 实用的指针用法
> 你可以用指针做下面四个最基本的操作：
>
> - 向OS申请一块内存，并且用指针处理它。这包括字符串，和一些你从来没见过的东西，比如结构体。
> - 通过指针向函数传递大块的内存（比如很大的结构体），这样不必把全部数据都传递进去。
> - 获取函数的地址用于动态调用。对一块内存做复杂的搜索，比如，转换网络套接字中的字节，或者解析文件。
> - 对一块内存做复杂的搜索，比如，转换网络套接字中的字节，或者解析文件。



> 指针词库
>
> - type *ptr
>
> type类型的指针，名为ptr。
>
> - *ptr
>
> ptr所指向位置的值。
>
> - *(ptr + i)
>
> （ptr所指向位置加上i）的值。
>
> 译者注：以字节为单位的话，应该是ptr所指向的位置再加上sizeof(type) * i。
>
> - &thing
>
> thing的地址。
>
> - type *ptr = &thing
>
> 名为ptr，type类型的指针，值设置为thing的地址。
>
> - ptr++
>
> 自增ptr指向的位置。
>



> 指针并不是数组
> 无论怎么样，你都不应该把指针和数组混为一谈。它们并不是相同的东西，即使C让你以一些相同的方法来使用它们。例如，如果你访问上面代码中的sizeof(cur_age)，你会得到指针的大小，而不是它指向数组的大小。如果你想得到整个数组的大小，你应该使用数组的名称age，就像第12行那样。
>

### 练习16

```
#include <stdio.h>
#include <assert.h>
#include <stdlib.h>
#include <string.h>

struct Person {
    char *name;
    int age;
    int height;
    int weight;
};

struct Person *Person_create(char *name, int age, int height, int weight)
{
    struct Person *who = malloc(sizeof(struct Person));
    assert(who != NULL);

    who->name = strdup(name);
    who->age = age;
    who->height = height;
    who->weight = weight;

    return who;
}

void Person_destroy(struct Person *who)
{
    assert(who != NULL);

    free(who->name);
    free(who);
}

void Person_print(struct Person *who)
{
    printf("Name: %s\n", who->name);
    printf("\tAge: %d\n", who->age);
    printf("\tHeight: %d\n", who->height);
    printf("\tWeight: %d\n", who->weight);
}

int main(int argc, char *argv[])
{
    // make two people structures
    struct Person *joe = Person_create(
            "Joe Alex", 32, 64, 140);

    struct Person *frank = Person_create(
            "Frank Blank", 20, 72, 180);

    // print them out and where they are in memory
    printf("Joe is at memory location %p:\n", joe);
    Person_print(joe);

    printf("Frank is at memory location %p:\n", frank);
    Person_print(frank);

    // make everyone age 20 years and print them again
    joe->age += 20;
    joe->height -= 2;
    joe->weight += 40;
    Person_print(joe);

    frank->age += 20;
    frank->weight += 20;
    Person_print(frank);

    // destroy them both so we clean up
    Person_destroy(joe);
    Person_destroy(frank);

    return 0;
}
```

这段代码用于创建一个Person结构体来表示一个人，包括名字、年龄、身高和体重。该程序包括以下部分：

定义结构体：定义了一个名为Person的结构体，包含四个成员变量：一个指向字符的指针name，表示名字；三个整型变量age、height和weight，分别表示年龄、身高和体重。
创建结构体：Person_create函数用于创建一个新的Person结构体。它接收一个名字、年龄、身高和体重作为参数，并动态分配内存来存储这些信息。该函数返回一个指向新创建的Person结构体的指针。
销毁结构体：Person_destroy函数用于释放由Person_create函数分配的内存。它接收一个指向Person结构体的指针，并释放该结构体和其成员变量所占用的内存。
打印结构体：Person_print函数用于打印Person结构体的信息。它接收一个指向Person结构体的指针，并打印出该结构体的所有成员变量的值。
主函数：在主函数中，首先使用Person_create函数创建两个Person结构体，然后打印出它们的内存地址以及它们的成员变量的值。接着，让这两个人的年龄增加20岁，身高减少2厘米，体重增加40磅和20磅，并再次打印出他们的信息。最后，使用Person_destroy函数销毁这两个结构体以释放内存。
这个程序演示了如何使用C语言中的结构体和动态内存分配来创建和操作对象。注意，这个程序使用了断言(assert)来检查内存分配是否成功，如果内存分配失败（例如，由于内存不足），则程序会立即终止。
