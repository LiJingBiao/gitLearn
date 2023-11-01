# gitLearn

## 跳过暂存区，直接提交工作目录中所有改变的文件

```
git commit -a -m "提交消息"
```

## 拉取远程分支

```
git fetch origin master 
```

## 远程分支合并本地分支

```
git merge origin/master
```

## 本地分支`develop`合并当前分支

```
git merge develop
```

## 创建分支

```
git checkout -b branchName
# 相当于
git branch branchName
git checkout branchName
```

## 将创建的本地分支与远程分支进行关联

```
git push --set-upstream origin branchName
```

## 查看合并日志

```
git cherry -v
```

## git修改当前分支为main

```
git branch -M main
```

## git 切换到某个tag

```
git checkout -b branch_name tag_name
```

## git放弃未提交的修改

```
git checkout README.md 
```

## 从之前的提交中查看 `hello.py` 文件，你可以使用下面的命令：

```
git checkout a1e8fb5 hello.py
```

## 回滚上次提交

```
git reset --hard HEAD~1
```

## 移除当前目录下未被跟踪的文件

```
# 移除当前目录下未被跟踪的文件。-f（强制）标记是必需的
git clean -f
# 移除未跟踪的文件，但限制在某个路径下。
git clean -f <path>
# 移除未跟踪的文件，以及目录。
git clean -df
```

## 查看日志

```
# 使用默认格式显示完整地项目历史。如果输出超过一屏，你可以用 空格键 来滚动，按 q 退出。
git log
# 用 <limit> 限制提交的数量。比如 git log -n 3 只会显示 3 个提交。
git log -n <limit>
# 将每个提交压缩到一行。当你需要查看项目历史的上层情况时这会很有用。
git log --oneline
# 除了 git log 信息之外，包含哪些文件被更改了，以及每个文件相对的增删行数。
git log --stat
# 显示代表每个提交的一堆信息。显示每个提交全部的差异（diff），这也是项目历史中最详细的视图。
git log -p
# 搜索特定作者的提交。<pattern> 可以是字符串或正则表达式。
git log --author="<pattern>"
# 搜索提交信息匹配特定 <pattern> 的提交。<pattern> 可以是字符串或正则表达式。
git log --grep="<pattern>"
# 只显示发生在 <since> 和 <until> 之间的提交。两个参数可以是提交 ID、分支名、HEAD 或是任何一种引用。
git log <since>..<until>
# 只显示包含特定文件的提交。查找特定文件的历史这样做会很方便。
git log <file>

```

## [git教程](https://github.com/geeeeeeeeek/git-recipes/wiki/)



