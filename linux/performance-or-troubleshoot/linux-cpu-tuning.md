# CPU拓扑

** SMP**

SMP（对称多处理器）拓扑允许所有的处理器同时访问内存。然而，由于内存访问权限的共享性和 平等性，固然会迫使所有 CPU 及 SMP 系统序列化的内存访问权限的局限性增加，目前这种情况常 不被接受。因此，几乎所有现代服务器系统都是 NUMA（非一致性内存访问）机器。


**NUMA**

比起 SMP 拓扑，NUMA（非一致性内存访问）拓扑是近来才开发的。在 NUMA 系统中，多个处理 器物理分组至一个 socket。每个 socket 都有一个专用内存区，对该内存进行本地访问的服务器统 称为一个节点。 同一个节点上的服务器能高速访问该节点的存储体，但访问其他节点上的存储体速度就较慢。因 此，访问非本地存储体会造成性能的损失。 考虑到性能损失，服务器执行应用程序时，NUMA 拓扑结构系统中对性能敏感的应用程序应访问同 一节点的内存，并且应尽可能地避免访问任何远程内存。 因此，在调节 NUMA 拓扑结构系统中的应用程序性能时，重要的是要考虑这一应用程序的执行点以 及最靠近此执行点的存储体。 在 NUMA 拓扑结构系统中，/sys 文件系统包含处理器、内存及外围设备的连接信 息。/sys/devices/system/cpu 目录包含处理器在系统中相互连接的详情。 /sys/devices/system/node 目录包含系统中 NUMA 的节点信息以及节点间的相对距离。


## 确定系统拓扑结构

> lscpu,lstopo,numactl --hardware确定cpu拓扑.


这里需要关注:

1. Numa node有几个,如何分布
2. 各级缓存大小
3. socket,core,threads数


**设置cpu亲和性**

```
taskset -p mask pid
```

```
numactl --hardware
```



**numastat**

- numa_hit
- numa_miss
- numa_foreign
- intervalave_hit
- local_node
- other_node


**numad自动均衡numa负载**



# CPU调度

- 调度相关
- 上下文切换


**调度类型**

1. 实时调度
    - SCHED_FIFO 作静态优先调度
    - SCHED_RR SCHED_FIFO 策略的轮循变体
1. 一般调度
    - SCHED_OTHER
    - SCHED_BATCH
    - SCHED_IDLE


**中断优化**


```
cat /proc/interrupts
```


设置/proc/irq/IRQ_NUMBER/smp_affinity


**cpu隔离**

```
isolcpus=2,5-7
```

# 检测工具

- uptime
- vmstat
- mpstat
- ps
- sar
- pidstat
