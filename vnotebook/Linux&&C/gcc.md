-std= 
    c90/c99 等表示使用是标准C语法
    gnu90/gnu99 等表示在对应的标准C上加上了gnu扩展特性（比如支持//注释）


ld -o test -dynamic-linker /lib64/ld-linux-x86-64.so.2 -pie /usr/lib/Scrt1.o /usr/lib/crti.o /usr/lib/gcc/x86_64-pc-linux-gnu/9.1.0/crtbeginS.o -L/usr/lib/gcc/x86_64-pc-linux-gnu/9.1.0 -L/usr/lib -L/lib/ test.o -lgcc --push-state --as-needed -lgcc_s --pop-state -lc -lgcc /usr/lib/gcc/x86_64-pc-linux-gnu/9.1.0/crtendS.o /usr/lib/crtn.o

全局/局部
静态/非静态
初始化/未初始化


所有初始化的全局/静态变量都存在.data段，所有未初始化的全局/静态变量都在.bss中，在程序加载时，.bss中的变量值将被赋值为0。
如果一个全局变量被明确地初始化为0，则默认情况下，该变量会保存在.bss中，可以通过fno-zero-initialized-in-bss来改变这一行为。

gcc在默认情况下，会将全局未初始化的变量(可重定位的目标文件中)放在.common段中，链接时，多个可重定位文件中的同名的变量将共享内存，大小为最大变量的大小。
改变这一默认行为可以用-fno-common，则未初始化的变量将放在.bss中。

字符串(值，非名字)保存在.rodata段中，不可以改变，如果改.rodata中的数据，则会引起Segmentation fault (core dumped)。



有个简单的命令可以查看gcc预定义了哪些宏：
gcc -E -dM -  < /dev/null
其中，
-E  表示仅作预处理，不进行编译、汇编和链接；
-dM 表示处理的所有宏，包括预定义宏；
-   管线符号，用作gcc的处理文件；
<   重定向输入符号，表示内容重定向到管线；
/dev/null null文件。


# GCC扩展
[嵌套函数](https://gcc.gnu.org/onlinedocs/gcc-10.2.0/gcc/Nested-Functions.html#Nested-Functions)


# 编译选项
-m32 : 将int ，long 和指针类型都设置为32位长度，生成的代码只能i386上运行
-march=cpu-type： 指定cpu类型
-mtune=cpu-type：
-masm=asm：选择汇编语言的语法 ，有att和intel可选