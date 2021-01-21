DNS 有多种类型：
    A:   域名的IPv4地址
    AAAA:    域名的IPv6地址
    CNAME:    域名的别名
    MX:    smtp邮箱域名的IP地址
        。
        。
        。
     同一个域名可以有多个DNS类型，因此同一个域名就可以解析出多个IP地址。

    同一个域名下提供的不同服务不一定就在同一台主机上，所以解析域名的时候，就要根据服务类型解析出对应的IP。

    host命令(arch上是bind-tools包)可以用来解析域名， -t参数可以指定类型

参考：https://www.zhihu.com/question/22362718