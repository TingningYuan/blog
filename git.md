# git命令

## 1-安装git以及第一次使用git在github上进行提交

参考链接：https://www.cnblogs.com/sdcs/p/8270029.html



## 2-git 命令

### 提交

```bash
git commit
```



### 分支与合并

#### 创建、切换分支

```bash
git branch <分支名>
git checkout <分支名> 
```

#### 创建并且同时切换到新分支

```bash
git chechout -b <分支名>
```

#### 合并分支

此时指针指向的是master，<分支名>所表示的是要合并的节点，因此合并后产生的新节点依然是master

```bash
git merge <分支名>
```

使用**git rebase**把当前分支里的工作直接移到目标（此处以master为例）分支上，移动以后会使得两个分支的功能看起来像是顺序开发的

```bash
git rebase master
```



### 在提交树上移动

#### 分离HEAD

HEAD 是一个对当前检出记录的符号引用 —— 也就是指向你正在其基础上进行工作的提交记录。

HEAD 总是指向当前分支上最近一次提交记录。大多数修改提交树的 Git 命令都是从改变 HEAD 的指向开始的。如果想看 HEAD 指向，可以通过 `cat .git/HEAD` 查看， 如果 HEAD 指向的是一个引用，还可以用 `git symbolic-ref HEAD` 查看它的指向。

可以使用**git checkout** 来改变HEAD的指向

#### 相对引用

用法：

* 使用^向上移动一个提交记录（如git checkout master^，表示HEAD指向master的父节点)
* 使用~<num>向上移动多个提交记录

使用相对引用最多的就是移动分支。可以直接使用 `-f` 选项让分支指向另一个提交。例如:

```bash
git branch -f master HEAD~3
```

上面的命令会将 master 分支强制指向 HEAD 的第 3 级父提交。

#### 撤销变更

主要有两种方法用来撤销变更 —— 一是 `git reset`，还有就是 `git revert`

`git reset` 通过把分支记录回退几个提交记录来实现撤销改动。你可以将这想象成“改写历史”。`git reset` 向上移动分支，原来指向的提交记录就跟从来没有提交过一样。

在你的本地分支中使用 `git reset` 很方便，但是这种方法对大家一起使用的远程分支是无效的。为了更改远端，我们需要使用 `git revert`



### 整理提交记录

如果你想将一些提交复制到当前所在的位置（`HEAD`）下面的话， Cherry-pick 是最直接的方式了

```bash
git cherry-pick <提交号>...
```

当你知道你所需要的提交记录（**并且**还知道这些提交记录的哈希值）时, 可以使用 cherry-pick ,但是如果你不清楚你想要的提交记录的哈希值呢? 可以利用交互式的 rebase 

交互式 rebase 指的是使用带参数 `--interactive` 的 rebase 命令, 简写为 `-i`

如果你在命令后增加了这个选项, Git 会打开一个 UI 界面并列出将要被复制到目标分支的备选提交记录，它还会显示每个提交记录的哈希值和提交说明，提交说明有助于理解这个提交进行了哪些更改。

当 rebase UI界面打开时, 能做3件事:

- 调整提交记录的顺序（通过鼠标拖放来完成）
- 删除不想要的提交（通过切换 `pick` 的状态来完成，关闭就意味着你不想要这个提交记录）
- 合并提交