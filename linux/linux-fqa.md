
### 网卡乱序

问题描述: 系统安装完了，发现顺序是乱的.


解决方案:

```
安装biosdevname
```

以后整理吧，这个具体看一下.调整udev rules应该就可以.

### `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!`

问题描述:

```
ubuntu@fishcried:~$ ssh ubuntu@192.168.252.199
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
f5:b1:4c:91:12:0f:22:1c:65:17:b4:63:1c:84:c1:c5.
Please contact your system administrator.
Add correct host key in /home/ubuntu/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/ubuntu/.ssh/known_hosts:22
  remove with: ssh-keygen -f "/home/ubuntu/.ssh/known_hosts" -R 192.168.252.199
  ECDSA host key for 192.168.252.199 has changed and you have requested strict checking.
  Host key verification failed.
  ubuntu@fishcried:~$
```

解决方案:

```
ssh -o "StrictHostKeyChecking no"
```

不用每次都删除，强制不做keycheck


