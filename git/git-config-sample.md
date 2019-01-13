> 可以通过`git config --list`来查看当前的配置, 更多可以查看`git config --help`.

# 通用配置
```
git config --global  user.name "name"
git config  --global user.email "name@example.com"
git config  --global core.editor vim
git config  --global core.pager ''
git config  --global color.ui true
# 解决中文名乱码问题
git config --global core.quotepath false
git config  --global merge.tool vimdiff
```
# `.gitignore`文件配置

*ignore的语法*

```
    # 注释
    *.a			# 忽略所有.a扩展名的文件
    !lib.a		# lib.a除外.
    /TODO		# 忽略当前目录下的TODO文件,子目录TODO不忽略
    buid/		# 忽略build目录下的文件 
    doc/*.txt	# 忽略doc下的.txt文件,但是子目录不忽略
    ```

# commit模板配置

```
git config --global commit.template $HOME/.gitmessage.txt
cat $HOME/.gitmessage.txt

subject line
what happened
[ticket: X]
```

# 解决冲突配置

- The local-checkin that your git tree has: LOCAL
- The head of the remote repository (that is going to be merged): REMOTE
- common ancestor to both LOCAL and REMOTE: BASE
- The file that will be written as a result: MERGED


*配置文件的级别*

- `/et/gitconfig` 对应--system
- `~/.gitconfig` 对应--global
- `$GIT_DIR/config` 

**这三个文件的影响范围是从整体到特殊的，特殊的配置会覆盖其上层配置**
