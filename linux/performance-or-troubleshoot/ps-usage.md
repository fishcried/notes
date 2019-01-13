```
whatis ps
ps (1)               - report a snapshot of the current processes.
```


# 选项说明

- 进程过滤
    - -e/-A 显示所有进程
    - -a 显示同一终端下的所有程序
    - -d all process except session leaders
    - -C<命令> 列出指定命令的状况
    - -G/g grplist
    - -U/u userlist
    - -p pidlist
    - -s sesslist
    - -t ttylist
- 格式控制
    - -l
    - -e
    - -f


- 项目

| 类别   | 详细                                   | 说明 |
|--------|----------------------------------------|------|
| cpu    | esp,eip,pcpu,class,cgroup              |      |
| signal | block,sig_block,sigmask,caught,pending | s    |
| mem    | rss                                    | v    |
| 传入   | args, comm                             |      |
| 线程   |                                        | -T   |

# 常用命令

```
ps -ef --sort -p[cpu,mem] 
```
