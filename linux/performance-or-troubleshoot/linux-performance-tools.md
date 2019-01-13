# Linux下top系列工具

  - top
  - atop
  - htop
  - iotop
  - iftop

## atop


[atop命令详解](http://www.cnblogs.com/bangerlee/archive/2011/12/23/2294090.html)


## slabtop

```
options:
 --delay=n, -d n    每隔n秒刷新信息
 --once, -o         只显示一次
 --sort=S, -s S     按照S排序，其中S为排序标准
 --version, -V      显示版本信息
 --help             显示帮助信息

排序标准
 a: sort by number of active objects
 b: sort by objects per slab
 c: sort by cache size
 l: sort by number of slabs
 v: sort by number of active slabs
 n: sort by name
 o: sort by number of objects
 p: sort by pages per slab
 s: sort by object size
 u: sort by cache utilization
 ```

## iotop

- 左右箭头控制排序
- r反向排序
- o显示有io的进程
- p只显示进程
- a显示iotop启动到目前为止总结

# Linux下stat系列工具

- ifstat
- vmstat
- iostat
- dstat

## dstat命令使用

| 项目      | 参数                                              |
|-----------|---------------------------------------------------|
| cpu       | --cpu /-c, -C; -l                                 |
| mem       | --mem/-m; --page/-g; --swap/s,S; --vmstat/-v      |
| disk      | -d/--disk, -D; --aio; --fs                        |
| net       | -n/--net, -N; --raw;--tcp;--udp;--unix; --socket  |
| interrupt | -i/--int                                          |
| proc      | -p/--proc;                                        |
| ipc       | --ipc                                             |
| lock      | --lock                                            |
| oters     | -t/--time; -y,--sys; -a/-all; -f/--full; --output |
