# 性能观测工具

- top/htop
- vmstat
- iostat
- sar
- hdparm -t
- lsof 
- ulimit 
- /proc/pid/fd/
- blktrace/blkparse


先用全局性能工具确定是否为io问题,然后可以使用iostat进行详细观察,blktrace更为详细.blkparse

# 负载生成工具

- aio-stress
- iozone
- fio



#  **参数调整工具** 

- tune2fs 
- reiserfstune
- jfs_tune


# **选择合适的调度算法** 

- as
- cfq 完全公平调度
- deadline 最后期限 I/O 调度程序
- noop Noop I/O 调度程序采用先入先出（FIFO）调度算法。合并原始块层中的请求，但只是一个最后命中缓存 （last-hit cache）。如果系统与 CPU 捆绑，且使用高速存储，这就是可以使用的最佳 I/O 调度程序。


# 文件系统

## 文件系统调整注意事项

### 格式化选项

- 文件系统块大小
- RAID
- 外部日志

### 挂在选项

- barries
- 访问时间

**分区顺序**

- 序号越小的分区越靠近盘外,所以访问频率较高的分区最好序列号越小
- 经常变动的数据，单独放一个分区，较小碎片

TODO:我怎样能图形化分区那


**是否需要交换分区**

需要的话设置swappines参数


```bash
cat /sys/block/sdb/queue/scheduler
echo 500 > /sys/block/sdb/queue/iosched/read_expire
echo 1000 > /sys/block/sdb/queue/iosched/write_expire
```

**合适的文件系统**

包括日志格式或者关闭

**noatime,nodirtime**

```
/etc/fstab noatime
```

**使用内存文件系统作为日志系统**

```
ramlog
wget http://www.tremende.com/ramlog/download/ramlog_2.0.0_all.deb
sudo dpkg -i ramlog_2.0.0_all.deb

TMPFS_RAMFS_SIZE=100m
```

**提高请求队列长度**

**ulimit**

增加文件系统描述符
增加进程数


# 参考记录

- [Linux 性能优化之 IO 子系统](http://liaoph.com/linux-system-io/)
