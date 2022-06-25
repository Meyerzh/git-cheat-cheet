# 入门 Getting Started
> {docsify-updated}

## 初始化一个新的仓库：git init
要创建新的存储库，您将使用该git init命令。git init是您在新存储库的初始设置期间使用的一次性命令。执行此命令将.git在您当前的工作目录中创建一个新的子目录。这也将创建一个新的主分支。

### 使用新的 git 存储库对现有项目进行版本控制
此示例假设您已经有一个想要在其中创建存储库的现有项目文件夹。您将首先cd进入根项目文件夹，然后执行`git init`命令。

```bash
cd /path/to/your/existing/code

git init
```

指向git init现有项目目录将执行与上述相同的初始化设置，但仅限于该项目目录。

```bash
git init <project directory>
```

## 克隆现有存储库： `git clone`
如果项目已经在中央存储库中设置，则克隆命令是用户获取本地开发克隆的最常用方法。像git init，克隆通常是一次性操作。一旦开发人员获得工作副本，所有版本控制操作都通过其本地存储库进行管理。

```bash
git clone <repo url>
```

## 将更改保存到存储库： `git add` 和 `git commit`
1. 进入项目目录：
```bash
cd /path/to/project
```
在项目目录下进行工作，修改代码。。。

2. 修改文件后提交代码：
```bash
git add . # 提交所有修改的文件。
git commit -m "added commit to the repo."
```
执行此示例后，您的 repo 现在将CommitTest.txt添加到历史记录中，并将跟踪文件的未来更新。


## Repo-to-repo 协同合作: `git push`
执行完 `git commit`, 我们的修改提交就会记录在我们本地的Git里面。如果我们想让同事拿到我们提交的代码。就需要将本地的 commit push 到公共的远端仓库。
- 如果你的仓库是 git clone 创建出来的话，执行命令 `git remote -v`
```bash
git remote -v
```
你可以看到对应的远程仓库地址。

- 如果你的仓库是 git init 创建出来的话，就需要配置添加对应的远程仓库。

## 配置和设置：git config
设置远程 repo 后，您需要将远程 repo url 添加到本地git config，并为本地分支设置上游分支。该git remote命令提供了这样的实用程序。
```bash
git remote add <remote_name> <remote_repo_url>
```
举个例子：
比如当前文档的 **repo url** 是 `git@github.com:Meyerzh/git-cheat-sheet.git`。
那么我将执行如下命令:
```bash
git remote add origin git@github.com:Meyerzh/git-cheat-sheet.git
```
!> 因为默认 **Clone** 的仓库远程 **Repo Url** 名字都是 `origin`，所以我们添加的时候也使用这个名字，作为默认远端仓库地址。