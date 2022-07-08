# Git - 日常开发
{docsify-updated}

> 简单介绍 CoverMore 日常开发用到的git命令, 主要用到分支有 master、develop、ADP-001、ADP-002。 （ ADP- 是 feature 分支）


<section>

## Git 基础操作

### 分支 master

现在只有一个主分支 master ，master 不能直接推送代码。

![image-20220708095125405](assets/images/image-20220708095125405.png)

### 创建 develop

我们需要基于 master 创建一个 develop 分支

```bash
git branch develop
```

 从图形界面上可以看到新增一个 develop 分支。

![image-20220708095312049](assets/images/image-20220708095312049.png)

### 切换 develop

但是我们现在仍在 master 分支，需要切换到 develop 分支：

```bash
git checkout develop
切换到分支 'develop'

# git switch develop 也可以切换分支.
```

![image-20220708100533816](assets/images/image-20220708100533816.png)

从图形界面上可以看到，develop移动到了最左边，说明我们切换到了 develop 分支。

> 创建分支 和 切换分支 可以合并成 `git checkout -b develop`

```bash
git chekcout -b develop # 从当前分支检出 develop
git checkout -b develop master # 从 master 检出 develop
```

develop分支上一般也不直接推送代码。

### 提交代码

因为 develop 和 master 在同一个节点上，我们需要在 develop 上提交一些代码来区分master.

修改代码后 查看状态

```bash
git status

位于分支 develop
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     docs/00git-daily.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

暂存所有修改的文件

```bash
git add .
```

再次查看状态

```bash
git status

位于分支 develop
要提交的变更：
  （使用 "git restore --staged <文件>..." 以取消暂存）
        修改：     docs/00git-daily.md
```

提交暂存代码

```bash
git commit -m "Update document in develop."

[develop 3fd2484] Update document in develop.
 1 file changed, 3 insertions(+)
```

再次查看状态

```bash
git status

位于分支 develop
无文件要提交，干净的工作区
```

查看已提交的代码变更

```bash
git show # 查看最新一次修改
git log -p # 常看历史log 的文件修改
```

![image-20220708103843067](assets/images/image-20220708103843067.png)

↑ *终端截图* 常规的代码提交连招

经过一系列操作 我们来看一下图形界面

![image-20220708103947723](assets/images/image-20220708103947723.png)

可以看到 develop 前进了一个节点。

> **总结一下**
>
> 虽然 develop 检出自 master，但是伴随着开发很多时候 develop 和 master 不在一个节点上， develop 会后很多新的代码提交。后面会遇到
>
> - 基于 develop 创建开发分支 ADP-001
> - 基于 master 创建开发分支 ADP-002
>
> 基于不同分支创建开发分支 修改代码的git操作会有所不同。



完成的代码，首先要进行本地的测试。

推送到 origin/develop 部署到 DEV 环境 进行测试。

```bash
git push origin develop
```

推送到自己 fork 的 github 仓库。

```bash
git push meyerz ADP-001
```

### 创建PR

	1. 进入fork的仓库，点击 Pull request ，
	1. 设置仓库和分支，
	1. 点击 Create pull request 完成创建。

![image-20220708113622094](assets/images/image-20220708113622094.png)

↑ *Github Create pull request 页面，经过ps的*

> **注意：** 记得把 PR url 地址， 写到对应 Ticket： ADP-001 的 **Deployment Steps** 里。


## 场景模拟 - 常规流程
### 创建 ADP-001

我们直接基于 master 创建开发分支 ADP-001：

```bash
git checkout -b ADP-001 master
切换到一个新分支 'ADP-001'
```

![image-20220708115100298](assets/images/image-20220708115100298.png)

↑ *图形界面*

可以看到新增的 ADP-001 和 master 是在同一个节点。因为 ADP-001 在最左边 所以我们在 ADP-001 分支上。

> Tip:
>
> 命令 `git branch -vv` 可以用来查看 对应的远端分支。
>
> 命令 `git reflog show ADP-001` 查看分支历史

查看分支对应远端分支 我常用的是：

```bash
git status -sb
```



### 提交 ADP-001

在ADP-001上提交一些代码。

常规提价命令

```bash
git add .
git commit -m "ADP-001: Create ADP-001 and update some file."
```

如果没有增删文件，只是修改原有的文件, 可以合并为一个命令

```bash
git commit -am "ADP-001: Remove console.log code."
```

![image-20220708123216250](assets/images/image-20220708123216250.png)

↑*图形界面: 位于 ADP-001*

![image-20220708123337131](assets/images/image-20220708123337131.png)

↑ *图形界面: 位于 develop*

比较在不同分支对应的图形界面区别，空心圆表示当前所在的分支。



### Merge `ADP-001` Into `develop`

将 ADP-001 合并进 develop 我们需要执行命令：

```bash
git checkout develop
# 切换到分支 'develop'

