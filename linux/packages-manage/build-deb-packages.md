# DEB包构建

## Debian的软件包命名方式

`<package name>_<version> deb`


## apt-get命令

| 参数 | 帮助                         |
|------|------------------------------|
| -h   | 帮助                         |
| -d   | 只下载,不安装或者解压        |
| -f   | 即便完整性检查失败了依然继续 |
| -s   | 不做什么，只是按照顺序模拟   |
| -y   | 所有问题假设为Yes            |
| -u   | 心事一系列已经要更新的包     |

> 包或下载到本地的/var/cache/apt/archives目录

| 功能项目  | 命令  |
|------|------------------------------|
| 清除无用的软件包   | `apt-get clean/autoclean` clean清除所有下载的包，autoclean清除不需要的                         |
| 显示软件包版本   | apt-show-versions pkg        |
| 搜索想要查找的包   | apt-cache search package |
| 获取常规信息   | apt-cache showpkg package |
| 查看依赖关系   | apt-cache  |
| 包最后一次更新做了什么   | apt-listchanges |
| 获取源码包 | apt-get source package |
| 下载附加包 | apt-get build-dep pkg |


## 软件源

仓库中目录包括dist,pool两个目录:

1. dist 存储软件包的相关信息，源码包的相关信息
2. pool 按照字母顺序存所有deb包的文件以及源码包文件

## 软件源工具

### apt-mirror

镜像工具，不能修改

### reprepro创建本地软件仓库

目录结构:

1. conf repepro的配置目录
2. db 仓库配置文件，发布时隐藏
3. dists 索引目录
    1. main 完全的自由软件
    2. restricted 不完全的自由软件
    3. universe ubuntu官方不提供支持与补丁，全靠社区支持
    4. muitiverse 非自由软件
    5. Release 存储components全部package,source,release文件的md5,保证数据完整性

#### reprepro软件仓库管理

**添加deb到仓库**

```
reprepro -Vb -C components -p priority includedeb codename /home/download/*.deb
```

**添加src到仓库**

```
reprepro -Vb -C main  includesrc  olivaia/*.dsc
```

**删除软件**

```
reprepro -vb remove -C main raring adduser
```

**查询**

```
reprepro -vb list raring adduser
```


# 参考文档

1. [Debian新维护者手册](https://www.debian.org/doc/manuals/maint-guide/index.zh-cn.html)
