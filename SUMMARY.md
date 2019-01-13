# Summary

* [笔记简介](README.md)
* 运维开发
  * SaltStack
    * [saltstack: 一 试水](devops/saltstack1.md)
    * [SaltStack: 二 远程执行](devops/saltstack2.md)
    * [SaltStack: 三 配置管理](devops/saltstack3.md)
    * [SaltStack: 四 配置管理之程序员视角](devops/saltstack4_.md)
  * Ansible
    * [Ansible: 一 Try it](devops/ansible-quick-guide.md)
    * [Ansible: 二 主机管理](devops/ansible-inventory.md)
    * [Ansible: 三 常用配置与命令行使用](devops/ansible-configs.md)
    * [Ansible: 四 使用Playbooks](devops/how-to-write-ansbile-playbooks.md)
    * [Ansible: 五 编写Ansible Role](devops/ansible-roles.md)
    * [Ansible: 六 Ansible常用模块](devops/ansible-common-modules.md)
    * [Ansible: 七 Ansible FQA](devops/ansible-tips.md)
* 常用工具
    * [curl命令使用](tools/curl-usage.md)
* Linux系统
    * [Linux常见问题FQA](linux/linux-fqa.md)
    * 软件包管理
      * [Debian包格式说明](linux/packages-manage/debian-package-format.md)
      * [构建deb软件仓库](linux/packages-manage/build-deb-packages.md)
      * [搭建ubuntu本地源](linux/packages-manage/ubuntu-deb-package-usage.md)
      * [ubuntu下软件包管理](linux/packages-manage/ubuntu-package-tools.md)
    * 开启启动与服务管理
      * linux开机启动
      * [systemd](linux/service-manage/systemd-usage.md)
      * [sysinit](linux/service-manage/sysinit-usage.md)
      * [ubuntu开机启动优化](linux/service-manage/ubuntu-boot-tuning.md)
      * [ubuntu开机服务管理](linux/service-manage/ubuntu-boot-manage.md)
    * 安全
      * [防火墙：玩转iptables](linux/iptables-tips.md)
      * [gpg使用](linux/gpg-usage.md)
      * [ssh使用](linux/linux-ssh-usage.md)
    * 进程
      * [工具: ps命令使用](linux/performance-or-troubleshoot/ps-usage.md)
    * 网络
      * [工具: ss](linux/performance-or-troubleshoot/linux-ss-usage.md)
      * [工具: nc](linux/performance-or-troubleshoot/linux-nc-usage.md)
      * [工具: wireshark](linux/performance-or-troubleshoot/linux-wireshark-usage.md)
      * [工具:tcpdump](linux/performance-or-troubleshoot/linux-tcpdump-usage.md)
      * [工具:ip](linux/performance-or-troubleshoot/linux-ip-usage.md)
      * [工具:route](linux/performance-or-troubleshoot/linux-route-usage.md)
      * [工具:dig](linux/performance-or-troubleshoot/linux-dig-usage.md)
      * [工具:网卡bond](linux/performance-or-troubleshoot/linux-bond-usage.md)
      * [工具:wget](linux/performance-or-troubleshoot/linux-wget-usage.md)
      * [工具:vlan](linux/performance-or-troubleshoot/linux-vlan-usage.md)
    * 磁盘
      * [工具: iotop命令使用](linux/performance-or-troubleshoot/iotop-usage.md)
      * [工具: lsof使用](linux/performance-or-troubleshoot/lsof-usage.md)
      * [工具: 文件系统相关命令使用](linux/performance-or-troubleshoot/linux-filesystem-tools.md)
    * 纵览
      * [工具: ulimit](linux/performance-or-troubleshoot/linux-ulimit-usage.md)
      * [最大文件数限制(一):原理上没有多大的事](linux/performance-or-troubleshoot/linux-max-fileno-limit.md)
      * [工具: sar](linux/performance-or-troubleshoot/linux-sar-usage.md)
      * [工具: top](linux/performance-or-troubleshoot/linux-top-usage.md)
      * [工具: glances](linux/performance-or-troubleshoot/linux-glances-usage.md)
      * [工具: htop](linux/performance-or-troubleshoot/linux-htop-usage.md)
    * 跟踪
      * 工具: perf
      * 工具: systap
      * [工具: strace命令使用](linux/performance-or-troubleshoot/strace-usage.md)
* Linux性能调优与问题定位
    * [性能优化: 方法论](linux/performance-or-troubleshoot/linux-tuning-model.md)
    * [性能优化: 资源使用方法论方法论](linux/performance-or-troubleshoot/linux-resource-glances.md)
    * [性能概览: Linux Proc文件系统](linux/performance-or-troubleshoot/linux-procfs.md)
    * [工具: linux性能工具概览](linux/performance-or-troubleshoot/linux-performance-tools.md)
    * [性能概览: 工具一览](linux/performance-or-troubleshoot/linux-procfs.md)
    * [性能概览: 工具一览](linux/performance-or-troubleshoot/linux-tuning-tools.md)
    * [压力测试: iozone](linux/performance-or-troubleshoot/iozone-usage.md)
    * [压力测试: sysbench](linux/performance-or-troubleshoot/sysbench-usage.md)
    * [压力测试: unixbench](linux/performance-or-troubleshoot/unixbench-usage.md)
    * [CPU性能调优： CPU调优思路](linux/performance-or-troubleshoot/linux-cpu-tuning.md)
    * [内存性能调优： Linux内存模型TODO](linux/performance-or-troubleshoot/linux-memory-model.md)
    * [内存性能调优： Linux内存优化总结](linux/performance-or-troubleshoot/linux-memory-tuning.md)
    * [内存性能调优： faq](linux/performance-or-troubleshoot/linux-memory-faq.md)
    * [网络性能调优： 总结](linux/performance-or-troubleshoot/linux-network-tuning.md)
    * [性能调优: IO](linux/performance-or-troubleshoot/linux-io-tuning.md)
* Git使用指南
    * [git使用指南](git/git-user-guide.md)
    * [Git FAQ](git/git-faq.md)
    * Git工作流
    * [git核心观念原理](git/git-theory.md)
    * [Git基本配置](git/git-config-sample.md)
    * [status/diff/log git下练就火眼金睛](git/git-fireeye.md)
    * [git patch](git/git-patch.md)
    * [git仓库管理](git/git-repo.md)
    * [git branch](git/git-branch.md)
    * [git魔法](git/git-magic.md)
    * [git merge](git/git_merge.md)
    * [git rebase用法](git/git-rebase-usage.md)
    * [git cherry-pick](git/git-cherry-pick.md)
    * [git review](git/git-review-usage.md)
    * [Git Submodule](git/git-submodule.md)
    * [Git参考资源](git/git-docs.md)
    * [防火墙：玩转iptables](linux/iptables-tips.md)
* 系统设计
    * [单点登录与集中权限管理的本质](system-design/the-essence-of-sso-and-pcm.md)
* OpenShift
    * [Openshift架构](openshift/openshift-arch.md)
  * OpenShitf: 1 架构与基本概念
  * OpenShitf: 2 单机环境搭建
  * OpenShitf: 3 集群环境搭建
  * OpenShitf: 4 镜像仓库搭建
  * OpenShitf: 5 与glusterfs进行对接
  * OpenShitf: 6 网络状况
  * OpenShitf: 7 监控系统对接
  * OpenShitf: 8 日志系统对接
  * OpenShitf: 9 恢复与备份
  * OpenShitf: 10 升级
