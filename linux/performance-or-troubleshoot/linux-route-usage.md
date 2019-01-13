# route使用说明

```
route [-CFvnee]
route  [-v]  [-A family] add [-net|-host] target [netmask Nm] [gw Gw] [metric N] [mss M] [window W] [irtt I] [reject] [mod] [dyn] [reinstate] [[dev] If]
route  [-v] [-A family] del [-net|-host] target [gw Gw] [netmask Nm] [metric N] [[dev] If]
```

- add:添加一条新路由。
- del:删除一条路由。
- -net:目标地址是一个网络。
- -host:目标地址是一个主机。
- netmask:当添加一个网络路由时，需要使用网络掩码。
- gw:路由数据包通过网关。注意，你指定的网关必须能够达到。
- metric：设置路由跳数。

**Flags**

- U 路由被启用。
- H 目标是一个主机
- G 使用网关。

# 举例

```
    route add -net 127.0.0.0 netmask 255.0.0.0 dev lo
    route add -net 192.56.76.0 netmask 255.255.255.0 dev eth0
    route del default
    route add default gw mango-gw
    route add -net 192.57.66.0 netmask 255.255.255.0 gw ipx4
    route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0
    route add -net 10.0.0.0 netmask 255.0.0.0.0 reject
```

# 路由匹配原理

**动态路由**

**静态路由**

**默认路由**

# 变更记录

|Why | Who | When |
|----|-----|------|
|创建文件,提醒日后完善内容|fishcired|2015-02-12 |
