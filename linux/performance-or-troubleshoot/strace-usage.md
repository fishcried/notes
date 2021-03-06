# 使用strace定位系统疑难杂症

> todo:
> 1. strace到底是什么，能干什么
> 2. strace每个参数最佳场景
> 3. -e 分类已经使用案例

`strace`是个好东西,值得花几个小时研究.回报会非常大.

- 发行版基本都会默认安装,是个基础工具
- strace可以快速窥探程序运行原理
- strace可以诊断性能.通过strace的统计信息,时间信息对性能分析很有帮助.
- strace是调试利器

以下列举下我曾经遇到的情况:

**1.内存不足问题定位**

 一次发布前夕,新程序总是崩溃,提示信息为内存不足(系统16G内存).可是更新代码的同学说没有大内存操作.strace跟踪后发现有大量的`system("cp ....")`操作,最后导致失败推断为system内使用fork创建新进程导致内存翻倍.最后可用内存不足.之后所有使用system的地方全部改写了,并重新封装一个函数较vsystem,内部使用vfork.问题解决.

 **2. sudo 命令执行非常慢问题定位**

 使用openstack创建了几个虚拟机,登陆虚拟机后发现执行`sudo ...`命令 超级慢,需要等待分钟的级别.strace摆上,一切无所遁形.最后发现问题是sudo命令会解析主机名,而`/etc/hosts`没有相应配置.结果sudo命令进行了dns请求.最后超时返回.

 以上两个问题定位可能有其他的思路,但是没有`strace`,问题分析可能需要一点时间.

# 1.使用方式

```
usage: strace [-dffhiqrtttTvVxx] [-a column] [-e expr] ... [-o file]
        [-p pid] ... [-s strsize] [-u username] [-E var=val] ...
        [command [arg ...]]
   or: strace -c -D [-e expr] ... [-O overhead] [-S sortby] [-E var=val] ...
        [command [arg ...]]
```

# 2.常用参数

- 获取帮助
	- -h 输出简要的帮助信息.
- 性能调优
	- -c 统计每一系统调用的所执行的时间,次数和出错的次数等. 
	- -r 打印出相对时间关于每一个系统调用.
	- -T 显示每一调用所耗的时间.
	- -t 在输出中的每一行前加上时间信息.
- 内容显示
	- -x 以十六进制形式输出非标准字符串.
	- -xx 所有字符串以十六进制形式输出.
	- -o file 讲输出信息写到file中
- 高级级定制
	- -e expr 指定一个表达式,用来控制如何跟踪.
- 其他
	- -f 跟踪由fork调用所产生的子进程.
	- p pid 加载已经启动的进程
	- i  打印入口指针,便于gdb调试

# 3.高级定制

```
	[qualifier=][!]value1[,value2]...
```

> 高级定制其实用的不多,但有的时候真的需要.因为strace跟踪系统调用,会有大量的信息
输出,当方向明确时,可以有效的进行信息过滤.qualifier的值只能是trace,abbrev,
verbose,raw,signal,read,write.

- trace
	- trace=set 指定系统调用`trace=read,open,write`
	- trace=file 跟踪与文件相关的系统调用.
		- 等价与`trace=open,stat,chmod,unlink,...`
	- trace=network 跟踪网络相关的系统调用
	- trace=signal 跟踪信号相关的系统调用
	- trace=ipc IPC相关
	- trace=desc 与文件描述符相关的系统调用
- abbrev
	- abbrev=set
- verbose
	- verbose=set
- raw
	- raw=set 指定系统调用的参数以十六进制显示
- signal
	- signal=set `signal=!SIGIO`
- read
	- read=set `read=3,5`
- write
	- write=set `write=5`


# 4.推荐阅读

- [使用strace,ltrace寻找故障原因的线索(较详细)](http://blog.csdn.net/delphiwcdj/article/details/7387325)
- [7 Strace Examples to Debug the Execution of a Program in Linux(能够找点感觉)](http://www.thegeekstuff.com/2011/11/strace-examples/)
- [anti-strace(反调试相关)](http://www.nsfocus.net/index.php?act=magazine&do=view&mid=2467)
