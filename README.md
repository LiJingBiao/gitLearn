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
## 从feture分支合并到dev分支示例
从 dev 分支创建 feature 分支：
```
git checkout dev
git checkout -b feature

```
在 feature 分支上进行开发。
将 dev 分支的更改合并到 feature 分支：
```
git checkout feature
git pull origin dev
```
解决冲突并提交：
```
# 解决冲突后
git add .
git commit -m "Resolved conflicts with dev"
```
将 feature 分支合并回 dev 分支：
```
git checkout dev
git merge feature
```
推送更改到远程仓库：
```
git push origin dev
```
在 Git 中，git pull origin dev 是一个常见的命令，它的作用是从远程仓库（origin）拉取指定分支（dev）的最新更改并将这些更改合并到当前分支。

从远程仓库获取最新的更改：相当于执行 git fetch origin dev，它会从远程仓库获取 dev 分支的最新提交和对象。
将这些更改合并到当前分支：相当于执行 git merge origin/dev，它会将获取到的 dev 分支的更改合并到你当前所在的分支。

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
在Git中，你可以使用`git log`命令结合`--author`选项来查找特定作者的提交记录。以下是几种方法：

git log查找作者

1. **查找特定作者的提交**

```bash
git log --author="作者名"
```

例如，如果你要查找名为"John Doe"的所有提交：

```bash
git log --author="John Doe"
```

2. **部分匹配作者名**

Git允许使用正则表达式进行匹配，所以你可以查找包含特定字符串的作者名：

```bash
git log --author="John"
```

这会匹配任何包含"John"的名字。

3. **忽略大小写**

如果你想忽略大小写，可以添加`-i`选项：

```bash
git log --author="john" -i
```

4. **使用正则表达式**

可以使用更复杂的正则表达式来匹配作者名：

```bash
git log --author="^(John|Jane) Doe$" -E
```

`-E`选项启用扩展的正则表达式模式，这里匹配的是名字为"John Doe"或"Jane Doe"的提交。

5. **显示简化日志**

如果你只想看到提交的哈希和提交信息，可以结合`--oneline`选项：

```bash
git log --author="John Doe" --oneline
```

6. **查找特定时间范围内的提交**

结合时间范围查找特定作者的提交：

```bash
git log --author="John Doe" --since="1 month ago" --until="2 weeks ago"
```

7. **查看修改的文件**

如果想看到作者修改了哪些文件，可以使用`--name-only`或`--name-status`：

```bash
git log --author="John Doe" --name-only
```

在Git中，你可以使用`git log`命令来查看提交日志，并且可以通过各种选项和参数来进行搜索。以下是一些常用的方法来搜索Git提交历史：

1. **基本搜索**

- **搜索提交信息中的文本**：
  ```bash
  git log --grep="关键词"
  ```

2. **搜索文件变更**

- **查看特定文件的提交历史**：
  ```bash
  git log -- path/to/file
  ```

- **搜索文件内容中的变更**：
  ```bash
  git log -S"搜索字符串" -- path/to/file
  ```
  `-S`选项会搜索文件内容中包含给定字符串的提交。

3. **作者或提交者搜索**

- **按作者搜索**：
  ```bash
  git log --author="作者名"
  ```

- **按提交者搜索**：
  ```bash
  git log --committer="提交者名"
  ```

4. **时间范围搜索**

- **在特定时间范围内搜索**：
  ```bash
  git log --since="1 week ago" --until="2 days ago"
  ```

5. **使用正则表达式搜索**

- **使用正则表达式**：
  ```bash
  git log --grep="正则表达式" -E
  ```
  `-E`选项启用扩展的正则表达式语法。

6. **组合条件搜索**

- **组合多个条件**：
  ```bash
  git log --author="作者名" --grep="关键词" -- path/to/file
  ```

7. **其他常用选项**

- **只显示一行简短的提交日志**：
  ```bash
  git log --oneline
  ```

- **查看所有分支上的提交**：
  ```bash
  git log --all
  ```

- **显示文件的修改情况**：
  ```bash
  git log --stat
  ```

- **显示文件的差异摘要**：
  ```bash
  git log --patch
  ```

- **显示提交的关联信息**：
  ```bash
  git log --graph --oneline --decorate --all
  ```

注意事项：

- 使用`--grep`时，默认是区分大小写的。如果想忽略大小写，可以添加`-i`选项：
  ```bash
  git log -i --grep="关键词"
  ```


注意事项：

- **引号使用**：如果作者名中包含空格，使用引号包围作者名。
- **正则表达式**：如果你使用正则表达式进行匹配，记得使用`-E`选项来启用扩展的正则表达式。
- **Git的搜索是区分大小写的**，除非你指定了`-i`选项。
- **效率**：对于大型仓库，搜索可能会比较慢，特别是如果没有优化索引或历史记录。

