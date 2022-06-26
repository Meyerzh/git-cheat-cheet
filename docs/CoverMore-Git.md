# CoverMore-Git

![img](assets/images/1*9yJY7fyscWFUVRqnx0BM6A.png)

## GitFlow 常用分支
> 在 Git 流程工作流中，有五种不同的分支类: Master, Develop, Feature, Release, Hotfix。

### master
 - 主分支, 产品的功能全部实现后, 最终由master分支对外发布。
 - 该分支为只读唯一分支，只能从其他分支(release/hotfix)合并, 不能在此分支修改。
 - 所有在master的推送应该打标签做记录，方便追溯。

![image-20220625185857296](assets/images/image-20220625185857296.png)

### develop
  - 主开发分支，基于`master`分支。
  - 包含所有要发布到下一个`release`的代码。
  - 该分支为只读唯一分支, 只能从其他分支合并。
  - feature功能分支完成, 合并到develop(此处合并应该创建 pull request)

### feature
  - 功能开发分支, 基于`develop`分支克隆 , 主要用于新需求新功能的开发。
  - 功能开发完毕后合到`develop`分支
  - feature分支可同时存在多个 , 用于团队中多个功能同时开发 , 属于临时分支 , 功能完成后可选删除

![image-20220625185929332](assets/images/image-20220625185929332.png)

### release
  - 测试分支, 基于`feature`分支合并到`develop`之后, 从`develop`分支克隆。
  - 主要用于提交给测试人员进行功能测试, 测试过程中发现的BUG在本分支进行修复, 修复完成上线后合并到develop/master分支并推送(完成功能), 打Tag
  - 属于临时分支, 功能上线后可选删除。

![image-20220625185953107](assets/images/image-20220625185953107.png)

### hotfix
  - 补丁分支, 基于`master`分支克隆, 主要用于对线上的版本进行BUG修复。
  - 修复完毕后分别合并到`develop`和`master`分支并推送, 打Tag。
  - 属于临时分支, 补丁修复上线后可选删除。

![image-20220625190016394](assets/images/image-20220625190016394.png)

## Cmap 分支介绍

[[CoverMore CMS] Cover More Self-Service Technical Kick-off ](https://docs.google.com/presentation/d/1G_1yFEj5OC5tsOggdILy2IOhxou_X-kHccWtKCxP_HI/edit#slide=id.ge8a66e3430_0_4)

| Git Flow | Cmap                               | 描述                                                         |
| -------- | ---------------------------------- | ------------------------------------------------------------ |
| master   | `master`                             |                                                              |
| develop  | `develop`                            | from **master**                                              |
| feature  | `ADP-* `                           | from **develop** then merge into **develop**                 |
| release  | `Release-*` or `Sprint-*`|                                                              |
| hotfix   | `hotfix`                             | from **master** then merged into **master** and **development** |

> 这里 **release-2022625**, 其它组也有用 **Sprint-11** 命名的。

## Git Flow 命令示例

### 开始 Feature

## Git merge
Merge **FeatureA** into **Master**

```bash
git checkout master

git merage FeatureA --no-ff
```

## Git reset
```bash
git reset --soft HEAD~
```
退回到上一个版本，并将提交返回到暂存区。

### 复习 git 三种状态
Git 有三种状态，你的文件可能处于其中之一：已提交（committed）、已修改（modified）和已暂存（staged）。
由此引入 Git 项目的三个工作区域的概念：Git 仓库、工作目录以及暂存区域。

![image-20220626113133226](assets/images/image-20220626113133226.png)

`git reset --soft HEAD~`,
只是修改了commit记录，并让已提交的的代码返回了暂存。
也就是说实际在运行的代码没有变化。
其本质就是要重新编辑 commit 文件。

当你只想查看 上一个commit 代码运行结果是 可以执行：
```bash
git checkout HEAD~

git chekcout <commit-id hash> 直接查看某个具体commit代码运行结果。
```



## Git blame
git-blame - 显示上次修改文件每一行的版本和作者
```bash
git blame <filename>

git blame -L start,end <filename>
```
例如: 查看 test.js 文件
```bash
git blame test.js

git blame -L 10,20 test.js // 查看10-20行的修改历史

git blame -L 10,+20 test.js // 查看10再加20行的修改历史
```

> `--color-lines`
> 如果它们来自与前一行相同的提交，则默认格式的行注释颜色不同。这使得区分不同提交引入的代码块变得更容易
> `--color-by-age`
> 根据默认格式的线条年份对线条注释进行着色

如果您对 v2.6.18 之前的更改不感兴趣，或者对 3 周之前的更改不感兴趣，您可以使用类似于git rev-list 的修订范围说明符：
```bash
git blame v2.6.18 .. -- foo
git blame --since=3.weeks -- foo

```