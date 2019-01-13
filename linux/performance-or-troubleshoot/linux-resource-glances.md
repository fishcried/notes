# 从资源使用角度观察操作系统


<!-- vim-markdown-toc GFM -->
* [什么是操作系统](#什么是操作系统)
  * [CPU资源查看相关维度](#cpu资源查看相关维度)
  * [内存资源相关维度](#内存资源相关维度)
  * [Disk资源相关维度](#disk资源相关维度)
  * [网络资源相关维度](#网络资源相关维度)
* [进程视角](#进程视角)

<!-- vim-markdown-toc -->

## 什么是操作系统

每个子系统需要关注那些信息

从资源角度看，一个系统主要有CPU,Mem,Disk,Net几大资源。附加文件描述符,RPC，锁等。


查看资源限制，最有效的就是`limit`命令. top,atop,htop,sar,glances.这些命令核心收拾读取了`proc`文件系统.

工具上也很有意思，`*stat/*top`，两个系列工具.

| 工具               | 功能                       |
|--------------------|----------------------------|
| uptime             | 最近一段时间系统的负载状态 |
| `dmesg 管道 tail ` | 一些内核问题日志           |
| vmstat 1           |                            |


**基准测试**

| 分类　　　 | 　工具               |
|------------|----------------------|
| CPU        | UnixBench,SysBench   |
| 内存I/O    | Imbench              |
| 文件系统   | Bonnie,SysBench, fio |
| 磁盘       | hdparm               |
| 网络       | iper                 |

SPECvirt_sc2010

### CPU资源查看相关维度

- uptime
- top
- lscpu


### 内存资源相关维度

- free -m

**Memory**

* swpd
  * si
  * so

* free
* buf
* cache

### Disk资源相关维度

- iostat

### 网络资源相关维度

- sar -n TCP,ETCP 1


## 进程视角
