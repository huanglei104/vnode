tty0 表示当前用户的虚拟终端的别名，这个是一定有的, 
tty 表示当前进程的控制终端，控制终端可能是虚拟终端，也可能是伪终端，但并不是所有的进程都一定有控制终端

Linux支持BSD和System V两种风格的伪终端设备，BSD风格下伪终端是系统预创建的，/dev/ptyXY表示主设备，/dev/ttyXY表示从设备，其中，X、Y分别属于字符集{{p-z},{a-e}}和{{0-9},{a-f}}。System V风格（又称为UNIX 98）下伪终端是动态创建的，所有的主设备对应的设备文件都是/dev/ptmx（主设备号为5，次设备号为2），而从设备对应的设备文件都位于/dev/pts/目录下，以设备的数字编号命名（如/dev/pts/0）。
从2.6.4版本内核开始，BSD风格伪终端被认为过时，不再被新的应用使用，可以在配置内核时去除对BSD伪终端的支持。

关于/dev/ptmx与/dev/pts/ptmx
https://unix.stackexchange.com/questions/492823/where-does-dev-pts-ptmx-come-from
http://tomoyo.osdn.jp/cgi-bin/lxr/source/Documentation/filesystems/devpts.txt?v=linux-4.6.7

/dev/vcsN 表示对应console(tty)的内容 ， /dev/vcsaN 表示对应 console(tty)的内容，且带有属性(颜色等)。

控制终端不一定就是标准输入输出(但一般都是)，即使当前进行有控制终端，标准输入输出也可以自由重定向。（bash > /dev/zero重定向输出，bash < /dev/zero重定向输入）控制终端主要用来处理信号与中断及与用户交互。


断开与控制终端的连接：ioctl(fd, TIOCNOTTY);
让一个终端设备成为控制终端： 
ioctl(fd,TIOCSCTTY, 
0);


文件描述符标志：目前只有一个FD_CLOEXEC,
置位表示exec时关闭该文件描述符。

/dev/console
console 只是一个输出设备，tty既能输出又能输入
https://blog.csdn.net/wangrunmin/article/details/7577807

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
linux内核有两种console设备，一种是system ， modular。
system有且只有一个，所有console共用。
modular可以有0个或多个，每个console可以单独指定使用哪个modular(fbcon=map)。但同时只能有一个modular是激活的。
内核启动后，console首先由system接管，之后可以由modular接管，modular之间不可以互相接管console。当没有modular接管console时，由system接管。

console驱动有许多种，在x86平台上，主要有 VGA text 和 framebuffer。 在Device Drivers-->Graphics support-->Console display driver support下
可以进行选择（可能没有显示）也可以在drivers/video/console/Kconfig 文件中看到 相关配置。
如果没有配置任何一种console驱动，则dummy console驱动会被默认使用。
每一种console驱动，都会在/sys/class/vtconsole/添加一个设备。

在x86平台上，system console驱动是VGA text。

framebuffer console(fbcon) 是一种 framebuffer device(fbdev) ，是一种使用framebuffer来实现的console。
所以framebuffer console ！= framebuffer device。只有内核配置了framebuffer device才能配置framebuffer console。
framebuffer 对上提供了统一的接口，对下屏蔽了各种不同硬件之间的差异。


