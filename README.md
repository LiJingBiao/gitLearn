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
# <new-branch> 是你要创建的新分支的名称。
# <start-point> 是你希望新分支基于的分支或提交。
git checkout -b <new-branch> <start-point>

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
# 查看指定分支日志
git log --oneline master
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
## git cherry-pick使用
```
某段提交移到当前分支
git cherry-pick '88b4687c8e^..7bc7403bcf'
CONFLICT (content): Merge conflict in InternalFramework/SettingStorage.h
解决冲突
git add .
git cherry-pick --continue
```
## 中断 cherry-pick
```
git cherry-pick --abort
```
## git rebase 缩减提交记录
```
#缩减前五条记录
git reabse -i HEAD~5
#进入交互界面
pick 88b4687c8e feat: 合并搜索结果
pick 8cfb053bae feat: 添加搜索输入间隔和延时的ducc配置
pick 7bc7403bcf feat: 修改搜索输入间隔和延时间隔
pick b37be32899 feat: 优化代码
pick 7d3a2081bd feat: 修改配置字段
...

# 修改
pick 88b4687c8e feat: 合并搜索结果
s 8cfb053bae feat: 添加搜索输入间隔和延时的ducc配置   
s 7bc7403bcf feat: 修改搜索输入间隔和延时间隔   
s b37be32899 feat: 优化代码   
s 7d3a2081bd feat: 修改配置字段
保存退出
:wq

git rebase --continue

```






## 修改分支名

在 Git 中，你可以使用 `git branch -m` 命令来修改分支的名称。这个命令既可以在当前分支上使用，也可以在指定的其他分支上使用。

### 修改当前分支的名称

如果你想重命名当前所在的分支，只需使用以下命令：

```sh
git branch -m <new-branch-name>
```

例如，如果你当前在 `old-branch` 分支上，想将其重命名为 `new-branch`：

```sh
git branch -m new-branch
```

### 修改其他分支的名称

如果你想重命名一个非当前所在的分支，需要指定当前名称和新名称：

```sh
git branch -m <old-branch-name> <new-branch-name>
```

例如，将 `old-branch` 重命名为 `new-branch`：

```sh
git branch -m old-branch new-branch
```

### 推送重命名后的分支到远程仓库

重命名本地分支后，你可能还需要更新远程仓库中的分支。可以使用以下步骤：

1. **删除远程旧分支**：

    ```sh
    git push origin --delete <old-branch-name>
    ```

2. **推送新分支**：

    ```sh
    git push origin <new-branch-name>
    ```

3. **更新本地追踪分支**（如果需要）：

    如果你有一个本地分支在追踪远程分支，你需要更新追踪信息：

    ```sh
    git branch --unset-upstream
    git branch -u origin/<new-branch-name>
    ```

### 示例

假设你有一个名为 `feature-old` 的分支，想将其重命名为 `feature-new`：

1. **重命名本地分支**：

    ```sh
    git branch -m feature-old feature-new
    ```

2. **删除远程旧分支**：

    ```sh
    git push origin --delete feature-old
    ```

3. **推送新分支**：

    ```sh
    git push origin feature-new
    ```

4. **更新本地追踪分支**（如果需要）：

    ```sh
    git branch --unset-upstream
    git branch -u origin/feature-new
    ```

### 总结

- **重命名当前分支**：`git branch -m <new-branch-name>`
- **重命名其他分支**：`git branch -m <old-branch-name> <new-branch-name>`
- **删除远程旧分支**：`git push origin --delete <old-branch-name>`
- **推送新分支**：`git push origin <new-branch-name>`
- **更新本地追踪分支**：`git branch --unset-upstream` 和 `git branch -u origin/<new-branch-name>`

通过这些步骤，你可以顺利地重命名分支并确保远程仓库中的分支名称也得到更新。

`git branch -M` 是 `git branch -m` 的一种变体，主要用于强制重命名分支。如果目标分支名称已经存在，`-M` 选项会覆盖现有的分支名称，而 `-m` 选项在目标分支名称已存在时会失败。

### 使用方法

1. **重命名当前分支**：

    ```sh
    git branch -M <new-branch-name>
    ```

    例如，如果你当前在 `old-branch` 分支上，想将其重命名为 `new-branch`，即使 `new-branch` 已经存在：

    ```sh
    git branch -M new-branch
    ```

2. **重命名其他分支**：

    ```sh
    git branch -M <old-branch-name> <new-branch-name>
    ```

    例如，将 `old-branch` 重命名为 `new-branch`，即使 `new-branch` 已经存在：

    ```sh
    git branch -M old-branch new-branch
    ```

### 示例

假设你有一个名为 `feature-old` 的分支，并且你想将其重命名为 `feature-new`，即使 `feature-new` 已经存在：

1. **重命名当前分支**：

    ```sh
    git branch -M feature-new
    ```

2. **重命名其他分支**：

    ```sh
    git branch -M feature-old feature-new
    ```

### 注意

使用 `-M` 选项时要小心，因为它会覆盖现有的分支，这可能会导致你丢失对旧分支的引用。如果你不确定目标分支是否存在，或者不希望覆盖现有分支，最好使用 `-m` 选项并手动检查分支是否存在。

### 总结

- **强制重命名当前分支**：`git branch -M <new-branch-name>`
- **强制重命名其他分支**：`git branch -M <old-branch-name> <new-branch-name>`

通过这些命令，你可以在需要时强制重命名分支，覆盖现有的分支名称。

## 删除分支
在 Git 中，你可以使用 `git branch -d` 或 `git branch -D` 命令来删除本地分支。你也可以使用 `git push` 命令来删除远程分支。以下是详细的步骤：

### 删除本地分支

1. **删除已合并的本地分支**：

    如果分支已经被合并到当前分支或其他分支，你可以使用 `-d` 选项：

    ```sh
    git branch -d <branch-name>
    ```

    例如，删除名为 `feature-branch` 的分支：

    ```sh
    git branch -d feature-branch
    ```

2. **强制删除本地分支**：

    如果分支尚未合并，你可以使用 `-D` 选项强制删除：

    ```sh
    git branch -D <branch-name>
    ```

    例如，强制删除名为 `feature-branch` 的分支：

    ```sh
    git branch -D feature-branch
    ```

### 删除远程分支

要删除远程分支，你需要使用 `git push` 命令并指定删除选项：

```sh
git push origin --delete <branch-name>
```

例如，删除远程仓库中的 `feature-branch` 分支：

```sh
git push origin --delete feature-branch
```

### 示例

假设你有一个名为 `feature-old` 的分支，并且你想删除它：

1. **删除本地分支**：

    如果分支已经合并：

    ```sh
    git branch -d feature-old
    ```

    如果分支尚未合并：

    ```sh
    git branch -D feature-old
    ```

2. **删除远程分支**：

    ```sh
    git push origin --delete feature-old
    ```

### 注意事项

- **删除本地分支**：确保你不在要删除的分支上。你不能删除当前所在的分支。
- **删除远程分支**：确保你有权限删除远程分支。

### 总结

- **删除已合并的本地分支**：`git branch -d <branch-name>`
- **强制删除本地分支**：`git branch -D <branch-name>`
- **删除远程分支**：`git push origin --delete <branch-name>`

通过这些命令，你可以轻松地删除不再需要的本地和远程分支。


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























