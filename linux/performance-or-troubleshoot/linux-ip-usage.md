# 使用方式

```
ip [option] [动作] [指令]
```


**options**

- -s 显示统计数据

**动作**


| 动作         | 含义                       |
|--------------|----------------------------|
| link         | device的相关设定,mtu,mac等 |
| addr/address | 格外ip的设定               |
| route        | 路由有关                   |

# link

```
ip link set [device] [动作与参数]
```

- show
    显示device内容,-s可以查看统计信息
- set
  - up|down
      启用关闭
  - address
      设置mac
  - name
      设置名称
  - mtu
      修改mtu

# addr

```
ip address [add|del] [ip参数] [dev] [相关参数]
```

- 参数
  - show
  - add|del
    - broadcast
    - label
    - scope

```
ip address show
ip address add 192.168.50.50/24 broadcast 192.168.50.255 dev eth0 label eth0:vbird
ip address del 192.168.50.50/24 dev eth0
```

# route

```
ip route [add|del] [ip或net] [via gateway] [dev]
```

- show
- add|del
    - ip or net
    - via
    - dev
    - mtu

```
ip route show
ip route add 192.168.5.0/24 dev eth0
ip route add 192.168.10.0/24 via 192.168.5.100 dev eth0
ip route add default via 192.168.1.2 dev eth0
```

# 参考

1. https://linux.cn/article-3144-1.html
