# linux内存不足时问题定位


## 查看全局状况

**free**

buffer/cache swap 内存区别

**/proc/meminfo**

```
[root@CNSZ045043 neutron]# cat /proc/meminfo 
MemTotal:        3882704 kB
MemFree:          114788 kB
MemAvailable:      86684 kB
Buffers:              64 kB
Cached:            70832 kB
SwapCached:        20996 kB
Active:          2431900 kB
Inactive:         958376 kB
Active(anon):    2400340 kB
Inactive(anon):   922888 kB
Active(file):      31560 kB
Inactive(file):    35488 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       4063228 kB
SwapFree:             40 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:       3298748 kB
Mapped:            13760 kB
Shmem:              3848 kB
Slab:             151804 kB
SReclaimable:      45684 kB
SUnreclaim:       106120 kB
KernelStack:        6944 kB
PageTables:        87504 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     6004580 kB
Committed_AS:    8148468 kB
VmallocTotal:   34359738367 kB
VmallocUsed:      166948 kB
VmallocChunk:   34359506580 kB
HardwareCorrupted:     0 kB
AnonHugePages:    210944 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:      106432 kB
DirectMap2M:     4087808 kB
```

**当cache特别多的时候**

```
echo 3>/proc/sys/vm/drop_caches
```

## 找出具体进程


top命令

- M 内存
- C 命令全
- P cpu
- T 时间


```
ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user,uid' | grep oracle |  sort -nrk5
```

## 分析进程段

pmap

/proc/pid/maps
/proc/pid/smaps