git merge ADP-001
# [develop 7ecd48c] Merge branch 'ADP-001' into develop
```

![image-20220708125704389](assets/images/image-20220708125704389.png)

合并 ADP-001 之后的图形界面



### 推送到 origin/develop

当前本地位于 develop 分支，首先来看下 develop 的远端分支

```bash
git branch -vv
```

![image-20220708130155254](assets/images/image-20220708130155254.png)

可以看出 除了 master 有对应的远端 分支 [origin/master], 其它分支都是没有对应远端分支。

我们也可以使用命令

```bash
git status -sb
```

![image-20220708130429550](assets/images/image-20220708130429550.png)

![image-20220708130454023](assets/images/image-20220708130454023.png)

分别位于 master 和 develop 执行 `git status -sb` 查看当前分支对应的远端分支。



下面我们执行推送命令 push：

```bash
git push origin develop -u
```

上述命令推送到远程仓库的 develop 分支。

 `-u`  作用是将 分支 'develop' 设置为跟踪 'origin/develop'。

![image-20220708131010257](assets/images/image-20220708131010257.png)

至此部署dev环境的git操作结束。



### 推送到 fork 仓库 创建 Pr

```bash
git checkout ADP-001
# 切换到分支 'ADP-001'

git status -sb
## ADP-001

git push meyerz ADP-001 -u  # 推动到远端 fork 仓库
```

![image-20220708131542829](assets/images/image-20220708131542829.png)

代码推送完成，后续操作进入 github fork 仓库页面完成 Pr 创建即可。



最后来看一下图形界面

![image-20220708132220440](assets/images/image-20220708132220440.png)

拿来合并ADP-001 的图形界面 做一下对比

![image-20220708125704389](assets/images/image-20220708125704389.png)

可以观察到 develop 和 ADP-001 右边分别 多出了 *origin* 和 *meyerz* 就是我们设置对应的 远端仓库, master 一直就设置着远端仓库 origin。



> **总结**
>
> 上述是一个比较顺利的Git流程。

</section>


## 场景模拟 - 进阶流程

现在我们用 ADP-002 来演示进阶流程，回顾一下我们大致会经历的git操作有：

- 创建分支
- 提交代码
- 合并代码
- 部署 DEV 环境 ➜ 推送代码到 origin/develop
- 创建 Pr ➜ 推送代码到 meyerz/ADP-002



### 创建 ADP-002

这次我们可以直接从 origin/master 检出 ADP-002:

```bash
git checkout -b ADP-002 origin/master

# 分支 'ADP-002' 设置为跟踪 'origin/master'。
# 切换到一个新分支 'ADP-002'
```

![image-20220708140254130](assets/images/image-20220708140254130.png)

从图形界面可以看到 ADP-002、master、 origin/master, 2个本地一个远端分支都处于一个节点。



### 开发提交代码





<section>

## 创建分支 <small class="opacity-25 fw-light">Create branch</small>
### 基于 origin/master 创建 ADP-001 分支

```bash
git branch ADP-001 origin/master
git checkout ADP-001
# git switch ADP-001 也可以切换分支。

→ 分支 'ADP-001' 设置为跟踪 'origin/master'
```
> This step and the next one could be combined into a single step with `checkout -b ADP-001 origin/master`.



### 开始修改代码

现在我们可以在分支 ADP-001 上修改代码。当代码发生改变的时候：

![image-20220708091618212](assets/images/image-20220708091618212.png)







</section>




## 部署dev <small class="opacity-25 fw-light">Deploy dev</small>


## 拉取请求 <small class="opacity-25 fw-light">Pull request</small>

