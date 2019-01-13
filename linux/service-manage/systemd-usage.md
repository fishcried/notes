# linux systemd

# 启动分析

```
systemd-analyze
systemd-blame
```

分析启动速度

# systemctl

```
systemctl
systemctl list-units
systemctl --failed
systemctl status xxx
systemctl start xxx
systemctl stop xxx
systemctl retart xxx
systemctl reload xxx
```


- failed 
    - greenbone-security-assistant.service
    - openvas-manager.service
    - openvas-manager
    - openvas-scanner

- slow
    - thin.service


# 变更记录

| Why                       | Who       | When       |
|---------------------------|-----------|------------|
| 创建文件,提醒日后完善内容 | fishcired | 2015-08-21 |
