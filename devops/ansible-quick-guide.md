# Ansible(一) Try it

学习ansible的最好方式就是使用，先别管什么inventory,playbook,module这些。按照安装文档安装，然后try it，一边学一边体验，这样的速度是最快的。当熟悉了之后，想要深入就需要去细读文档了。

下面什么都不会介绍，只是总结下怎么安装，然后try it。

## ubuntu14.04下安装ansible

**方法一: ubuntu下pip安装最新版本**

```
sudo apt-get install libffi-dev
sudo easy_install pip
sudo pip install ansible
```

**方法二: ubuntu下apt-get安装**

```
sudo apt-get install ansible
```

## Try it


```bash
$ mkdir ansible-demo
$ cd ansible-demo

# 建立hosts文件，输入一下内容，ip根据自己的机器进行配置
$ cat hosts 
[demo]
demo-1 ansible_ssh_host=192.168.250.20
demo-2 ansible_ssh_host=192.168.250.66
demo-3 ansible_ssh_host=192.168.250.5
```

> host文件里的主机根据实际情况配置ip,当然还需要打通秘钥登陆。具体可以google或者百度，关键词"ssh 密钥登陆"。

**测试连通性**

```
$ ansible -i hosts demo -m ping
demo-2 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
demo-1 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
demo-3 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

**远程执行命令**

```
$ ansible -i hosts demo -m shell -a "date"
demo-3 | SUCCESS | rc=0 >>
Tue May 17 13:19:49 UTC 2016

demo-1 | SUCCESS | rc=0 >>
Tue May 17 13:19:49 UTC 2016

demo-2 | SUCCESS | rc=0 >>
Tue May 17 13:19:49 UTC 2016

$ ansible -i hosts demo -m shell -a "uptime"
demo-2 | SUCCESS | rc=0 >>
 13:20:06 up  4:45,  0 users,  load average: 0.02, 0.02, 0.05

demo-3 | SUCCESS | rc=0 >>
 13:20:06 up  5:00,  0 users,  load average: 0.00, 0.01, 0.05

demo-1 | SUCCESS | rc=0 >>
 13:20:06 up  5:02,  1 user,  load average: 0.00, 0.01, 0.05

```


## 更近一步的学习

**查看官方文档**

google ansible然后就可以看到官方网站，阅读吧。

**查看程序帮助**

1. ansible的具体使用可以查看其帮助信息`ansible -h`
1. ansible的相关模块可以使用`ansible-doc module_name`来查看,`ansible-doc -l`查看系统模块有哪些。

**多多使用**

文档看的再多，也没有用的多掌握的深入。所以尽情的使用吧，遇到不懂的就去查文档，这样一点点的就什么都掌握了。

比如可以用ansible来维护自己的工作环境。使用ansible自动安装vim，firefox，zsh啥的，肯定比shell用着强点。更进一步的是用ansible来维护自己的生产环境。

慢慢来，一切都会更好的！