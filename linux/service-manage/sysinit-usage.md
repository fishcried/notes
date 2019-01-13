# sysinit

- rcS.d 必要执行的服务
- rc1.d 单机维护
- rc3.d 
- rc5.d

# upstart

- /etc/init

服务配置文件结构:

```
# 注释区 
description  "xxx xxx"
author "fishcried <fishcried@163.com>"

start on runlevel [!2345]
# 失败重试
respawn 

pre-start script
    正常的shell指令即可
end script

exec ...
```

服务管理命令 

- start
- stop
-

# 更多阅读

1. [linux初始化init系统系列](http://www.ibm.com/developerworks/cn/views/linux/libraryview.jsp?sort_by=&show_abstract=true&show_all=&search_flag=&contentarea_by=Linux&search_by=浅析+Linux+初始化+init+系统&topic_by=-1&type_by=所有类别&ibm-search=搜索)
1. [upstart把应用封装成系统服务](http://blog.fens.me/linux-upstart/)
1. [浅析Linux初始化init系统（1）：sysvinit](http://blog.jobbole.com/85076/)
1. [浅析Linux初始化init系统（2）：UpStart](http://blog.jobbole.com/85107/)
1. [浅析Linux初始化init系统（3）Systemd](http://blog.jobbole.com/85070/)
