### 选项：
    -q 不显示介绍信息
    -batch 以批处理模式运行，没有错误则退出状态为0，有错误则退出状态为非0
    -x 从指定的文件中读取gdb的命令来执行
    -ex  指定一个gdb命令
    -s 指定符号文件

### 命令
    info threads 查看线程信息
    info break 显示断点信息
    thread 显示当前线程信息
        threads id 切换到某个线程
        thread apply 在多个线程上执行某个命令， 后面可以是空格分隔的多个线程id，也可以是all表示所有线程
            （thread apply all bt 显示所有线程的堆栈）
        thread find 通过正则表达式来查找线程
        thread name 设置当前线程的名称
    x 查看内存或寄存器 （$regname 表示寄存器）
    e 编辑源码
    list 显示源码

汇编单步： si
设置汇编风格：set disassembly-flavor intel
查看寄存器： info reg