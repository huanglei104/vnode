# IPC
当FIFO只读(O_RDONLY)或只写(O_WRONLY)打开时，如果没有设置O_NOBLOCKING，则会阻塞住，直到管道的两端都被打开。或者是以读写的方式打开就不会阻塞。

## 信号量
### linux下的信号量有XSI信号量和posix信号量两种
### XSI信号量的接口：

    int semget(key_t key, int nsems, int semflg);
        创建或获取一个信号量数组
        key：信号量数组在内核中的唯一标识
        nsems：数组中信号量的个数
        semflg：flag
    int semop(int semid, struct sembuf *sops, size_t nsops);
        改变信号量的值或flag
        semid：信号量数组的ID
        sops：对信号量的操作
        nsops：要操作的信号量的个数
    int semctl(int semid, int semnum, int cmd, ...);
        操作信号数组
        semid：信号量数组的ID
        semnum：信号量在数组里的编号
        cmd：操作的命令

### POSIX信号量
### 命名信号量接口：
        sem_t *sem_open(const char *name, int oflag);
            创建或使用一个现有的信号量
            name：信号量的名字
            oflag：标志
        int sem_close(sem_t *sem);
            释放信号量相关资源
        int sem_unlink(const char *name);
            与文件的unlik相似
        int sem_wait(sem_t *sem);
        int sem_trywait(sem_t *sem);
        int sem_timedwait(sem_t *sem, const struct timespec *abs_timeout);
            信号量P操作
        int sem_post(sem_t *sem);
            信号量V操作
        int sem_getvalue(sem_t *restrict, int *restrict);
            获取信号量当前值

### 无名信号量接口：
        int sem_init(sem_t *sem, int pshared, unsigned int value);
        初始化一个无名信号量
        int sem_destroy(sem_t *sem);
        销毁一个无名信号量

# 共享内存
linux上共享内存有三种：XSI共享内存，POSIX共享内存，mmap
## XSI共享内存接口
    int shmget(key_t key, size_t size, int shmflg);
    创建或获取一个共享内存
    size：共享内存的大小
    void *shmat(int shmid, const void *shmaddr, int shmflg);
    将共享内存映射到当前进程中
    int shmctl(int shmid, int cmd, struct shmid_ds *buf);
    对共享内存进行操作
    int shmdt(const void *shmaddr);
    解除共享内存的映射
## POSIX共享内存接口
    POSIX共享内存是对mmap的封装，使用时还需要用mmap
    int shm_open(const char *name, int oflag, mode_t mode);
    创建或打开一个共享内存对象
    int shm_unlink(const char *name);
    移除一个共享内存对象
## mmap接口
    void *mmap(void *addr, size_t length, int port, int flags, int fd, off_t offset);
    将一块内存地址映射到进程空间中
    int munmap(void *addr, size_t length);
    取消内存映射