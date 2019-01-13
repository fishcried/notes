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