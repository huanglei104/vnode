vesafb 驱动只能直接编译进内核，不支持模块的方式

uvesafb能提供比vesafb更多的特性，但需要用户空间v86d程序的的支持。


linux/module.h:
#define module_init(x)       __initcall(x);
linux/init.h:
#define __initcall(fn)      device_initcall(fn)
linux/init.h:
#define device_initcall(fn)      __define_initcall(fn, 6)

init.h中定义了8种级别的initcall, 从0 到 7：
     pure_initcall, core_initcall, postcore_initcall, arch_initcall, subsys_initcall, fs_initcall, rootfs_initcall, device_initfs, late_initcall
     (rootfs_initcall 不属于这8个级别，其级别是固定的，在5和6之间)



start_kernel
          set_task_stack_end_magic(&init_task)    //系统的第一个进程，0号进程
          printk_safe_init
          console_init
          vfs_caches_init          
               mnt_init      //创建并挂载rootfs和sysfs
               bdev_cache_init    //块设备init
               chrdev_init          //字符设备init
          proc_root_init             //创建并挂载procfs
          arch_call_rest_init
               rest_init             //主要是创建1号，2号进程
                    kernel_thread(kernel_init, NULL, CLONE_FS)    //1号进程， init
                         kernel_init_freeable
                              do_basic_setup      //调用各种initcall，包括rootfs_initcall
                              ksys_open((const char __user *) "/dev/console", O_RDWR, 0)
                    kernel_thread(kthreadd, NULL, CLONE_FS | CLONE_FILES)  //2号进程 ，kthreadd 

rootfs未挂载前，内核如何根据 root＝/dev/xxx 找到设备的 ?
roofs的挂载与其他文件系统的挂载不一样，是通过名称直接解析出设备号的。
initramfs 就是 rootfs

即使内核配置不支持initramfs, 内核依然会创建一个最小的rootfs， 仅仅包含/dev/, /dev/console, /root
init/noinitramfs.c



  obj-m+=hello.o 表示编译成模块
obj-y+=hello.o 表示编译进内核

内核的初始化函数为int init_module(void)，卸载函数为void cleanup_module(void);
如果不是这两个函数，则需要分别用module_init和module_exit来调用。




   内核维护了一个日志缓冲区，叫做ring buffer，它的大小可以在编译内核前时行配置。在内核中，使用printk打印的信息会全部放到ring buffer里，并且优先级高于(数字小)当前终端的console_loglevel的信息会打印到控制台(console)上。

通过用户空间的函数klogctl(syslog)可以来改变console_loglevel，也可以通过/proc/sys/kernel/printk。klogctl(syslog)是通过系统调用syslog来控制ring buffer的。

但在内核启动的早期，控制台尚未初始化，这个时候使用printk打印的信息只会放到ring buffer,直到控制台初始化后，ring buffer里的信息才会被一并输出。linux提供了early console机制boot console，简称bcon，可以使用early_printk向

bcon输出信息，但这些信息不会保存到ring buffer里。early console机制有两种实现方式，早期的early_printk和后面的earlycon

要启用early_printk，要在内核中进行配置Kernel hacking ---> Kernel low-level debugging functions --> Early printk ，并在启动参数上加上 earlyprintk


printk的默认日志级别(default_message_loglevel)是 4( KERN_WARNING)。

dmesg也是调用了klogctl函数


/proc/sys/kernel/printk 的4个数字分别对应：console_loglevel default_message_loglevel minimum_console_loglevel default_console_loglevel

ring buffer 有3个标志，log_start(日志的起始位置) ,con_start(需要输入到控制台的日志的起始位置), log_end(日志的结束位置)

/proc/kmsg 只会输出可读的信息，已经输出过的不会再输出，并且还会阻塞，等待信息的到来 。 而dmesg会输出所有的信息，从log_start 到 log_end
