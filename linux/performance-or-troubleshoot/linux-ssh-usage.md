# 1. ssh基础

## 1.1 ssh原理

SSH协议是建立在应用层和传输层基础上的安全协议，其主要由以下三部分组成，共同实现SSH的安全保密机制：

- 传输层协议:
   该协议提供诸如认证、信任和完整性检验等安全措施，此外还可以任意地提供数据压缩功能。通常情况下，这些传输层协议都建立在面向连接的TCP数据流之上。
- 用户认证协议层
  用来实现服务器的跟客户端用户之间的身份认证，其运行在传输层协议之上。
- 连接协议层
  分配多个加密通道至一些逻辑通道上，它运行在用户认证层协议之上。

ssh有客户端和服务端组成,有两个大版本,相互不能兼容.1.x & 2.x

## 1.2 ssh常用选项

## 1.3 ssh服务端常用配置项

# 2. ssh使用技巧

## 2.1保持连接

## 2.2别名配置

```
cat .ssh/config
Host me
  HostName 127.0.0.1
  User	root
  Port 2222
```


## 2.3端口转发

## 2.4 跳转

```
ProxyCommand ssh gateway netcat -q 600 %h %p
```

## 2.5 无密码自动登陆

```
ssh-keygen 
ssh-copy-id -i /path/id_rsa.pub user@host
```

## 共享链接

```
ControlMaster auto
ControlPath /tmp/ssh_mux_%h_%p_%r
```

# 3.ssh安全

1. 调整端口号
  通过配置文件进行修改`Port xxx`.
1. 使用秘钥进行认证
1. 使用版本2
1. 禁止root用户
  `PermitRootLogin no`
1. 修改端口大于1024
1. 创建一个虚拟用户
1. 使用iptables与tcp wrapper双重保护
  `host.allow`,`hosts.deny`
