# 最大文件数限制(二):搞懂ulimit命令与limit.conf配置文件

> 上下文承接

# ulimit命令

**为什么需要ulimit**

ulimit用于系统资源限制,默认的配置很多时候是不适用的,对于部署的特殊应用常常会出现资源不足的抱怨. 执行一下`ulimit -a`查看对当前用户的资源限制情况.

**ulimit都对哪些资源进行限制**

![ulimit效果图](/img/ulimit.png)

可以看到输出的括号内表明了每种资源的单位,unlimited表示不做限制.

| 选项 | 含义                                       | 举例                                                                                      |
|------|--------------------------------------------|-------------------------------------------------------------------------------------------|
| -a   | 显示当前所有的limit信息                    | ulimit – a, 可以看到资源限制的概况                                                        |
| -c   | 最大的core 文件的大小,单位为blocks         | ulimit – c unlimited,  如果允许系统生成core文件,那么最好对core大小做限制,防止占用太多空间 |
| -d   | 进程最大的数据段的大小                     | ulimit -d unlimited；对进程的数据段大小不进行限制                                         |
| -f   | 进程可以创建最大文件的大小，单位为blocks   | ulimit – f unlimited                                                                      |
| -i   | 挂起信号最大数                             | ulimit -i unlimited                                                                       |
| -l   | 最大可加锁内存大小，以 Kbytes 为单位       | ulimit – l unlimited                                                                      |
| -m   | 最大内存大小，以 Kbytes 为单位。           | ulimit – m unlimited；对最大内存不进行限制。                                              |
| -n   | 可以打开最大文件描述符的数量。             | ulimit – n 10240；限制最大可以使用10240个文件描述符。                                     |
| -p   | 管道缓冲区的大小，以 Kbytes 为单位。       | ulimit – p 512；限制管道缓冲区的大小为 512 Kbytes。                                       |
| -q   | 消息队列大小                               | ulimit -q 819200                                                                          |
| -s   | 线程栈大小，以 Kbytes 为单位。             | ulimit – s 512；限制线程栈的大小为 512 Kbytes。                                           |
| -t   | 最大的 CPU 占用时间，以秒为单位。          | ulimit – t unlimited；对最大的 CPU 占用时间不进行限制。                                   |
| -u   | 用户最大可用的进程数。                     | ulimit – u 64；限制用户最多可以使用 64 个进程。                                           |
| -v   | 进程最大可用的虚拟内存，以 Kbytes 为单位。 | ulimit – v 200000；限制最大可用的虚拟内存为 200000 Kbytes。                               |

> ulimit只对当前终端有效,所以无法登陆的用户(比如特定服务的用户)是不能修改的.只能改变`/etc/security/limits.conf`

# limits.conf配置永久修改

ulimit控制的是终端,而且退出后,修改会失效.想进行用户级控制,或者修改默认的控制值只能通过修改`/etc/security/limits.conf`文件来进行.该文件的格式如下:

```
<domain>        <type>  <item>          <value>
```

例如:

```
*               soft    core            0
root            hard    core            100000
*               hard    rss             10000
@student        hard    nproc           20
@faculty        soft    nproc           20
@faculty        hard    nproc           50
ftp             hard    nproc           0
@student        -       maxlogins       4
```

具体可以查看`man limits.conf`

> **需要注意的是指定root用户时`*`是无效的,必须写明domain必须为`root`**

**打开文件数的限制调整**

如果提供web服务,默认最多打开1024个文件,这远远不够,需要调整.

```
配置系统打开文件的最大总数
#/etc/sysctl.conf
fs.file-max = 64000

配置用户级别的控制
#/etc/secutiry/limits.conf
* - nofile 8192
```
