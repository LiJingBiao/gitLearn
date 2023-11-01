# gitLearn
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

