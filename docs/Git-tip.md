# Git 命令介绍
## Git merge

### --no-ff
git merge 合并时的 --no-ff 的作用： 禁止快进式合并

```bash
git checkout develop
git merge feature --no-ff
```

Git 合并两个分支时，如果顺着一个分支走下去可以到达另一个分支的话，那么 Git 在合并两者时，只会简单地把指针右移，叫做“快进”（fast-forward）：
```bash
           A---B---C feature
         /
D---E---F develop
```
要把 feature 合并到 develop 中，执行以下命令
```bash
git checkout develop
git merge feature

==== > 结果就会变成

D---E---F---A---B---C feature
                    develop
```
因为 feature 就在 develop 的下游，所以直接移动了 develop 的指针(HEAD)，master 和 feature 都指向了 **C**。
而如果执行了 `git merge --no-ff feature` 的话，是下面的结果：
```bash
git checkout develop
git merge feature --no-ff

==== >  结果就会变成

          A---B---C feature
         /         \
D---E---F-----------G develop
```
由于 --no-ff 禁止了快进，所以会生成一个新的合并提交，master 指向 `G`。

#### 总结
从合并后的代码来看，结果其实是一样的，区别就在于 `--no-ff` 会让 Git 生成一个新的提交对象。
主要方面后期查看代码历史

## Git reset
```bash
git reset --soft HEAD~ # 退回到上一个版本，并将提交返回到暂存区。
```


| options                        | 描述                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| git reset --soft               | 将分支回退到指定提交，工作区维持现状不变,暂存区会在现有基础上增加该commit之后的提交。 |
| git reset --mixed （默认操作） | 将分支回退到指定提交，暂存区也被同步为该指定提交，工作区保持不变。 |
| git reset --hard               | 将分支回退到指定分支，暂存区和工作区都会被同步为该指定的提交。 |



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


## 查看父级分支
查看当前千分是基于哪个分支创建。
```bash
git reflog show <childBranch>
```