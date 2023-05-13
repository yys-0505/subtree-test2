# git subtree 命令
## 添加子项目：
```
git subtree add --prefix=存放子项目的相对路径 子项目git地址 分支 --squash
```
例如：
```
git subtree add --prefix=src/subtree https://github.com/yys-0505/subtree.git master  --squash
```
## 修改子项目代码
在原项目中直接commit，无需其他特殊配置，建议子项目代码单独commit，不要跟外围代码一起提交
## 推送子项目代码 push
命令：
```
git subtree push --prefix=存放子项目的相对路径 子项目git地址 分支 --squash
```

例如：
```
git subtree push --prefix=src/subtree https://github.com/yys-0505/subtree.git master
```

问题:
subtree push实际上是遍历本工程每一次提交，把提交文件涉及到subtree目录的挑出来，同步到subtree工程，如果提交有很多，遍历提交的过程是有严重的性能问题的

spilt命令可以解决这个问题

## 拉取子项目最新代码 pull
命令：
```
git subtree pull --prefix=存放子项目的相对路径 子项目git地址 分支 --squash
```

例如：
```
git subtree pull --prefix=src/subtree https://github.com/yys-0505/subtree.git master --squash
```

## 其他 git subtree split
命令：
```
git subtree split --rejoin --prefix=存放子项目的相对路径 --branch temp
git push subtree地址 本地分支:远程分支
```

例如：
```
git subtree split --rejoin --prefix=src/subtree  --branch subtreeSplitBranch
git push https://github.com/yys-0505/subtree.git subtreeSplitBranch:master
```

# 注意事项
- pull subtree之前要commit当前工程的修改
- subtree提交后, 要提交父工程, 然后其他人pull父工程可以拿到最新的subtree
- 更新subtree后, 也要提交父工程, 然后其他人pull父工程, 可以拿到最新的subtree
