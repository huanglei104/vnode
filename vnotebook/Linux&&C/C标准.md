C语言标准最初由ANSI定义，所以称为ANSI C (C89)
之后ANSI C89的基础上作了一些小改动，被纳入了ISO标准，这个标准称为ISO C (C90)
由些可见ANSI C， C89, ISO C , C90 其实可以看作同一标准(差别不大)

C99是由ISO 发布 ，是C语言的第二个标准版本
C11是由ISO 发布 ，是C语言的第三个标准版本

C89 头文件：assert, ctype, errno, float, iso646, limits, locale, math, setjmp, signal, stdarg, stddef, stdio, stdlib, string, time, wchar, wctype
C99 新增：    complex, fenv, inttypes, stdbool, stdint, tgmath 
C11 新增：    stdalign, stdatomic, stdnoreturn, threads, uchar

POSIX最初是由IEEE制定的一个标准，仅仅规范了操作系统的调用服务接口，正式名称为 IEEE Std 1003.1-1988, 修定了多次之后成为IEEE Std 1003.1-1990正式出版，
该标准也称为POSIX.1。该标准持续发展，加入了许多新的内容，像IEEE Std 1003.2， IEEE Std 1003.2 等。整个标准可以被分为POSIX.1， POSIX.2, POSIX.3, POSIX.4 
4个部分。

POSIX 必须的头文件：
     dirent, fcntl, fnmatch, glob, grp, netdb, pwd, regex, tar, termios, unistd, utime, wordexp, arpa/inet, net/if, netinet/in, 
     netinet/tcp, sys/mman, sys/select, sys/socket, sys/stat, sys/times, sys/types, sys/un, sys/utsname, sys/wait

POSIX XSI 扩展必须的头文件：
     cpio, dlfcn, fmtmsg, ftw, iconv, langinfo, libgen, monetary, ndbm, nl_types, poll, search, strings, syslog, ulimit, utmpx, 
     sys/ipc, sys/msg, sys/resource, sys/sem, sys/shm, sys/statvfs, sys/time, sys/uio
     ucontext(被废弃)， sys/timeb(被废弃)

POSIX 可选的头文件：
     aio, mqueue, pthread, sched, semaphore, spawn, stropts, trace

POSIX XSI 扩展是Single Unix Specifition 规定的，只能实现了该标准的系统才能被称为Unix

     
