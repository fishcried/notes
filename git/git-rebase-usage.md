# git rebase用法


用于分支合并

```
$ git checkout -b mywork origin
```

![](http://gitbook.liuhui998.com/assets/images/figure/rebase0.png)

```
$ vi file.txt
$ git commit
$ vi otherfile.txt
$ git commit
```
但是与此同时，有些人也在"origin"分支上做了一些修改并且做了提交了. 这就意味着"origin"和"mywork"这两个分支各自"前进"了，它们之间"分叉"了。


![](http://gitbook.liuhui998.com/assets/images/figure/rebase1.png)

在这里，你可以用"pull"命令把"origin"分支上的修改拉下来并且和你的修改合并； 结果看起来就像一个新的"合并的提交"(merge commit):


**git merge**

![](http://gitbook.liuhui998.com/assets/images/figure/rebase2.png)



**git rebase**

```
$ git checkout mywork
$ git rebase origin
```

![](http://gitbook.liuhui998.com/assets/images/figure/rebase3.png)

![](http://gitbook.liuhui998.com/assets/images/figure/rebase4.png)


在rebase的过程中，也许会出现冲突(conflict). 在这种情况，Git会停止rebase并会让你去解决 冲突；在解决完冲突后，用"git-add"命令去更新这些内容的索引(index), 然后，你无需执行 git-commit,只要执行:

```
$ git rebase --continue
```


# 参考文档

- http://blog.csdn.net/hudashi/article/details/7664631/
- http://blog.chinaunix.net/uid-27714502-id-3436706.html