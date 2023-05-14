# git subtree 命令
## 添加子项目
```
git subtree add --prefix=存放子项目的相对路径 子项目git地址 分支 --squash
```
例如：
```
git subtree add --prefix=src/subtree https://github.com/yys-0505/subtree.git master  --squash
```
## 修改子项目
在原项目中直接commit，无需其他特殊配置，建议子项目代码单独commit，不要跟外围代码一起提交
## 推送子项目
```
git subtree push --prefix=存放子项目的相对路径 子项目git地址 分支
```

例如：
```
git subtree push --prefix=src/subtree https://github.com/yys-0505/subtree.git master
```

问题:
subtree push实际上是遍历本工程每一次提交，把提交文件涉及到subtree目录的挑出来，同步到subtree工程，如果提交有很多，遍历提交的过程有严重的性能问题

spilt命令可以解决这个问题

## 拉取子项目
```
git subtree pull --prefix=存放子项目的相对路径 子项目git地址 分支 --squash
```

例如：
```
git subtree pull --prefix=src/subtree https://github.com/yys-0505/subtree.git master --squash
```

## git subtree split
```
git subtree split --rejoin --prefix=存放子项目的相对路径 --branch 本地临时分支名称
git push subtree地址 本地临时分支名称:远程分支
```

例如：
```
git subtree split --rejoin --prefix=src/subtree  --branch subtreeSplitBranch
git push https://github.com/yys-0505/subtree.git subtreeSplitBranch:master
```

# 注意事项
- 遇到问题：fatal:working tree has modifications. Cannot add --- 解决：add, pull subtree之前要commit当前工程的修改
- subtree提交后, 要提交父工程, 这样其他人pull父工程可以拿到最新的subtree
- 更新subtree后, 也要提交父工程, 其他人pull父工程可以拿到最新的subtree
- 第一次提交subtree可能会慢, 从第二次开始正常

# 其他
- --squash参数表示不拉取历史信息，而只生成一条commit信息。是否使用 squash 都是可以的， 但需要在开始阶段作出选择，并一直坚持下去 。如果一会儿用一会儿不用，得到的不是两者的优点，而是两者的缺点之和。
在使用 --squash 参数的情况下， subtree add 或者 pull 操作的结果对应两个 commit， 一个是 Squash 了子项目的历史记录， 一个是 Merge 到主项目中。
如果不使用 --squash 参数，子项目更新的时候，subtree pull 很顺利， 能够自动处理已解决过的冲突，缺点就是子项目的更新记录“污染”了主项目的。
- git subtree -h 查看命令
- If you do all your merges with '--squash', don't use
'--rejoin' when you split, because you don't want the
subproject's history to be part of your project anyway. (https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt)
- 为了方便, 把部分命令放到package.json, 需将`scripts`中`st:xxx`开头的命令, 和`config`中`st-`开头的配置复制到需要的工程, 日常会用到3个命令：
1. npm run st:add - 将subtree添加到当前工程
2. npm run st:pull - 在当前工程更新subtree
3. npm run st:push - 将当前工程subtree的改动提交到远程仓库