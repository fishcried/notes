patch其实是一个差异文件,保存了目标在两个时间点的差异细节.如果时刻A是文件的v1版本,时刻B是你对v1的一个bug修改时刻.
你不必将时刻B的所有文件都传给管理员,只需要把patch文件上传即可.对方可以通过patch文件快速的把问题修复.patch的好处就是:

1. 能够直接看到变更内容,方便审理
2. 数据传输量小

协同开发时,patch是非常重要的.


# patch的格式

**unix/linux**

**git**

  1. 包含作者,时间等信息.
  2. 多个patch,一个节点一个

# 生成patch


    git diff > patch
    git diff --cached > patch
    git diff branchname --cached > patch

**git format-patch**

- -s 添加作者签名信息

    git format-patch A B
    git format-patch -n A
    git format-patch HEAD^
    git format-patch -M master
    git format-patch -s 4e16
    git format-patch -1

**`git send-mail`**

# 应用patch

**git apply**

    git apply --check patch
    git apply --stat newpatch.patch

**git am**

    git am  newpatch.patch