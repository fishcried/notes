# linux sockets监测工具ss

![](/img/ss_statistics.png)

ss是Socket Statistics的缩写,与netstat命令一样用户查看套接字的.但是ss比netstat更加的先进.

1. ss速度更快,ss不再像netstat遍历`/proc/pid`目录获取信息了，而是读取`/proc/net/`,服务器上上规模的sockets时，ss的速度很明显。
2. ss输出的信息更加详细,比如定时器，内存，sockets管理信息等，对调优很有帮助。
3. ss提供的精确的过滤功能,一般人不会用，用的人不一般。


# 像netstat一样使用ss

ss提供了与netstat一样的选项,所以从netstat迁移到ss很平滑.

| 选项     | 含义                                                                |
|----------|---------------------------------------------------------------------|
| -a       | 把listen与not-listen的都显示出来,默认只显示established状态的sockets |
| -l       | only listening                                                      |
| -p       | 显示进行相关信息,ss显示的比较全                                     |
| -n       | 数字形式                                                            |
| -t/u/x/w | tcp/udp/unix/raw                                                    |


**`ss -s`查看sockets分布**

查看当前有多少个sockets连接，每个状态分别是多少,每次了解系统连接时，最先需要的就是了解整体状况.netstat来了:

```

netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) printf("%s\t%d\n",a, S[a])}' |\
        sort -n -k2r,2
```

很nb的样子，可是敲几次试试，所有我就写成了个命令叫`cnstat`，但是调试别的机器时就又很麻烦。

```
$ cnstat
ESTABLISHED     6
SYN_SENT        2
```

最后,学会了`ss`.


```
$ ss -s
TCP:   49 (estab 3, closed 1, orphaned 39, synrecv 0, timewait 0/0), ports 0

Transport Total     IP        IPv6
*         0         -         -
*         RAW       0         0         0
*         UDP       8         8         0
*         TCP       48        48        0
*         INET      56        56        0
*         FRAG      0         0         0
```

如果ss命令搞来搞去感觉很麻烦，请记住`ss -s`.


# 更加精细的输出控制

| 选项 | 含义               |
|------|--------------------|
| -i   | tcp内部详细信息    |
| -e   | socket详细信息     |
| -o   | 定时器信息         |
| -m   | socket内存使用情况 |

todo: 进行实例说明


# NB的过滤功能

**根据state进行过滤**

```
ss state established
```

![](/img/tcp_status.png)


listen, established , syn-sent , syn-recv , fin-wait-1 , fin-wait-2 , time-wait , closed , close-wait , last-ack ,  closing

**根据ip(src/dst)进行过滤**

```
src 192.168.0.1
src 192.168.0/24
dst 192.168.0/24
src 192.168.0/24
```

**根据端口(sport/dport)进行过滤**


```
KEY              OP         value

                 eq         :value
                 neq
dport            ge
sport            gt
                 lt
                 le
```

**ip & port**

```
ss dst www.baidu.com:https
```

**state&ip&port**

```
ss state established  '( dport = :https  and dst  www.baidu.com )'
```

>  **条件之间可以进行`and`,`or`,`not`组合,两边最好用`'()'`封装，或者进行转义**


# 举例

```
# from man manual
# 查看所有tcp sockets
ss -t -a    
# 查看所有udp sockets
ss -u -a
# 源或目的端口为ssh,状态为established的tcp sockets
ss -o state established `( dport = :ssh or sport = :ssh )'
# 打开/tmp/.X11-X11/下文件的unix sockets
ss -x src  /tmp/.X11-unix/*
# 服务器上响应193.233.7/24网段客户端请求(http和https)的sockets，处于fin-wait-1状态
ss -o state fin-wait-1 '( sport = :http or sport = :https )' dst 193.233.7/24
```
