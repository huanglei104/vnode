# 文件IO

STDIN_FILENO        0
STDOUT_FILENO    1
STDERR_FILENO     2

 每个进程能打开的文件描述符的范围 0 ～ OPEN_MAX - 1

文件名的长度最大 NAME_MAX
整个路径名的最大长度 PATH_MAX

_POSIX_NO_TRUNC 常量决定当文件名或路径名长度超过最大值时是出错还是截断（不同的文件系统类型不一样）

进程终止时，内核会自动关闭该进程所有的打开文件