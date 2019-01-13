# ubuntu 包工具

- dpkg   dpkg is a tool to install build remove and manage debian packages
- apt-get  front tools of APT
- aptitude advance tools of APT

```
# search package from the repo
apt-cache search package

# show the info of the package
apt-cache show package

# install packge
apt-get install package [-reinstall]
apt-get -f install
apt-get remove packge [-purge]


apt-get check
```

**The important configuration files**

```
/etc/apt/source.list
/etc/apt/apt.conf
/etc/apt/preferences
/var/cache/apt/archives/partial #packages that are downloading
/var/cache/apt/archives #pacakge download
/var/lib/apt/lists #list info of packges download
/var/lib/apt/lists/partial #details of packages dowloading
```

## DPKG usage

```
dpkg -i package.deb
dpkg -r package
dpkg -p package
depk -L packge #list the relative files of the package
dpkg -l package #show the version
dpkg -unpack packge.deb
dpkg -S keyword
```

## ubuntu software types

- main canonical-support open source softs
- multiverse 各个社区支持
- restricted 有专利限制
- universe 有版权限制


## 更新软件类型

- security
- updates
- proposed pre-release updates
- backport unsupported updates

> `deb|deb-src http://path/to/ubuntu/ ubuntu发行版|发行版民称-更新类型 软件园类型
