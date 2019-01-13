# git merge

```
git config merge.tool vimdiff
git config merge.conflictstyle diff3
git config mergetool.prompt false
```


git mergetool
```
+--------------------------------+
| LOCAL  |     BASE     | REMOTE |
+--------------------------------+
|             MERGED             |
+--------------------------------+
```

# 解决冲突配置



- **LOCAL**
    A temporary file containing the contents of the file on the current branch. 
- **BASE**
    A temporary file containing the common base for the merge. 
- **REMOTE**
    A temporary file containing the contents of the file to be merged. 
- **MERGED**
    The file containing the conflict markers. Git has performed as much automatic conflict resolution as possible and the state of this file is a combination of both LOCAL and REMOTE with conflict markers surrounding anything that Git could not resolve itself. The mergetool should write the result of the resolution to this file
    
    
    
# 参考

- http://vim.wikia.com/wiki/A_better_Vimdiff_Git_mergetool