# 1. 为什么使用git

> 1. "jjjjjjjj",vim内键入了多次'j'，系统没有响应。郁闷的等待几分钟，top一下看到开发服务器上登录了30多个用户，1分钟内的均衡负载达到了9点几(4cpu)。不用想，肯定是有人运行了grep,find,rsync,svn status等
> 2. jjjjjjjj,vim内键入了多次'j'，系统良久无响应。一会同事喊"断网了......"
> 3. svn下一份分支下的文件，保存了几个版本，针对bug修改的，添加了新功能的，有些特别想法的。这个文件每个版本都不能commit.svn加上手动版本管理，这种日子什么时候能结束那

# 2. 工欲善其事必先利其器

`git config`用于配置git，良好的配置会达到事半功倍的效果。

## 2.1 配置存在哪里

有三个文件存放git的配置

+ `/et/gitconfig` 对应--system
+ `~/.gitconfig` 对应--global
+ `$GIT_DIR/config` 

很容易看出来这三个文件的影响范围是从整体到特殊的，特殊的配置会覆盖其上层配置。

## 2.2 最基本的配置就是邮箱与名字

		git config --global user.name "name"
		git config --global user.email "name@example.com"

## 2.3 忽略文件

	# 注释
	*.a			# 忽略所有.a扩展名的文件
	!lib.a		# lib.a除外.
	/TODO		# 忽略当前目录下的TODO文件,子目录TODO不忽略
	buid/		# 忽略build目录下的文件 
	doc/*.txt	# 忽略doc下的.txt文件,但是子目录不忽略

## 3.4 常用配置

	git config --global core.editor vim
	git config --global merge.tool vimdiff
	git config --global core.pager ''
	git config --global color.ui true
	git config --list #查看配置信息
	git config --help #获取帮助

# 4. 常用操作

## 4.1 仓库操作

	git init 
	git init --bare 
	git clone url

## 4.2 添加与提交

	git add <filename>
	git add/rm * 
	git commit -m "commit message" <filenames> 
	# 以上只是提交到本地,git push后才是提交到远程仓库
	
	# 提交到网络服务器
	git push origin master 
	
	# 快速提交
	git commit -a -m "commit comment"
	
	# 查看已经缓存的内容
	git diff --cached

## 4.3 移动文件

	git rename file rfile
	git commit -m "mesage" rfile

## 4.4 状态查看

`git status`显示文件状态,但是输出内容过于人性,不是很简洁.我常常使用`alias gitst=git status -sb`来代替.`-s`是使用精简格式.`-b`是输出分支信息.

精简格式的输出每行如下"**`XY PATH1->PATH2`**".

- X表示版本库与暂存区中文件状态的比较.
- Y表示暂存区与当前工作空间文件状态的比较.

状态标志如下:

+ ' ' = unmodified
+ M	= modified
+ A = added
+ D = deleted
+ R = renamed
+ C = copied
+ U = updated but unmerged

## 4.5 日志查看

	git log 
	git log --pretty=oneline
	# 这个比较直观一点
	git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
	# 查看每一次版本大致变动情况
	git log --stat --summary
	# 详细查看特定变更
	git show nnnn
	# 当前最新变更
	git show HEAD
	# 关于版本号的制定这里有一些语法糖，可以让操作更加便利
	git show 7623^
	git show 7623^^
	git show 7623~3
	
	# 显示patch
	git log -p

## 4.6 撤销修改

![](/img/git_stage.png)

	# 想丢弃本地修改时如下,该命令会使用HEAD中的最新内容替换掉你的工作目录中的文件。添加到缓冲区的改动不受影响的。
	git checkout <filename>
	git checkout hash #跳到一个旧状态
	
	# 放弃提交的修改
	git reset --hard origin/master
	
	# 修改上次提交的注释内容
	git commit --amend
	
	git reset HEAD #master目录树替换暂存区内容
	
	git rm --cached <file> #直接删除暂存区的文件
	
	git checkout . #暂存区覆盖工作去
	
	git checkout HEAD . #master覆盖index，工作去

## 4.7 Alias

	#from .gitconfig
	[alias]
		co = checkout
		ci = commit
		st = status
		br = branch
		hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
		type = cat-file -t
		dump = cat-file -p
	
	#from .bashrc
	alias gs='git status '
	alias ga='git add '
	alias gb='git branch '
	alias gc='git commit'
	alias gd='git diff'
	alias go='git checkout '
	alias gk='gitk --all&'
	alias gx='gitx --all'
	
	alias got='git '
	alias get='git '

## 4.8 Git的Tag

一般是软件发布新版本时会打一下tag。

## 4.9 Git的分支管理

### 4.9.1 本地分支

	# 1 分支管理
	git branch #列出所有分支
	git branch -v #查看各个分支最后一个提交的对象的信息
	git branch --merge
	git branch --no-merge
	# 2  切换分支
	git checkout testing #切换到该分支
	
	# 3  删除分支
	#删除已经被合并的分支
	git branch -d testing
	
	#强制删除分支
	git branch -D testing
	
	# 4  合并分支
	git merge testing
	
	# 5 撤销一个合并
	git reset --hard HEAD
	
	git reset --hard ORIG_HEAD
	
	# 6 解决冲突
	#手动修改,然后标记他们为合并成功
	git add <filename>
	
	# 7 创建分支
	git branch testing # 创建分支
	git checkout testing #切换到该分支
	
	git checkout -b iss53 #相当于以上两条命令

### 4.9.2 远程分支管理
	
	git ls-remote	 # 查看远程分支有哪些
	git brance -r	 # 查看远程分支
	
	git pull 					#抓取远程仓库所有分支合到本地
	git fetch orgin				#抓取远程仓库更新
	git merge origin/master		#将远程主分支合并到本地当前分支
	git checkout --track origin/branch #跟踪远程某分支，创建相应的本地分支
	git checkout -b <local_branch> origin/<remote_branch> #基于远程分支创建本地分支，功能其实同上
	
	git push					# push所有分支
	git push origin master		# 将本地主分支推送到远程主分支
	git push -u origin master	# 将本地主分支推动到远程，无远程主分支时创建，用于初始化
	git push origin <local_branch> # 创建远程分支
	git push 
	git clone url
	git remote add name url
	git push (远程仓库名) (分支名)

## 4.10 远程仓库管理

	git remote -v
	git remote rename new-remote user2

## 4.11 备份本地仓库

	git archive --format=zip -o backup.zip HEAD

## 4.12 diff

	# Workspace vs index
	git diff  
	
	# Workspace vs tree
	git diff HEAD
	git diff master
	
	# index vs tree
	git diff --cached
	git diff --cached HEAD

## 4.13 stash

	git stash list
	git stash
	git stach pop
	git stash clear
