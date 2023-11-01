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