这些命令可以帮助你过滤Git日志，找到特定作者的提交记录，方便进行代码审查、历史追踪或其他需要根据作者进行筛选的任务。



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
git checkout 6c8b47a6fc -- MyLink.m
```

## git上传大文件
```
git lfs上传AMap3DMap-NO-IDFA
git init #创建本地仓库环境
git lfs install #安装大文件上传应用
git lfs track MAMapKit #追踪要上传的大文件，*表示路径下的所有文件
git add .gitattributes #添加先上传的属性文件(要先上传属性文件，不然有可能失败)
git commit -m "pre" #添加属性文件上传的说明
git remote add origin https://github.com/Youpeng-Zhang/MOP.git #建立本地和Github仓库的链接
git push origin master #上传属性文件
git add * #添加要上传的大文件，*表示路径下的所有文件
git commit -m "Git LFS commit" #添加大文件上传的说明
git push origin master #上传大文件
```
## 使用git pull origin feature/dev_7.2.0 hint: You have divergent branches and need to specify how to reconcile them. hint: You can do so by running one of the following commands sometime before
```
% git checkout -b feature/lijingbiao/miniApi_merge 
Switched to a new branch 'feature/lijingbiao/miniApi_merge'
% git pull origin feature/dev_7.2.0               
From coding.xxxx.com:app/xxxxMEApp
 * branch                  feature/dev_7.2.0 -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
% git config pull.rebase false
% git pull origin feature/dev_7.2.0
```
这个提示信息表明你的本地分支和远程分支之间有分歧（divergent branches），Git 不确定应该如何合并这些更改。你需要指定合并策略。以下是你可以采取的步骤：

合并（merge）：这会创建一个合并提交，将两个分支的历史合并在一起。
```
git config pull.rebase false
```
重基（rebase）：这会将你的本地提交重新应用到远程分支的顶部，创建一个线性的历史。
```
git config pull.rebase true
```
仅快进（fast-forward only）：这只会在没有分歧的情况下进行合并，否则会失败。
```
git config pull.ff only
```
你可以选择其中一种策略来解决当前的分歧。具体操作如下：

1. 合并（merge）
如果你希望使用合并策略，可以运行：
```
git config pull.rebase false
git pull origin feature/dev_7.2.0
```
2. 重基（rebase）
如果你希望使用重基策略，可以运行：
```
git config pull.rebase true
git pull origin feature/dev_7.2.0
```
3. 仅快进（fast-forward only）
如果你希望只在没有分歧的情况下进行合并，可以运行：
```
git config pull.ff only
git pull origin feature/dev_7.2.0
```
临时指定策略
如果你只想临时指定一次策略，可以在命令行中直接使用参数：

对于合并：
```
git pull --no-rebase origin feature/dev_7.2.0
```
对于重基：
```
git pull --rebase origin feature/dev_7.2.0
```
对于仅快进：
```
git pull --ff-only origin feature/dev_7.2.0
```
选择合适的策略后，执行相应的命令即可解决分支分歧问题。

## [git教程](https://github.com/geeeeeeeeek/git-recipes/wiki/)

## 拉代码git报错You have not concluded your merge (MERGE_HEAD exists).
这表示 Git 检测到一个未完成的合并操作
第一种方法
```
git merge --abort
```
第二种解决方法
```
# 查看当前状态
git status

# 解决冲突，编辑冲突文件并解决冲突内容
nano conflicted_file.txt

# 标记冲突已解决
git add conflicted_file.txt

# 完成合并并提交
git commit
```

## 查看某次提交更新的文件
```
git show --name-only a1b2c3d4

git show --name-status a1b2c3d4
#显示文件名以及文件的状态（如新增、修改、删除）
```

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


git下载工程报错
```
sudo vim ~/.ssh/config
Host *
ServerAliveInterval 60
ServerAliveCountMax 30
```
git checkout xxx && git pull命令合并,在`~/.gitconfig`中
```
[alias]
    cop = "!f() { git checkout $1 && git pull origin $1; }; f"
```

## 子模块
以下是关于 Git 子模块拉取和更新的主要命令：

1. 克隆包含子模块的项目:
```bash
# 方式1：克隆时同时下载子模块
git clone --recursive [URL]

# 方式2：克隆后再初始化子模块
git clone [URL]
git submodule init
git submodule update
```

2. 更新子模块:
```bash
# 更新所有子模块到最新提交
git submodule update --remote

# 更新特定子模块
git submodule update --remote [submodule_name]

# 更新子模块到主仓库记录的提交点
git submodule update --init
```

3. 拉取子模块变更:
```bash
# 一次性拉取所有子模块的变更
git pull --recurse-submodules

# 先进入子模块目录再拉取
cd [submodule_directory]
git pull origin master
```

4. 查看子模块状态:
```bash
# 查看子模块信息
git submodule status

