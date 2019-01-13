# 最大文件数限制(三):使用lsof命令诊断文件资源问题

## 通过一个例子理解lsof的用途

lsof的用途非常清晰, lsof(list open files), 通过该命令可以查看当前系统都打开了哪些文件. 下面简单执行下lsof命令来熟悉一下。

```
lsof
COMMAND   PID      USER   FD   TYPE             DEVICE SIZE/OFF     NODE NAME
...
tmux    63806 fishcried  cwd    DIR                8,1     4096 17563675 /home/fishcried
tmux    63806 fishcried  rtd    DIR                8,1     4096        2 /
tmux    63806 fishcried  txt    REG                8,1   467144 26224300 /usr/bin/tmux
tmux    63806 fishcried  mem    REG                8,1   141574 17829714 /lib/x86_64-linux-gnu/libpthread-2.19.so
tmux    63806 fishcried  mem    REG                8,1  1840928 17829722 /lib/x86_64-linux-gnu/libc-2.19.so
tmux    63806 fishcried  mem    REG                8,1   101240 17829704 /lib/x86_64-linux-gnu/libresolv-2.19.so
tmux    63806 fishcried  mem    REG                8,1   276880 26222194 /usr/lib/x86_64-linux-gnu/libevent-2.0.so.5.1.9
tmux    63806 fishcried  mem    REG                8,1   167096 17826068 /lib/x86_64-linux-gnu/libtinfo.so.5.9
tmux    63806 fishcried  mem    REG                8,1    10680 17829724 /lib/x86_64-linux-gnu/libutil-2.19.so
tmux    63806 fishcried  mem    REG                8,1   149120 17829715 /lib/x86_64-linux-gnu/ld-2.19.so
tmux    63806 fishcried    0u   CHR              136,2      0t0        5 /dev/pts/2
tmux    63806 fishcried    1u   CHR              136,2      0t0        5 /dev/pts/2
tmux    63806 fishcried    2u   CHR              136,2      0t0        5 /dev/pts/2
tmux    63806 fishcried    3u  unix 0x0000000000000000      0t0 72370395 socket
tmux    63806 fishcried    4u  unix 0x0000000000000000      0t0 72370396 socket
tmux    63806 fishcried    5u  unix 0x0000000000000000      0t0 72370397 socket
...
```

当在系统上执行了该命令后，会输出一大堆东西，而且不一定会像上面那样规整，我做了整理，这样可以更好的多输出进行说明。

> lsof输出格式为: COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME

| 字段　   | 说明　                                                      |
|----------|-------------------------------------------------------------|
| COMMAND  | 进程名,默认最多显示前９个字符，如果要显示全，需要参数指定　 |
| PID      | 进程ID号                                                    |
| USER     | 进程归属用户                                                |
| FD       | 文件描述符,看不懂就去差手册，多差几遍就记住了               |
| TYPE     | 类型, IPv4/6, DIR,LINK　                                    |
| DEVICE   | 设备号                                                      |
| SIZE/OFF | 文件大小                                                    |
| NODE     | inode号　                                                   |
| NAME     | 文件名称　                                                  |

> 还是将manual中关于FD的说明直接放在这里吧

```
 FD         is the File Descriptor number of the file or:

                 cwd  current working directory;
                 Lnn  library references (AIX);
                 err  FD information error (see NAME column);
                 jld  jail directory (FreeBSD);
                 ltx  shared library text (code and data);
                 Mxx  hex memory-mapped type number xx.
                 m86  DOS Merge mapped file;
                 mem  memory-mapped file;
                 mmap memory-mapped device;
                 pd   parent directory;
                 rtd  root directory;
                 tr   kernel trace file (OpenBSD);
                 txt  program text (code and data);
                 v86  VP/ix mapped file;

            FD is followed by one of these characters, describing the mode under  which
            the file is open:

                 r for read access;
                 w for write access;
                 u for read and write access;
                 space if mode unknown and no lock
                      character follows;
                 `-' if mode unknown and lock
                      character follows.

            The  mode character is followed by one of these lock characters, describing
            the type of lock applied to the file:

                 N for a Solaris NFS lock of unknown type;
                 r for read lock on part of the file;
                 R for a read lock on the entire file;
                 w for a write lock on part of the file;
                 W for a write lock on the entire file;
                 u for a read and write lock of any length;
                 U for a lock of unknown type;
                 x for an SCO OpenServer Xenix lock on part      of the file;
                 X for an SCO OpenServer Xenix lock on the      entire file;
```



## 如果作为专家去使用lsof

lsof可以看做是一个搜索器,输入搜索条件,返回对应打开的文件.所以使用lsof主要就是掌握怎么输入条件.更高级一点就是按照lsof提供的高级语法来让加速lsof.这个工具真的是只做一件事,做就做到极致!

> 1. lsof的过滤词一般支持`^`(取反),`-`(区间),`,`(列表)操作
> 2. 两个过滤词可以通过-a选项来表示必须同时满足
> 3. 同时指定关键词,表示or的关系

下面只列出比较常用的选项:

**1. 通过文件名查看**

- `lsof filename`
- `lsof -d FD` FD可以是文件的fd,也可以是类型
- lsof +d /usr/local
- lsof +D /usr/local

**进程**

- lsof -c abc 通过进程名
- lsof -p pid 通过pid来查看

**2. 通过归属来查看**

- lsof -u user

**3. 过滤socket**

- `lsof -i [46][protocol][@hostname|hostaddr][:service|port]`

## lsof高级用例

**定位端口占用问题**

```
$ sudo lsof -i :9901
COMMAND     PID USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
docker-pr 21624 root    4u  IPv6 45110837      0t0  TCP *:9901 (LISTEN)
```

**定位卸载失败问题**

```
$ sudo lsof /home/fishcried
COMMAND   PID      USER   FD   TYPE DEVICE SIZE/OFF     NODE NAME
zsh      1331 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
sudo     4341      root  cwd    DIR    8,1     4096 17563675 /home/fishcried
lsof     4342      root  cwd    DIR    8,1     4096 17563675 /home/fishcried
lsof     4343      root  cwd    DIR    8,1     4096 17563675 /home/fishcried
zsh     25971 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
zsh     27921 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
vim     34631 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
zsh     54945 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
tmux    57913 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
zsh     63773 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
tmux    63806 fishcried  cwd    DIR    8,1     4096 17563675 /home/fishcried
```

**恢复被删除的文件**
