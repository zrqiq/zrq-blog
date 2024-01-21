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

![image-20240121211040600](/home/zrq/.config/Typora/typora-user-images/image-20240121211040600.png)



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

