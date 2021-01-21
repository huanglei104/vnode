    cmake了内置了多个模块，就是一个个的.cmake文件，在/usr/share/cmake/<version>/Modules/目录下。
    一个模块中通常会定义一些函数，变量，宏等功能。如果要使用某个模块的功能，需要在CMakeLists.txt
    文件中使用find_package(ModuleName)包含进该模块，ModuleName是.cmake文件名去掉Find。

    在cmake中使用pkg-config：
    首先引入FindPkgConfig模块，然后使用该模块提供的命令pkg_search_module查找需要的库。例如，
    pkg_search_module(glib REQUIRED glib-2.0) (glib是随便定义的一个名字)
    如果该库被找到，则${glib_LIBRARIES}代表所有的库，${glib_INCLUDE_DIRS}代表所有的头文件目录
    
    添加一个头文件目录(gcc -I) ：include_directories(dir) ，dir可以是一个变量

    链接一个库(gcc -l)：link_libraries(lib)，lib可以是一个变量。该方式已经被废弃了，推荐使用target_link_libraries

    链接一个库(gcc -l)推荐方式：target_link_libraries(target item1 item2 ...)。target在前面必须已在存在，使用add_executable
    或add_library生成。item是库名，也可以是变量。



cmake_minimum_required (VERSION 2.8)  最低版本号

project (Demo1)  项目名称

add_executable(Demo main.cc) 将源文件编译成可执行文件(源文件可以有多个)

aux_source_directory(<dir> <variable>)  查找指定目录<dir>下的所有源文件，然后将结果存进指定变量<variable>

add_subdirectory(dir) 包含一个子目录

target_link_libraries(main abc) 表示可执行文件main需要链接一个abc库

add_library (abc a.c)  表示将源文件a.c 编译成abc静态链接库

pkg_check_modules(prefix gtk+-3.0) 用于检查包的信息，并将结果放在多个"prefix_"开关的变量中：
prefix_FONUD : 
如果包存在，则该变量对应的值为 1 
prefix_LIBRARIES ： 所有链接的库(没有 '-l')

prefix_LIBRARY_DIRS ： 所有链接的库的路径(没有 '-L')

prefix_LDFLAGS ： 所有链接器的参数

prefix_LDFLAGS_OTHER ： 所有链接器的其他参数

prefix_INCLUDE_DIRS ： 预处理器的-I参数(没有 '-I')
prefix_CFLAGS : 所有的cflags

prefix_CFLAGS_OTHER : 其他编译参数

cmake 包含多个模块，在/usr/share/cmake-3.15/Modules/ 目录下，要使某个模块的命令，需要在CMakeLists.txt文件中包含进该模块
比如使用FindPkgConfig : include(FindPkgConfig)
FindPkgConfig 模块提供了命令 
pkg_check_modules，
