# 网络资源

## 整体网络流量状况查看

**ifstat**

```
ifstat 
```

**sar**

```
sar -n DEV 1 30
sar -n EDEV 1 30
```

**iptraf**

**bmon**
比较详细的全局观

> sar功能更加强大,能够查看错误数据，也能够查看历史数据.

## 通过session查看去查看流量数据

**iftop**
iftop可以查看流量具体的session，知道流量数据到底是什么.

```
iftop
```

**tcptrack**

**ss\/netstat**

## 进程角度查看

**nethogs**

Net top tool grouping bandwidth per process

## 链路连通

* mtr [使用 MTR 诊断网络问题](https://meiriyitie.com/2015/05/26/diagnosing-network-issues-with-mtr/?utm_source=tuicool&utm_medium=referral)
* traceroute
* ping

## 数据包分析

**tcpdump**
**wireshare**
**tcpflow**



# 参考文章

- [Linux System Administration Basics](https://www.linode.com/docs/tools-reference/linux-system-administration-basics/)


