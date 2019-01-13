# 1.开机启动过程

## 1.1 基础知识

运行级别(通过runlevel获取):

- 0 停机状态 `init 0`快速关机
- 1 root单用户维护状态
- 2-5 多用户(3为字符界面,5为图形)
- 6 重启 `init 6`重启

**Debain中2-5没有区别,就是没有字符界面**

## 1.2 开机启动过程

1. 读取MBR信息，启动Boot Manager，Linux通常使用GRUB作为Boot Manager。
2. 加载系统内核，启动init进程。init进程是Linux的根进程，所有的系统进程都是它的子进程。
3. init进程读取/etc/inittab文件中的信息，并进入预设的运行级别。在这里需要说下的是，在ubuntu的6.10版本
   以后，就没有了/etc/inittab文件，是因为inittab已经被update软件包所取代了，具体的可以查看
   /usr/share/doc/update目录。就不在这里介绍了。
4. 执行/etc/rcS.d/目录下的脚本，然后是/etc/rcX.d/目录下的脚本，X代表的是数字0～6。rcS.d和rcX.d目录下
   的文件都是以，S或K加上两位数字组成的，其中S代表start，K代表kill，而两位数字代表启动顺序，数字越大
   代表级别越低。

```
    /etc/inittab -> /etc/rc.sysint(/etc/rc.d/rc.sysinit) -> /etc/rc[?].d(/etc/rc.d/rc[?].d)->/etc/rc.local(/etc/rc.d/rc.local)

```

# 2.管理开机启动

## 2.1 `/etc/rc.local`

## 2.2 桌面开机启动

## 2.3 sysv-rc-conf

sysv-rc-conf使用非常简单.有点傻瓜式.记住几个操作就可以了.而且还支持鼠标点击.这东西简单好用,只是不能
进行脚本操作,指定优先级等.

| 快捷键  | 功能
|---------+------
| 空格    | 选择
| 方向键  |  移动
| ctrl+N  | 下一页
| ctrl+P  | 上一页
| q   |  退出

![sysv-rc-conf](/img/sysv-rc-conf.png)

## 2.4 update-rc.d

	man update-rc.d
	
	NAME
	       update-rc.d - install and remove System-V style init script links
	
	SYNOPSIS
	       update-rc.d [-n] [-f] name remove
	       update-rc.d [-n] name defaults [NN | SS KK]
	       update-rc.d   [-n]   name   start|stop  NN  runlevel  [runlevel]...   .
	              start|stop NN runlevel [runlevel]...  . ...
	       update-rc.d [-n] name disable|enable [ S|2|3|4|5 ]
	OPTIONS
	       -n     Don't do anything, just show what we would do.
	       -f     Force removal of symlinks even if /etc/init.d/name still exists.

**1. 例子**

	# 添加默认启动
	  update-rc.d foobar defaults
	
	# 指定优先级和level，注意后面的.
	  update-rc.d foobar start 20 2 3 4 5 . stop 20 0 1 6 .
	  update-rc.d foobar start 30 2 3 4 5 . stop 70 0 1 6 .
	  update-rc.d script_for_A defaults 80 20
	  update-rc.d script_for_B defaults 90 10
	
	# 移除开机启动
	  update-rc.d foobar remove
	  update-rc.d -f foobar remove
	
	# stop
	  update-rc.d foobar stop 20 2 3 4 5 .
	  update-rc.d foobar start 45 S . stop 31 0 6 .
	  update-rc.d foobar stop 45 S .
