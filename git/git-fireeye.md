#  练就火眼金睛 


<!-- vim-markdown-toc GFM -->
  * [status](#status)
  * [diff](#diff)
* [显示5小时内的历史记录](#显示5小时内的历史记录)
* [显示五小时前最后的一个记录](#显示五小时前最后的一个记录)
* [(sha1,sha2)区段的历史记录](#sha1sha2区段的历史记录)

<!-- vim-markdown-toc -->

diff, status, log.

##  status

`git status`显示状态.`git status -sb`SB一点.显示分支信息,并将状态信息简化.

- -s表示用精简方式
- -b同时显示当前工作分支的名称

其中标识有两列，拿状态M来说

1. 第一列含义是：版本库中的文件与处于中间状态——提交任务（提交暂存区，stage）中的文件相比有改动
2. 第二列含义是：工作区当前的文件与处于中间状态——提交任务（提交暂存区，stage）中的文件相比有改动

## diff

       git diff [options] [<commit>] [--] [<path>...]
       git diff [options] --cached [<commit>] [--] [<path>...]
       git diff [options] <commit> <commit> [--] [<path>...]
       git diff [options] <blob> <blob>
       git diff [options] [--no-index] [--] <path> <path>

![](/img/git-diff.png)

```
    工作区     暂存区             仓库
    ----------------------------------
    |            |                   |
    | `git diff` |                   |
    |------------|                   |
    |            |`git diff --cached`g
    |            |-------------------|
    | `git diff HEAD`                |
    |--------------------------------|
    ```

##  日志查询

`git log`默认不用任何参数的话，会按时间列出所有的更新，最新的更新安排在最上面. 每次更新
都有一个SHA-1校验,作者名字邮件和提交时间，以及提交说明.

```
commit 7ce5cf4e0217e2c5d202af20b0fae2b325f9b459
Author: fishcried <wangtq@neunn.com>
Date:   Tue Dec 6 17:05:13 2016 +0800

    Fix packages version in requirements.txt

    refs: https://releases.openstack.org/liberty/index.html

    Change-Id: Ib5432f275b4b9733666711df7c223e7b1b08f63c

```

### git log常用选项


| 选项             | 功能                       |
|------------------|----------------------------|
| -p               | 查看差异,diff              |
| -n               | 查看最近的n次提交          |
| <since>..<until> | since与until之间的提交     |
| --graph          |                            |
| --stat           | 代码审查比较方便           |
| --pretty=xxx     | oneline/short/format/email |
| --author | 过滤提交者 |
| --since | |
| --before | |

### git log指定范围查找

**时间范围**

```
# 显示5小时内的历史记录
git log --since="5 hours"

# 显示五小时前最后的一个记录
git log --before="5 hours" -1
```

**提交之间**

```
# (sha1,sha2)区段的历史记录
git log sha1...sha2
```

> 两种操作符供参考:
> 1. `^`: 相当于回溯一个版本, sha1^就表示sha1之前的个版本;sha1^^ 相当于sha1^2
> 2. `~N`; 回溯N个版本, sha1~1相当于sha1的父节点

### git log统计代码行举例

```bash
git log --author="$(git config --get user.email)"  --pretty=tformat: --numstat --since="2016-05-20" | awk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "added lines: %s removed lines : %s total lines: %s\n",add,subs,loc }' -  
```
