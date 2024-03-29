gitLearn

## 跳过暂存区，直接提交工作目录中所有改变的文件

```
git commit -a -m "提交消息"
# 通过创建一个新的提交，以替换当前分支的前端。所代表的含义就是在最新一次提交的基础上进行提交
git commit --amend -m "提交消息"
```

## 拉取远程分支

```
git fetch origin main 
```

## 远程分支合并本地分支

```
git merge origin/main
```

如果报错`fatal: refusing to merge unrelated histories`使用下面指令

```shell
/**
出现 "fatal: refusing to merge unrelated histories" 错误通常是由于两个不相关的 Git 仓库（例如，一个全新的本地仓库和一个包含提交历史的远程仓库）尝试进行合并操作。
这种情况下，Git 默认会拒绝合并操作，因为它认为这两个仓库的提交历史没有共同的祖先，无法简单地进行合并。
通过添加 --allow-unrelated-histories 选项，您可以告诉 Git 允许合并这两个不相关的历史。然后，您可以手动处理任何合并冲突，确保合并后的内容符合预期。
*/
git merge origin/main --allow-unrelated-histories
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
# 丢弃工作区的修改
git checkout -- README.md
# 切换到master分支
git checkout master 
# git checkout -- file 是用来丢弃工作区(working directory)对文件file的修改。这会将文件file恢复到最后一次git commit或git add时的状态。
# git checkout file 主要用于切换分支。它会将文件file切换到指定分支上的版本
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

## 从git暂存区恢复文件

```
git restore --staged file1.txt
恢复暂存区中的所有文件。
git restore --staged . 
```

## git stash使用

```
# 贮藏
git stash save stash_name
# 使用贮藏
git stash pop stash@{<stash_id>}
# 应用最新的 stash 更改并从 stash 列表中删除
git stash pop
# 查看当前的 stash 列表
git stash list
# 应用最新的 stash 更改但不删除它
git stash apply
# 查看 stash 中的更改内容
git stash show

```

## git命令重命名

```
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch

git config --global alias.mg merge
git config --global alias.lg log
git config --global alias.ps push
git config --global alias.pl pull

git config --global alias.ad add
git config --global alias.df diff  
git config --global alias.rs reset
git config --global alias.rm remote

git config --global alias.fe fetch
git config --global alias.rb rebase
git config --global alias.tg tag
git config --global alias.sh stash
```

文件最后会写到`~/.gitconfig`

```
[alias]
	st = status
	co = checkout
	ci = commit
	br = branch
	mg = merge
	lg = log
	ps = push
	pl = pull
	ad = add
	df = diff
	rs = reset
	rm = remote
	fe = fetch
	rb = rebase
	tg = tag
	sh = stash
```

## git更新远程分支

```
git remote update origin -p
git fetch -p
```

## git要将某个文件还原到特定的提交，您可以使用以下命令：

```
git checkout <commit-hash> -- <file-path>
```



## [git教程](https://github.com/geeeeeeeeek/git-recipes/wiki/)



## github配置了ssh无法clone的问题

在配置了代理之后，会出现ssh无法连接github的情况（猜测是因为防火墙会拒绝来自代理服务器的SSH连接）

[官方解决方案链接](https://docs.github.com/zh/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)

这时候应该尝试使用HTTPS端口建立的SSH连接。

要测试通过HTTPS端口的SSH是否可行

```text
$ ssh -T -p 443 git@ssh.github.com
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

端口为443的主机名为`ssh.github.com`

此时克隆仓库的方式为

```text
git clone ssh://git@ssh.github.com:443/YOUR-USERNAME/YOUR-REPOSITORY.git
```

很麻烦，但可以通过覆盖SSH设置来强制与[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)的任何连接均通过上面验证成功的服务器和端口进行。

一劳永逸

需要在`~/.ssh/config`中编辑内容如下

```text
Host github.com
    Hostname ssh.github.com
    Port 443
    User git
```

可以再次测试到[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)的连接进行测试

```text
$ ssh -T git@github.com
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```























