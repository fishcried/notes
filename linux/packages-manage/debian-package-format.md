# Debian说明

> 总结的补全，后续需要补充

## 需要的开发工具

| 工具名                          | 用途                          |
|---------------------------------|-------------------------------|
| build-essential                 | 构建环境所需的工具链          |
| autoconf,automake,autotools-dev | 处理configure脚本和Makefile的 |
| debhelper,dh-make               |                               |
| devscripts                      |                               |
| fakeroot                        | 以不同用户模拟root用户环境    |
| file                            |                               |
| git                             |                               |
| lintian                         | Debian软件包检查工具          |
| pbuilder                        | 创建和维护chroot环境工具                              |


## Debian软件包制作流程

1. 获取一份软件拷贝，通常为tar格式. 例如`package-version.tar.gz`
2. 在上游源码的debian目录中添加Debian打包专用文件
  1. package_version.orgi.tar.gz
  2. package_version-revision.debian.tar.gz
  3. package_version-revision.dsc
3. 用Debian源码包构建Debian二进制文件



> 注意: 在 Debian 软件包的文件名中，分隔 package 和 version 的字符从 tarball 名称中的 - (连字符)换成了 _ (下划线)。 

上面根据Debian Policy将package这个部分替换为package name,将version替换为upstream version, 将revisoin这个部分替换为Debian revision

## 包名称和版本

## debian目录

| 重要      | 作用 |
|-----------|------|
| control   |      |
| copyright |      |
| changelog |      |
| rules     |      |

### control

参见[手册4.1](https://www.debian.org/doc/manuals/maint-guide/dreq.zh-cn.html)

### copyright

### changelog

```
glance (2014.1.5-1) unstable; urgency=low

  * Initial release (Closes: #nnnn)  <nnnn is the bug number of your ITP>

  -- wangtq <ubuntu@neutron-pkg.novalocal>  Thu, 15 Dec 2016 07:25:02 +0000
```

### rules

**Target**



| Target                 | 作用                                                                                                              |
|------------------------|-------------------------------------------------------------------------------------------------------------------|
| clean target           | 清理所有编译的、生成的或编译树中无用的文件。(必须)                                                                |
| build target           | 在编译树中将代码编译为程序并生成格式化的文档。(必须)                                                              |
| build-arch target      | 在编译树中将代码编译为依赖于体系结构的程序。(必须)                                                                |
| build-indep target     | 在编译树中将代码编译为独立于平台的格式化文档。(必须)                                                              |
| install target         | 把文件安装到 debian 目录内为各个二进制包构建的文件树。如果有定义，那么 binary* target 则会依赖于此 target。(可选) |
| binary target          | 创建所有二进制包(是 binary-arch 和 binary-indep 的合并)。(必须)                                                   |
| binary-arch target     | 在父目录中创建平台依赖(Architecturany)的二进制包。(必须)                                                          |
| binary-indep target    | 在父目录中创建平台独立(Architectureall)的二进制包。(必须)                                                         |
| get-orig-source target | 从上游站点获得最新的原始源代码包。(可选)                                                                          |


> 当想执行target的时候就将target作为参数执行即可.
> debian/rules build
> fakeroot make -f debian/rules binary


### package.cron

- package.cron.hourly
- package.cron.daily
- package.cron.weekly
- package.cron.monthly
- package.cron.d

### package.init和package.default

- package.init 会被安装到/etc/init.d/package
- package.default /etc/default/package

### install

如果标准的make install没有安装的文件,可以把文件名和目录路径写入install文件

```
src/bar /usr/bin
```

### patches


## 构建软件包

构建软件包必须要安装以下包:

- build-essential
- Build-Depends
- Build-Depends-indep

在源码包目录中执行一下命令`dpkg-buildpacage -us -uc`

- debian/rules clean 清除源代码树
- dpkg-source -b 构建源代码包
- debian/rules build 构建程序
- fakeroot debian/rules binary 构建二进制包
- 制作.dsc 
- 用dpkg-genchanges 制作.changes文件

### 手动构建glance软件包

**1. 下载源码**


**2. 设置dh_make**

```
export DEBMAIL="wangtq@neunn.com"
export DEBFULLNAME="wangtq"
```

**3. 初始化外来Debian软件包**

dh_make生成debian目录


## 检查软件包


### 校验软件包的安装过程

```
sudo debi xxx.changes
```

### 检查maintainer scripts

```
# remote
sudo dpkg -r xxx
# Purge
sudo dpkg -P xxx
# install
sudo dpkg -i xxx.deb
```

### debdiff命令

```
debdiff old-package.dsc new-package.doc
```

## 更新软件包
