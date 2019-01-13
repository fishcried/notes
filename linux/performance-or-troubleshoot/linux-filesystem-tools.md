# df  report file system disk space usage

针对的是文件系统,去读分析系统的superblock信息,速度非常快.鸟瞰的作用.

| 参数 | 说明                                                 |
|------|------------------------------------------------------|
| -a   | 列出所有文件系统,包括系统特有/proc等文件系统         |
| -k   | 以KBytes容量显示各文件系统                           |
| -m   | 以MBytes容量显示各文件系统                           |
| -h   | 以人们较易阅读的GBytes, MBytes, KBytes等格式自行显示 |
| -H   | 以 M=1000K 叏代 M=1024K 癿迚位方式                   |
| -T   | 连同该partition的filesystem 名称(例如 ext3)也列出    |
| -i   | 不用硬盘容量,而以inode的数量来显示                   |


# du estimate file space usage

| 选项 | 说明                                                        |
|------|-------------------------------------------------------------|
| -a   | 列出所有档案与目彔容量,因为默讣仅统计目彔底下癿档案量而已。 |
| -h   | 以人们较易读的容量格式 (G/M) 显示                           |
| -s   | 列出总量而已,而不列出每个各别目彔占用容量                   |
| -S   | 不包括子目彔下的总计,不 -s 有点差别。                       |
| -k   | 以KBytes列出容量显示                                        |
| -m   | 以MBytes列出容量显示                                        |


# dumpe2fs


# fdisk manipulate disk partion table

管理分区的工具

# mkfs.xxx 格式化

# fsck,badblocks 磁盘检查

# 磁盘的挂在与卸载

```
mount [-t 文件系统] [-L Label 名] [-o 额外选顷] [-n] 装置文件名 挂载点
mount -o remount,rw,auto /
```

# mknod

```
mknod 装置文件名 [bcp] [Major] [Minor]
```
