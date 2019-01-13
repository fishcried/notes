# Git Submodule使用

**添加submodule**

```
git submodule add git@xxx.git
```

> 该命令会产生一个.gitmodules文件

**第一次使用更新**

```
git submodule update --init --recurisive
git submodule foreach git checkout master
```

**更新子模块**

```
cd submodulename
git pull origin master
```


**更新所有子模块**

```
git submodule update --init --recursive
```

**克隆子模块**

```
git clone --recursive git@xxx.git
```

**删除子模块**

```
# Remove configurations in .gitmodule
# Remove configurations in .git/config
git rm <SubModuleName> --cached
git sync
```


