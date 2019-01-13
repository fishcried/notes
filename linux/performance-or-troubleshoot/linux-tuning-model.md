# 性能调优方法论

# 性能调优到底要干什么?

**性能调优指标**

1. 响应时间
  从用户操作到系统给用户以正确反馈的时间
2. Transaction Per Second
  每秒处理的事务数

**性能调优目标**

优化响应时间，提高TPS

**优化方式**

+ 降低执行时间
  + 缓存
  + 优化存储类型
  + 算法优化
  + 逻辑优化
  + 需求优化
+ 同步改异步
+ 提前或延迟操作


# 全局观测工具

- [Linux性能调优工具图谱](/2014-12-14/linux_tuning_tools/)
- [使用sar收集系统性能数据 ](/2014-12-15/linux_sar_usage/)
- [sysbench性能测试 ](/2015-06-16/next/sysbench/)
- [文件系统基准测试: iozone ](/2015-06-16/next/iozone_usage/)
- [linux系统性能概览工具(一): top ](/2014-12-15/top_usage/)
- [linux系统性能概览工具(二): htop ](/2015-06-08/htop_usage/)
- [linux系统性能概览工具(三):glances ](/2015-06-08/glances_usage/)



# linux系统优化具体点

## linux调度优化

### 常用工具

鸟瞰工具:`vmstat`,`sar`,`iostat -c`

### 调度系统的因素

- Context Switch
- Run Queue
- Cpu Utilization
- Load Average
- 上下文切换
- 终端次数
- iowait
- system
- user
- load
- cpu utilization
- runable processes
- blocked
- context switch

### 相关文章

- [Cpu bindings (一) 理解cpu topology ](/2015-01-09/cpu_topology/)


## linux内存优化

### 常用工具

- free
- proc
    - meminfo
    - pid/status
    - pid/statm
    - pid/maps
    - pid/smaps
- vmstat

### 可以调整的内核参数

- /proc/sys/vm/dirty_background_ratio 脏数据什么时候写到硬盘
- /proc/sys/vm/dirty_expire_centisecs 脏数据在物理内存逗留时间 ms单位
- /proc/sys/vm/swappiness swap分区使用衡量

## I/O调度器

###  工具

- sar -d
- iostat -d 

### 调整的内核参数

- 调度算法
- page size
- block size

## 网络子系统

### 工具

- ping
- netstat -i 

### 调整项目

- MTU
- 增加缓存
    - net.ipv4.tcp_rmem tcp读缓存
    - net.ipv4.tcp_wmem tcp写缓存
- 禁用window_scaling net.ipv4.tcp_dinwow_scaling=0
- ipv4.tcp_tw_reuse=1 ipv4.tcp_tw_recyle=1 tcp可重用性
- ipv4.tcp_keepalive_time=1800
- ipv4.tcp_max_syn_backlog=4096
- 绑定tcp类型的终端到一个cpu上

**一些限制**

```
# ipc
# 共享内存段最大尺寸 1G
kernel.shmmax = 214783648
# 共享内存段最大数量
kernel.shmmin = 4096
# 共享内存总量,单位为页 一下为8G
kernel.shmall = 2087152
kernel.sem = 250 32000 100 128
# 文件描述符
fs.file-max=393322
```

**具体项目**

```
##############################################
# icmp
##############################################

net.ipv4.icmp_echo_ignore_broadcast=1
net.ipv4.icmp_ignore_bogus_error_responses=1
#net.ipv4.icmp_ignore_all = 1

##############################################
# ip
##############################################

net.ipv4.ip_local_port_range 

##############################################
# tcp
##############################################

# 缓存
sys.net.ipv4.tcp_mem

# 系统套接字缓冲区 接收
net.core.rmem_default
net.core.rmem_max = 8388608
# 系统套接字缓冲区 发送
sys.net.core.wmem_default
sys.net.core.wmem_max = 8388608

# tcp 发送接收缓存 最小值 初始值 最大值
net.ipv4.tcp_rmem="4096 87380 8388608"
net.ipv4.tcp.wmem="4096 87380 8388608"

# socker buffer初始最大值
sys.net.core.optmem_max

# 防止syn flood, 延迟数据结构创建
#net.ipv4.tcp_syncookies 1

net.core.somaxconn=102400

net.ipv4.tcp_sack=0
net.ipv4.tcp_dsack=0

# 第二次握手重新发送次数
net.ipv4.tcp_synack_retries = 3
# 半连接
net.core.netdev_max_backlog= 102400
net.ipv4.tcp_max_syn_backlog= 102400
net.ipv4.tcp_abort_on_overflow = 1

# 重传最大次数
net.ipv4.tcp_retries2 = 9

# 利用timewait状态的链接
net.ipv4.tcp_tw_reuse = 1
#net.ipv4.tcp_tw_recycle = 1
net.ipv4.tcp_timestamps=0

# 四次握手优化
net.ipv4.tcp_fin_timeout = 30
# TIME_WAIT状态的连接数
net.ipv4.tcp_max_tw_buckets = 4096

# 保活机制调优
net.ipv4.tcp_keepalive_time = 1800
net.ipv4.tcp_keepalive_invel = 30
net.ipv4.tcp_keepalive_probes = 3



# 滑动窗口
net.ipv4.tcp_window_scalling=0

# 安全
net.ipv4.conf.eth0.accept_source_route=0
net.ipv4.conf.lo.accept_source_route=0
net.ipv4.conf.default.accept_source_route=0
net.ipv4.conf.all.accept_source_route=0

net.ipv4.conf.eth0.secure_redirects=1
net.ipv4.conf.lo.secure_redirects=1
net.ipv4.conf.default.secure_redirects=1
net.ipv4.conf.all.secure_redirects=1

net.ipv4.ipfrag_low_tresh = 262144
net.ipv4.ipfrag_high_tresh = 393216
```

**transmit queue length**

```
ifconfig eth1 txqueuelen 2000
```

# 参考资源

- [Linux 下网络性能优化方法简析](http://www.ibm.com/developerworks/cn/linux/l-cn-network-pt/#toggle)
- [Linux TCP/IP 协议栈调优](http://colobu.com/2014/09/18/linux-tcpip-tuning/)
- [使用四种框架分别实现1百万websocket常连接的服务器](http://www.udpwork.com/item/14378.html)

# 拓展阅读

- [浅谈Linux优化及安全配置(1)](http://os.51cto.com/art/200907/133990.htm)
- [Linux 2.6.31内核优化指南](http://os.51cto.com/art/201003/190616.htm)