# 查看子模块详细信息
git submodule foreach git status
```

5. 添加新的子模块:
```bash
git submodule add [URL] [path]
```

注意事项：
- 子模块默认处于分离头指针(detached HEAD)状态
- 更新子模块前最好先确保主仓库无未提交的修改
- 如果子模块有自己的子模块，可能需要递归操作
- 建议在对子模块做修改前先切换到具体分支

git submodule update 的这两个选项有重要的区别：

1. `git submodule update --init`
- 将子模块更新到主仓库记录的特定提交点
- 使用的是主仓库中记录的子模块提交 hash
- 适用于需要和团队保持一致的场景
- 相当于把子模块"锁定"在特定版本

例如:
```bash
# 主仓库记录子模块commit为 abc123
# 执行后子模块就会切换到 abc123
git submodule update --init
```

2. `git submodule update --remote`
- 将子模块更新到远程仓库的最新提交
- 会直接拉取子模块远程仓库的最新代码
- 适用于需要使用子模块最新功能的场景
- 可能会导致团队成员之间不一致

例如:
```bash
# 子模块远程最新commit为 xyz789
# 执行后子模块会更新到 xyz789
git submodule update --remote
```

使用建议：
- 团队协作时优先使用 `--init` 保持一致性
- 需要更新子模块时:
  1. 先用 `--remote` 更新到最新
  2. 测试没问题后提交主仓库
  3. 其他成员再用 `--init` 同步

这样可以避免团队成员使用不同版本的子模块导致的问题。

提交子模块需要分两步：先提交子模块的修改，再提交主仓库的变更。具体步骤如下：

1. 提交子模块修改:
```bash
# 进入子模块目录
cd [submodule_directory]

# 常规的 git 提交流程
git add .
git commit -m "子模块的修改信息"
git push origin [branch_name]
```

2. 提交主仓库:
```bash
# 回到主仓库目录
cd ..

# 此时会看到子模块有新的提交
git status  # 会显示子模块有更改

# 提交主仓库中的子模块变更
git add [submodule_directory]
git commit -m "更新子模块到新版本"
git push
```

使用简化命令：
```bash
# 一次性查看所有子模块的状态
git submodule foreach git status

# 一次性添加所有子模块的更改
git submodule foreach git add .

# 一次性提交所有子模块的更改
git submodule foreach git commit -m "提交信息"

# 一次性推送所有子模块的更改
git submodule foreach git push
```

注意事项：
1. 确保先提交子模块再提交主仓库
2. 子模块的提交需要推送到远程
3. 主仓库记录的是子模块的提交指针
4. 如果忘记推送子模块，其他人更新时会遇到问题

最佳实践：
```bash
# 1. 确认在正确的分支
git submodule foreach git checkout main

# 2. 提交子模块更改
git submodule foreach git add .
git submodule foreach git commit -m "update submodule"
git submodule foreach git push

# 3. 提交主仓库更改
git add .
git commit -m "update submodules"
git push
```

`git submodule foreach` 是一个用于在所有子模块上执行命令的工具。它会遍历项目中的每个子模块，并在每个子模块目录中执行指定的命令。

基本语法：
```bash
git submodule foreach '<command>'
```

常见用例：

1. 查看所有子模块状态：
```bash
git submodule foreach git status
```

2. 切换所有子模块分支：
```bash
git submodule foreach git checkout main
```

3. 拉取所有子模块更新：
```bash
git submodule foreach git pull origin main
```

4. 批量提交：
```bash
git submodule foreach 'git add . && git commit -m "update"'
```

特点：
1. 自动遍历 - 自动在每个子模块中执行命令
2. 显示路径 - 会显示当前执行命令的子模块路径
3. 支持复杂命令 - 可以用引号包含多个命令
4. 支持中断 - 可以用 ctrl+c 中断执行

举个实际例子：
```bash
# 项目结构
main-repo/
  ├── sub1/   # 子模块1
  ├── sub2/   # 子模块2
  └── sub3/   # 子模块3

# 执行命令
git submodule foreach git status

# 输出可能是：
Entering 'sub1'
On branch main
nothing to commit, working tree clean
Entering 'sub2'
On branch main
modified: file.txt
Entering 'sub3'
On branch main
nothing to commit, working tree clean
```

这个命令需要在主仓库的根目录下执行，而不是在子模块目录内。

例如:
```bash
# 项目结构
main-repo/         # ← 在这里执行命令
  ├── sub1/
  ├── sub2/
  └── sub3/

# 正确的执行位置
cd main-repo
git submodule foreach 'git add . && git commit -m "update"'

# 错误的执行位置
cd main-repo/sub1  # ❌ 不要在子模块目录内执行
```

工作原理：
1. `git submodule foreach` 命令会：
   - 从主仓库根目录开始
   - 自动进入每个子模块目录
   - 执行指定的命令
   - 然后返回继续处理下一个子模块

2. 执行顺序示例：
```bash
# 在 main-repo/ 下执行命令后
Entering 'sub1'
[master abc1234] update
Entering 'sub2'
[master def5678] update
Entering 'sub3'
[master ghi9012] update
```

如果你当前在子模块目录中，需要：
```bash
# 先回到主仓库根目录
cd ..   # 或者适当的路径返回主仓库根目录
# 再执行命令
git submodule foreach 'git add . && git commit -m "update"'
```


## git回滚到某次提交
git reset --hard <commit-hash>

git reset --soft HEAD













