auto tool 使用流程：
      运行autoscan  生成 configure.scan
      对configure.scan进行适当修改， 重命名为configure.ac （configure.ac也可手动编写）
       运行autoconf ，根据 configure.ac 生成 configure
       编写 Makefile.am
       运行automake，根据Makefile.am生成Makefile.in
       运行 ./configure，根据Makefile.in生成 Makefile
       make

configure.ac的配置：
    AC_PREREQ： autoconf 的最低版本   （该宏必须在AC_INI前调用）
    AC_INIT： 指定包名，版本号，bug报告地址  （该宏必须在所有会产生输出文件的宏之前调用）
    AC_CONFIG_SRCDIR： 指定源代码目录中的某个文件名，通过检查该文件是否存在来确定是否是实际的源代码目录 

