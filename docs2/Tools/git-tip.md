# Git-tip

## Tip 01: 在您的 Git 提交消息前添加用户故事 ID

在提交消息之前添加一些有意义的东西总是一个好习惯。例如，在使用Jira等项目管理工具时，通常会在提交之前添加您正在处理的用户故事 ID。这也是非常标准的。

让我们从查看基本的提交消息开始。一种相当普遍的风格是
```text
ABC-123: 对已完成工作的简洁描述
```
其中ABC-123是项目管理平台（例如 Jira）中的工单/故事 ID。这是一种简单的格式

因此，如果我们的分支被命名为“ABC-123-some-nice-feature”，我们想要提取ABC-123段并将其添加到我们的提交消息中。

这就是 Git Hooks 的用武之地。Git Hooks 只是在某些版本控制系统 (VCS) 事件发生时触发自定义脚本的一种方式，它们可以在基于 git 的项目的 .git/hooks 目录中找到。

### 如何解决？

我们可以找到目录 `.git/hooks/prepare-commit-msg`

打开文件 `prepare-commit-msg` 写入以下代码:

```bash
#!/bin/bash

# List the branches that don't apply bellow
if [ -z "$BRANCHES_TO_IGNORE" ]; then
  BRANCHES_TO_IGNORE=(master develop staging test)
fi

# Pick the current branch name and check if it is excluded
BRANCH_NAME=$(git symbolic-ref --short HEAD)
BRANCH_IGNORED=$(printf "%s\n" "${BRANCHES_TO_IGNORE[@]}" | grep -c "^$BRANCH_NAME$")

# Remove the unnecessary parts
TRIMMED=$(echo $BRANCH_NAME | sed -E -e 's:^(\w+)\/([^-]*-[^-]*)-.*:\2:' -e 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/')

# If it isn't excluded, prepend the part that interests us to the given commit message
if [ -n "$BRANCH_NAME" ] &&  ! [[ $BRANCH_IGNORED -eq 1 ]]; then
  sed -i.bak -e "1s/^/$TRIMMED: /" $1
fi
```

然后再初始化仓库:

```bash
git init
```

此时我们只需执行 `git commit` 就可以了



### 参考链接
1. [Enhancing Your Git Commit Messages](https://hackernoon.com/enhancing-your-git-commit-messages-2a299295o)
2. [Prepending Your Git Commit Messages with User Story IDs](https://medium.com/@nicklee1/prepending-your-git-commit-messages-with-user-story-ids-3bfea00eab5a) ←(推荐)
3. [How to specify a git commit message template for a repository in a file at a relative path to the repository?](https://stackoverflow.com/questions/21998728/how-to-specify-a-git-commit-message-template-for-a-repository-in-a-file-at-a-rel)




## Tip 02: git把本次修改的内容添加到上次提交中
开发中经常出现已经 `commit` 但是又修改内容，不想提交新的 `commit`, 我们可以执行下面命令:

```bash
git commmit --amend

```

这个命令会把当前修改的暂存文件添加到上一次提交中，但是会弹出编辑修改场次的提交文本，如果不想修改提交文本:

```bash
git commit --amend --no-edit
```
如果确实需要修改可以:

```bash
git commit --amend -m "new commit message."
```

git hook `prepare-commit-msg` 会自动给我们添加前缀 `ABC-123:`  不用担心。

查看log信息
```bash
git log
```

应该可以看到
```text
ABC-123: new commit message.
```

### Bitbcket 上的 git 教程
[改写类似](https://www.atlassian.com/git/tutorials/rewriting-history#:~:text=The%20git%20commit%20%2D%2Damend,message%20without%20changing%20its%20snapshot.)