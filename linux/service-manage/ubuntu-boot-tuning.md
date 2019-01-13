安装 bootchart

查看dmesg

查看服务

- landscape
- zfs-fuse
- 关闭ipv6


# Diable appmorar

```
service apparmor stop
update-rc.d -f apparmor remove
apt-get --purge remove apparmor  -y
```

# Disable ipv6

**sysctl.conf**

```
#tail -f /etc/sysctl.conf
...
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# sysctl -p
```

**kernel**

```
GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disable=1 quiet splash"
```

**modules**

```
/etc/modprobe.d/blacklist
blacklist ipv6
modprobe -a
```
