查看内存: xp /nuf addr   从物理地址addr开始， 查看n个单元， 每个单元的大小是u, 显示的方式是f 
         x /nuf addr   从线性地址addr开始， 查看n个单元， 每个单元的大小是u, 显示的方式是f 
         u: x 16进制，d 十进制，u 无符号， o 八进制， b 二进制， c ascii
         f: b 字节， h 字， w双字

0x100138 call pre_gdt

grub 有数据段和代码段两个段，都是base为0的4G空间。
. = 0xxxx 是将代码加载到该位置 。 加载的代码前面有300字节的其他的数据。
ENTRY实际是设置了eip的值。