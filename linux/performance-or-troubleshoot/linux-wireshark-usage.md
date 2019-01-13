# wireshark实用技巧

# 安装

```
sudo apt-add-repository ppa:wireshark-dev/stable
sudo apt-get update
```

> for ubuntu16.04


# 六个包延迟定位法

```

   	A						      B
		--------SYN------->
		<-------SYN/ACK---- 线路延迟
		--------ACK------->

		--------HTTP GET--> 客户端延迟
		<-------ACK-------- 线路延迟

		--------POST------> 服务器延迟

```

# IO图

常用曲线

- tcp.analysis.lost_segment: 丢包
- tcp.analysis.duplicate_ack: 重复确认
- tcp.analysis.retransmission: 重传
- tcp.analysis.window_update: 通常通过该图形能判断接收断的负载
- tcp.analysis.bytes_in_flight: 
- tcp.analysis.ack_rtt: 查看网络延迟
