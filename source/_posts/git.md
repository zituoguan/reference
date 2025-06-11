---
title: Git
date: 2020-11-25 18:28:43
background: bg-[#d7593e]
tags:
  - github
  - gitlab
  - version
  - VCS
categories:
  - Linux 命令
intro: 这份速查表总结了常用的 Git 命令行指令，以便快速参考。
plugins:
  - copyCode
---

## 入门

### 创建仓库

创建一个新的本地仓库

```shell script
$ git init [项目名称]
```

克隆一个仓库

```shell script
$ git clone git_url
```

将仓库克隆到指定目录

```shell script
$ git clone git_url my_directory
```

### 进行更改 {.row-span-2}

显示工作目录中已修改的文件，这些文件已暂存，准备进行下一次提交

```shell script
$ git status
```

暂存文件，准备提交

```shell script
$ git add [file]
```

暂存所有已更改的文件，准备提交

```shell script
$ git add .
```

将所有暂存的文件提交到版本历史

```shell script
$ git commit -m "提交信息"
```

将所有已跟踪的文件提交到版本历史

```shell script
$ git commit -am "提交信息"
```

丢弃工作目录中未暂存的更改

```shell script
$ git restore [file]
```

取消暂存一个已暂存的文件

```shell script
$ git restore --staged [file]
```

取消暂存文件，保留文件更改

```shell script
$ git reset [file]
```

将所有内容还原到最后一次提交

```shell script
$ git reset --hard
```

显示已更改但未暂存的内容的差异

```shell script
$ git diff
```

显示已暂存但尚未提交的内容的差异

```shell script
$ git diff --staged
```

应用当前分支中领先于指定分支的任何提交

```shell script
$ git rebase [branch]
```

### 配置

设置将附加到您的提交和标签的名称

```shell script
$ git config --global user.name "名称"
```

设置将附加到您的提交和标签的电子邮件地址

```shell script
$ git config --global user.email "邮箱"
```

启用 Git 输出的一些颜色化

```shell script
$ git config --global color.ui auto
```

在文本编辑器中编辑全局配置文件

```shell script
$ git config --global --edit
```

### 使用分支

列出所有本地分支

```shell script
$ git branch
```

列出所有分支，包括本地和远程

```shell script
$ git branch -av
```

切换到 my_branch 分支，并更新工作目录

```shell script
$ git checkout my_branch
```

创建一个名为 new_branch 的新分支

```shell script
$ git checkout -b new_branch
```

删除名为 my_branch 的分支

```shell script
$ git branch -d my_branch
```

将 branchA 合并到 branchB

```shell script
$ git checkout branchB
$ git merge branchA
```

标记当前提交

```shell script
$ git tag my_tag
```

### 查看您的仓库

显示当前活动分支的提交历史

```shell script
$ git log
```

显示 branchA 上但不在 branchB 上的提交

```shell script
$ git log branchB..branchA
```

显示更改了文件的提交，即使文件被重命名

```shell script
$ git log --follow [file]
```

显示 branchA 中存在但 branchB 中不存在的内容的差异

```shell script
$ git diff branchB...branchA
```

以人类可读的格式显示 Git 中的任何对象

```shell script
$ git show [SHA]
```

### 同步

从该 Git 远程仓库获取所有分支

```shell script
$ git fetch [alias]
```

将远程分支合并到当前分支以使其保持最新

```shell script
$ git merge [alias]/[branch]
# 不快进合并
$ git merge --no-ff [alias]/[branch]
# 仅快进合并
$ git merge --ff-only [alias]/[branch]
```

将本地分支的提交传输到远程仓库分支

```shell script
$ git push [alias] [branch]
```

从跟踪的远程分支获取并合并任何提交

```shell script
$ git pull
```

仅将另一个分支的特定提交合并到当前分支

```shell script
$ git cherry-pick [commit_id]
```

### 远程

添加一个 git URL 作为别名

```shell script
$ git remote add [alias] [url]
```

显示您已设置的远程仓库的名称

```shell script
$ git remote
```

显示远程仓库的名称和 URL

```shell script
$ git remote -v
```

移除一个远程仓库

```shell script
$ git remote rm [remote repo name]
```

更改 git 仓库的 URL

```shell script
$ git remote set-url origin [git_url]
```

### 临时提交

保存已修改和已暂存的更改

```shell script
$ git stash
```

列出已储藏文件更改的堆栈顺序

```shell script
$ git stash list
```

从储藏堆栈顶部恢复工作

```shell script
$ git stash pop
```

丢弃储藏堆栈顶部的更改

```shell script
$ git stash drop
```

### 跟踪路径更改

从项目中删除文件并将删除操作暂存以供提交

```shell script
$ git rm [file]
```

更改现有文件路径并将移动操作暂存

```shell script
$ git mv [existing-path] [new-path]
```

显示所有提交日志，并指示任何已移动的路径

```shell script
$ git log --stat -M
```

### 忽略文件

```
/logs/*

# "!" 表示不要忽略
!logs/.gitkeep

/# 忽略 Mac 系统文件
.DS_store

# 忽略 node_modules 文件夹
node_modules

# 忽略 SASS 配置文件
.sass-cache
```

`.gitignore` 文件指定了 Git 应该忽略的、有意不跟踪的文件。

## Git 技巧

### 重命名分支

- #### **重命名**为 `new_name`
  ```shell script
  $ git branch -m <new_name>
  ```
- #### **推送**并重置上游
  ```shell script
  $ git push origin -u <new_name>
  ```
- #### **删除**远程分支
  ```shell script
  $ git push origin --delete <old>
  ```
  {.marker-timeline}

### 日志

按内容搜索更改

```shell script
$ git log -S'<源中的术语>'
```

显示特定文件随时间的变化

```shell script
$ git log -p <file_name>
```

打印出酷炫的日志可视化效果

```shell script {.wrap}
$ git log --pretty=oneline --graph --decorate --all
```

### 分支 {.row-span-2}

列出所有分支及其上游分支

```shell script
$ git branch -vv
```

快速切换到上一个分支

```shell script
$ git checkout -
```

仅获取远程分支

```shell script
$ git branch -r
```

从另一个分支检出单个文件

```shell script
$ git checkout <branch> -- <file>
```

### 改写历史

改写最后一次提交信息

```shell script
$ git commit --amend -m "新信息"
```

修改最新的提交，但不更改提交信息。

```shell script
$ git commit --amend --no-edit
```

另请参阅：[改写历史](https://www.atlassian.com/git/tutorials/rewriting-history)

### Git 别名

```cmd
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

另请参阅：[更多别名](https://gist.github.com/johnpolacek/69604a1f6861129ef088)

## 高级 Git

### 子模块

在您的仓库中创建一个新的子模块：

```shell script
$ git submodule add <repository_url> <path>
```

克隆一个仓库并初始化其子模块：

```shell script
$ git clone --recursive <repository_url>
```

将仓库中的所有子模块更新到其各自自分支的最新提交：

```shell script
$ git submodule update
```

从子模块的远程仓库拉取最新更改并在主仓库中更新它们：

```shell script
$ git submodule update --remote
```

从您的仓库中移除一个子模块：

```shell script
$ git submodule deinit <path>
$ git rm <path>
$ git commit -m "移除了子模块"
```

### 遴选 (Cherry-picking)

遴选允许您将一个分支的特定提交应用到另一个分支。

```shell script
$ git cherry-pick <commit_hash>
```

### Reflog

显示 reflog，展示 HEAD 和分支移动的历史记录：

```shell script
$ git reflog
```

使用 reflog 找到丢失的提交或分支的哈希值，然后检出到该哈希值以恢复它：

```shell script
$ git checkout <commit_or_branch_hash>
```
