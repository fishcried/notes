# Linux procfs

## 内存

- meminfo
- slabinfo
- vmstat
- zoneinfo
- buddyinfo

**/proc/meminfo**


```
MemTotal:        3955012 kB  #可用内存大小,物理内存减去一些预留与内核二进制代码大小
MemFree:         2068536 kB  #为使用的内存大小.
MemAvailable:    2616712 kB 
Buffers:           89828 kB
Cached:           674260 kB
SwapCached:            0 kB
Active:          1112724 kB
Inactive:         610856 kB
Active(anon):     960484 kB
Inactive(anon):    75084 kB
Active(file):     152240 kB
Inactive(file):   535772 kB
Unevictable:          16 kB
Mlocked:              16 kB
SwapTotal:       8178684 kB
SwapFree:        8178684 kB
Dirty:                16 kB
Writeback:             0 kB
AnonPages:        959548 kB
Mapped:           128668 kB
Shmem:             76072 kB
Slab:              90824 kB
SReclaimable:      58180 kB
SUnreclaim:        32644 kB
KernelStack:        3640 kB
PageTables:        26112 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:    10156188 kB
Committed_AS:    3254572 kB
VmallocTotal:   34359738367 kB
VmallocUsed:      575780 kB
VmallocChunk:   34359147064 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       76540 kB
DirectMap2M:     4014080 kB

```

**/proc/swaps**

```
Filename			Type	  	Size	  Used	Priority
/dev/sda5     partition	8178684	0	    -1
```


## cpu与调度

**/proc/cpuinfo**

**/proc/interrupts**

**/proc/stat**

包含了系统启动后的统计信息

```

#    user   nice sys     idle     iowait irq sfirq steal guest
cpu  24058  26   5832    456366   32060   0  78     0    0     0 #各个cpu总的统计
cpu0 6831   4    1476    114318   6732    0  32     0    0     0 #每一个cpu单独的统计
cpu1 5837   8    1530    110794   11432   0  26     0    0     0
cpu2 7177   7    1775    112476   7998    0  13     0    0     0
cpu3 4212   6    1050    118776   5896    0  6      0    0     0
intr  ...                                                        # 中断
ctxt 2497808                                                     # 上下文切换次数
btime 1415795241                                                 # 启动到现在的时间,秒
processes 4941                                                   # 自启动以来创建的任务数
procs_running 5                                                  # 当前运行队列的任务数
procs_blocked 0                                                  # 被族塞的任务数
softirq 961758 16120 143581 42120 1476 30621 0 492301 59744 456 175339
```

**/proc/uptime**


```
#启动时间 空闲时间
1939.39 7066.73
```

## IPC

**/proc/locks**

```
#NO 类型   xxx       xxx   PID  锁定的文件     开始区域   结束区域
                                主:次:inode   
1:  POSIX  ADVISORY  READ  4572 08:01:57672021 1073741826 1073742335
2:  POSIX  ADVISORY  READ  4572 08:01:57672536 128 128
3:  POSIX  ADVISORY  READ  4572 08:01:57671824 1073741826 1073742335
4:  POSIX  ADVISORY  READ  4262 08:01:57672290 128 128
5:  POSIX  ADVISORY  READ  4262 08:01:57671737 1073741826 1073742335
6:  POSIX  ADVISORY  READ  4207 08:01:57672290 128 128
7:  POSIX  ADVISORY  READ  4207 08:01:57671737 1073741826 1073742335
8:  POSIX  ADVISORY  WRITE 4332 08:01:3670020 0 EOF
9:  POSIX  ADVISORY  WRITE 2894 00:0f:12359 0 0
10: POSIX  ADVISORY  WRITE 2718 00:0f:12335 0 EOF
11: POSIX  ADVISORY  READ  4572 08:01:57672371 128 128
12: POSIX  ADVISORY  READ  4572 08:01:57671830 1073741826 1073742335
13: POSIX  ADVISORY  WRITE 4572 08:01:57671810 0 EOF
14: FLOCK  ADVISORY  WRITE 2762 00:0f:8057 0 EOF
15: POSIX  ADVISORY  READ  4572 08:01:57672724 128 128
16: POSIX  ADVISORY  READ  4572 08:01:57671855 1073741826 1073742335
```

## 磁盘

**/proc/diskstats**
**/proc/partitions**硬盘分区信息

```
major minor  #blocks  name

   8        0  976762584 sda
   8        1  968581120 sda1
   8        2          1 sda2
   8        5    8178688 sda5
  11        0    1048575 sr0
```

**/proc/mounts**

## 设备

**/proc/devices**

**/proc/misc** 杂项设备,主设备10上注册的设备

```
#次设备号 设备名
237 loop-control
130 watchdog
 57 freefall
 58 rfkill
 59 mei
232 kvm
234 btrfs-control
236 device-mapper
 60 network_throughput
 61 network_latency
 62 cpu_dma_latency
227 mcelog
  1 psaux
228 hpet
231 snapshot
184 microcode
 63 vga_arbiter
```

## 内核信息

- cmdline 内核启动参数
- modules
- sys 内核参数,可以进行调整

**/proc/modules**
加载的模块

```
...
mfd_core 12601 2 lpc_ich,rtsx_pci, Live 0xffffffffa0044000
...
usb_common 12440 1 usbcore, Live 0xffffffffa0000000

```

# 进程信息

## 进程

- `cwd`     指向当前进程的工作目录.
- `cmdline` 启动当前进程的完整命令，但僵尸进程目录中的此文件不包含任何信息
- `environ` 进程的环境变量
- `exe`     指向当前进程二进制文件
- `fd`      当前进程打开的文件.`ls -l fd`看一下
- `fdinfo`  与fd对应,打开权限
- `root`    进程的根目录
- `limits`  进程限制
- `task`    线程

## cpu


## 内存

- statm
- stat
- status
- map
- smap

## 文件系统

- io

# 参考资料

- [/proc 文件系统](http://man.ddvip.com/linux/Mandrakelinuxref/proc-fs.html)
- [使用/sys文件系统访问Linux内核](http://www.ibm.com/developerworks/cn/linux/l-cn-sysfs/)
