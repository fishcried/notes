# 使用apt-mirror搭建本地源

1. apt-get原理，目录
2. apt-mirror建立同步源
3. reporepo手动创建源

## 安装apt-mirror

```
apt-get install apt-mirror
```


## 配置

```
cat /etc/apt/mirror.list
set base_path /var/spool/apt-mirror
set skel_path $base_path/skel
set var_path $base_path/var
set cleanscript $var_path/clean.sh

set defaultarch amd64
set nthreads 20
set _tilde 0

deb xxxx trusty main restricted universe multiverse

clean xxx
```

## 开始同步

```
apt-mirror
```

# 参考文档

- [deb打包手册](http://blog.csdn.net/michaelwubo/article/details/40588059)
- [reprepro构建本地源](http://www.laxjyj.com/view-htm-tid-165612-cid-49.html)
