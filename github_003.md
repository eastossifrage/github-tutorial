<!--
author: 东方鹗
date: 2016-06-08
title: 第三章 Git 功能详述
tags: git, github, 你应该会玩github
category: git
status: publish
summary: 前面已经说过，Github 是为开发者提供 Git 仓库的托管服务。那么在学好 GitHub 之前，肯定先得掌握 Git ，这一章就是为详述 Git 的功能而做的，你需要耐心学习和实践，最好在 [http://learngitbranching.js.org/](http://learngitbranching.js.org/) 网站中进行一些实际操作，这样对你掌握 Git 更有帮助。
-->

> 前面已经说过，Github 是为开发者提供 Git 仓库的托管服务。那么在学好 GitHub 之前，肯定先得掌握 Git ，这一章就是为详述 Git 的功能而做的，你需要耐心学习和实践，最好在 [http://learngitbranching.js.org/](http://learngitbranching.js.org/) 网站中进行一些实际操作，这样对你掌握 Git 更有帮助。

## 基本操作

### git init —— 初始化仓库

要使用 Git 进行版本管理，必须先初始化仓库。（这个要求很多时候是唬人的，这是老派做法）。 Git 是使用 git init 命令进行初始化的。

```bash 
$ mkdir ousikongjiantest
$ cd ousikongjiantest
$ git init
初始化空的 Git 仓库于 /home/eastossifrage/ousikongjiantest/.git/
```

如果初始化成功，执行了 git init 命令的目录下就会生成 .git 目录。这个 .git 目录里存储着当前目录内容所需的仓库数据。

这个目录其实就时“该仓库的工作树”。

### git status —— 查看那仓库的状态

git status 命令嗯用于显示 Git 仓库的状态。这时一个十分常用的命令，请务必牢记。

工作树和仓库在被操作的过程中，状态会不断发生变化。在 Git 操作过程中常用 git status 命令产看当前状态，可谓基本中的基本。

```bash
$ git status
位于分支 master

初始提交

无文件要提交（创建/拷贝文件并使用 "git add" 建立跟踪）
```

结果显示了我们当前正处于 master 分支下（现在还不必深究分支的内容，以后再说）。接着还显示了没有可提交的内容。所谓提交（ commit ），是指“记录工作树中所有文件的当前状态”。

尚没有可提交的内容，就是说当前我们建立的这个仓库中还没有记录任何文件的任何状态。这我们先建立 README.md 文件作为管理对象，为第一次提交做前期准备。

```bash
$ touch README.md
$ git status
位于分支 master

初始提交

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

	README.md

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）

```

可以看到在 未跟踪的文件（ Untracked files ）中显示 README.md 文件。类似地，只要对 Git 的工作树或仓库进行了操作， git status 命令的显示结果就会发生变化。

### git add —— 向暂存区中添加文件

如果只是用 Git 仓库的工作树创建了文件，那么该文件并不会被记入 Git 仓库的版本管理对象当中。因此我们用 git status 命令查看 README.md 文件时，它会显示在未跟踪的文件（ Untracked files ）里。

要想让文件成为 Git 仓库的管理对象，就需要用 git add 命令将其加入暂存区（ Stage 或者 Index ）中。暂存区是提交之前的一个临时区域。

```bash
$ git add README.md 
$ git status
位于分支 master

初始提交

要提交的变更：
  （使用 "git rm --cached <文件>..." 以取消暂存）

	新文件：   README.md
```

将 README.md 文件加入暂存区后，git status 命令的显示结果发生了变化。可以看到， README.md 文件显示在 要提交的变更（ Changes to be committed ）中了。

### git commit —— 保存仓库的历史记录

git commit 命令可以将暂存区中的文件世纪保存到仓库的历史记录中。通过这些记录，我们可以在工作树中复原文件。

- 记述以行提交信息

我们来实际运行一下 git commit 命令。

```bash
$ git commit -m "First commit"
[master （根提交） f8d9fbf] First commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```

-m 参数后的 “First commit” 称作提交信息，是对这个提交的概述。

- 记述详细提交信息

刚才我们只简洁的记述了一行提交信息，如果想要记述得更加详细，请不要加 -m，直接执行 git commit 命令。执行后编辑器 nano 就会启动，并显示如下结果。

```bash
$ touch A.md
$ git add A.md
$ git commit
  GNU nano 2.5.3 文件： ...sifrage/ousikongjiantest/.git/COMMIT_EDITMSG         


# 请为您的变更输入提交说明。以 '#' 开始的行将被忽略，而一个空的提交
# 说明将会终止提交。
# 位于分支 master
# 要提交的变更：
#       新文件：   A.md
#
```

在编辑器中记述提交信息的格式如下。

- 第一行：用以行文字描述提交的更改内容
- 第二行：空行
- 第三行以后：记述更改的原因和详细内容

只要按照上庙的格式输入，今后便可以通过确认日志的命令或工具看到这些记录。

在以 # （井号）标为注释的 要提交的变更（ Changes to be committed ）栏中，可以查看本次提交中包含的文件。将提交信息按格式记述完毕后，请保存并关闭编辑器，以 # （ 井号 ）标为注释的行不必删除。随后，刚才记述的提交信息就会被提交。

- 中止提交

如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编辑器，随后提交就会被中止。

- 查看提交后的状态

执行完 git commit 命令后在来查看当前状态。

```bash
$ git status
位于分支 master
无文件要提交，干净的工作区
```

当前工作树处于刚刚完成提交的最新状态，所以结果显示没有更改。

### git log —— 查看提交日志

git log 命令可以查看以往仓库中提交的日志。包括可以查看什么人在什么时候进行了提交或合并，以及操作前后有怎样的差别。关于合并我们会在后面解释。
先来看看刚才的git commit 命令是否被记录了。

```bash
$ git log
commit 9f89adfddc81fdd8b31c85150006f0ed68dd5340
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:29:43 2016 +0800

    测试文件，用于测试 git 的提交信息内容。
    
    测试文件，仅此而已。

commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:14:55 2016 +0800

    First commit
```

因为提交了两次，所以显示两个提交操作。commit 栏旁边显示的“f8d9fbf4ae......”是指向这个提交的哈希值。 Git 的其它命令中，在指向提交时会用到这个哈希值。

Author栏中显示我们给 Git 设置的用户名和邮箱地址。 Date 栏中显示提交执行的日期和时间。再往下就是该提交的提交信息。

### 只显示提交信息的第一行

如果只想让程序显示第一行简述信息，可以在git log命令后加上 --pretty=short。这样伊朗开发人员就能够更轻松地把握多个提交。

```bash
$ git log --pretty=short
commit 9f89adfddc81fdd8b31c85150006f0ed68dd5340
Author: eastossifrage <eastossifrage@gmail.com>

    测试文件，用于测试 git 的提交信息内容。

commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>

    First commit

```

### 只显示指定目录、文件的日志

只要在 git log 命令后加上目录名，便会只显示该目录下的日志。如果加的是文件名，就会只显示与该文件相关的日志。

```bash
$ git log README.md
commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:14:55 2016 +0800

    First commit

```

### 显示文件的改动

如果想查看提交所带来的改动，可以加上 -p 参数，文件的前后差别就会显示在提交信息之后

```bash
$ git log -p
commit 9f89adfddc81fdd8b31c85150006f0ed68dd5340
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:29:43 2016 +0800

    测试文件，用于测试 git 的提交信息内容。
    
    测试文件，仅此而已。

diff --git a/A.md b/A.md
new file mode 100644
index 0000000..e69de29

commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:14:55 2016 +0800

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

```

比如，执行下面的命令，就可以查看 README.md 文件提交日志以及提交前后的差别。
```bash
$ git log -p README.md
commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:14:55 2016 +0800

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

```
如上所述，git log 命令可以利用多种参数帮助开发者把握以往提交的内容。不必勉强自己一次记下全部参数，每当有想查看的日志就积极去查，慢慢就能得心应手了。

### git diff —— 查看更改前后的差别

git diff 命令可以查看工作树、暂存区、最新提交之间的差别。我们在刚刚提交的 README.md 中写点东西。

```bash
# GitHub 教程
```
用Markdown语法书写。

### 查看工作树和暂存区的差别

执行 git diff 命令，查看当前工作树与暂存区的差别。

```bash
 git diff
diff --git a/README.md b/README.md
index e69de29..6a297ed 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# GitHub 教程

```

由于我们尚未用 git add 命令向暂存区添加任何东西，所以程序只会显示工作树与最新提交状态之间的差别。
“+”号标出的是新添加的行，被删除的行则用“-”号标出。这里只添加了一行。

用 git add 命令将 README.md 文家加入暂存区。

```bash
$ git add README.md
```

### 查看工作树和最新提交的差别

如果现在执行 git diff 命令，由于工作树和暂存区的状态并无差别，结果什么都不会显示。要查看与最新提交的差别，请执行以下命令。

```bash
$ git diff HEAD
diff --git a/README.md b/README.md
index e69de29..6a297ed 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# GitHub 教程
```

不妨养成这样一个号习惯：在执行 git commit 命令之前先执行 git diff HEAD 命令，查看卜辞提交与赏赐提交之间有什么差别，等确认完毕后再进行提交。这里的 HEAD 是指向当前分支中最新一次提交的指针。

由于我们刚刚确认过两个提交之间的差别，所以直接运行 git commit 命令。
```bash
$ git commit -m "Add index"
[master a4184b4] Add index
 1 file changed, 1 insertion(+)

```

保险起见，我们查看一下提交日志，确认提交是否成功。

```bash
commit a4184b4709e1eaf6fea6623241c570e4df2cd6cf
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 18:29:35 2016 +0800

    Add index

commit 9f89adfddc81fdd8b31c85150006f0ed68dd5340
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:29:43 2016 +0800

    测试文件，用于测试 git 的提交信息内容。
    
    测试文件，仅此而已。

commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Mon Jun 6 17:14:55 2016 +0800

    First commit

```
成功查到了“ Add index ”提交。

## 分支的操作

在进行多个并行作业时，我们会用到分支。在这类并行开发的过程中，往往同时存在多个最新代码状态。如下图所示，从 master 分支创建 feature-A 分支和 fix-B 分支后，每个分支中都拥有自己的最后代码。 master分支是 Git 默认创建的分支，因此基本上所有开发都是以这个分支为中心进行的。

![001.png-10.6kB][1]

不同分支中，可以同时进行完全不同的作业。等该分支的作业完成之后再也 master 分支合并。比如 feature-A 分支的作业结束后与 master 合并，如下图所示：

![002.png-13.6kB][2]

通过灵活运用分支，可以让多人同时高效地进行并行开发。

### git branch —— 显示分支一览表

git branch 命令可以将分支名列表显示，同时可以确认当前所在分支。让我们来世纪运行 git branch 命令。

```bash
$ git brach
* master
```

可以看到 master 分支左侧标有 “*”（星号），表示这是我们当前所在的分支。也就是说，我们正在 master 分之下进行开发。结果中没有显示其它分知名，表示本地仓库中只存在一个分支。

### git checkout -b —— 创建、切换分支

如果想以当前的 master 分支为基础创建新的分支，我们需要用到 git checkout -b 命令。

- 切换到 feature-A 分支进行提交

执行下面的命令，创建名为 feature-A 的分支。

```bash
$ git checkout -b feature-A
切换到一个新分支 'feature-A'
```

实际上，连续执行下面两条命令也能收到同样效果。

```bash
$ git branch feature-A
$ git checkout feature-A
```

创建 feature-A 分支，并将当前分支切换到 feature-A 分支。这时在来查看分支列表，会显示我们处于分支 feature-A 下。

```bash
$ git branch
* feature-A
  master
```

feature-A 分支左侧标有“*”，表示当前分支为 feature-A。在这个状态下像正常开发那样修改代码、执行 git add 命令并进行提交的花，代码就会提交至 feature-A分支。像这样不断对一个分支（例如 feature-A）进行提交的操作，我们称为“培育分支”。
下面来实际操作一下。在 README.md 文件中添加一行。

```bash
# GitHub 教程

- feature-A
```

然后进行提交。

```bash
$ git add README.md
$ git commit -m "Add feature-A"
[feature-A d33a19e] Add feature-A
 1 file changed, 2 insertions(+)
```
于是，这一行就添加到feature-A分支中了。

- 切换到 master 分支

现在我们再来看看 master 分支有没有受到影响。首先切换至 master 分支。

```bash
$ git checkout master 
切换到分支 'master'
```

然后查看 README.md 文件，会发现 README.md 文件仍然保持原先的状态，并没有被添加文字。 feature-A分支的更改不会影响到 master 分支，这正是在开发中创建分支的优点。只要创建多个分支，不互相影响的情况下同时进行多个功能的开发。

- 切换会上一个分支

现在，我们再切换会 feature-A 分支。

```bash
$ git checkout -
切换到分支 'feature-A'
```
像上面这样用“-”（连字符）代替分知名，就可以切换至上一个分支。当然，将“-”替换成 feature-A 同样可以切换成 feature-A 分支。

### 特性分支

特性分支顾名思义，是集中实现单一特性（主题），除此之外不进行任何作业的分支。在日常开发中，往往会创建数个特性分支，同时在此之外保留一个随时可以发布软件的稳定分支。稳定分支的角色通常由 master 分支担当。如下图所示：

![003.png-11.4kB][3]

之前，我们创建了 feature-A 分支，这一分支主要实现 feature-A, 除了 feature-A 的实现之外不能进行任何作业。即便在开发过程中发现了 BUG ，也需要再创建新的分支，在新的分支中进行修改。

基于特定主题的作业在特性分支中进行，主题完成后再与 master 分支合并。只要保持这样一个开发流程，就能保证 master 分支可以随时供人查看。这样以来，其他开发者也可以放心大胆地从 master 分支创建新的特性分支了。

### 主干分支

通常我们会用 master 分支作为主干分支。主干分支中并没有开发到一半的代码，可以随时供他人查看。
有时我们需要让这个主干分支总是配置在正式环境中，有时又需要用标签 Tag 等创建版本信息，同时管理多个版本发布。拥有多个版本发布时，主干分支也有多个。

### git merge —— 合并分支

接下来，我们假设 feature-A 已经实现完毕，想要将它合并到主干分支 master 中。首先切换到 master 分支。

```bash
$ git checkout master
切换到分支 'master'
```

然后合并 feature-A 分支。为了在历史记录种明确记录下本次分支合并，我们需要创建合并提交。 因此，在合并时加上 --no-ff 参数。

```bash
$ git merge --no-ff feature-A
```

随后编辑器会启动，用于录入合并提交的信息。

```bash
GNU nano 2.5.3 文件： ...astossifrage/ousikongjiantest/.git/MERGE_MSG 

Merge branch 'feature-A'

# 请输入一个提交信息以解释此合并的必要性，尤其是将一个更新后的上游分支
# 合并到主题分支。
#
# 以 '#' 开头的行将被忽略，而且空提交说明将会终止提交。
```

默认信息中已经包含了时从 feature-A 分支合并过来的相关内容，所以可不必做任何更改。将编辑器中显示的内容保存，关闭编辑器，然后就会看到下面的结果。

```bash
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
```

这样以来， feature-A 分支的内容就合并到 master 分支中了。


## 更改提交的操作

### git reset —— 回溯历史版本

Git的另一个特征便是可以灵活操作历史版本。借助分散仓库的优势，可以在不影响其它仓库的前提下对历史版本进行操作。

在这里，为了让大家熟悉对历史版本的操作，先回溯历史版本，创建一个名为 fix-B 的特性分支，如下图：

![004.png-15kB][4]

- 回溯到创建 feature-A 分支前

让我们先回溯到上一节分支创建之前，创建一个名为 fix-B 的特性分支。
要让仓库的HEAD、暂存区、当前工作树回溯到指定状态，需要到 git reset --hard命令。只要提供目标时间的哈希值（利用git log --graph 命令），就可以恢复至该时间点的状态。

```bash
$ git reset --hard a4184b4709e1eaf6fea6623241c570e4df2cd6cf
HEAD 现在位于 a4184b4 Add index
```

我们已经成功回溯到特性分支（ feature-A ）创建之前的状态。由于所有文件都回溯到了制定哈希值对应的时间点上， README.md 文件的内容也恢复到了当时的状态。

- 创建 fix-B 分支

使用下面的命令创建特性分支（ fix-B ）。

```bash
$ git checkout -b fix-B
切换到一个新分支 'fix-B'
```

作为这个主题的作业内容，我们在 README.md 文件中添加一行文字。

```bash
# GitHub 教程

    - fix-B
```

然后直接提交 README.md 文件。

```bash
$ git add README.md 
$ git commit -m "Fix B"
[fix-B 2722c9a] Fix B
 1 file changed, 2 insertions(+)
```

现在的状态如下图所示：

![005.png-7.3kB][5]


接下来我们的目标是下图所示的状态，即主干分支合并 feature-A 分支的修改后，又合并了 fix-B 分支的修改。

![006.png-18.1kB][6]

- 推进至 feature-A 分支合并后的状态

首先恢复到 feature-A 分支合并后的状态。不妨称这一操作为“推进历史”。

git log命令只能查看以当前状态为终点的历史日志。所以这里要使用 git reflog 命令，查看当前仓库的操作日志。在日志中找出回溯历史之前的哈希值，通过 git reset --hard 命令恢复到回溯历史的状态。

首先执行 git reflog 命令，查看当前仓库执行过的操作的日志。

```bash
$ git reflog
2722c9a HEAD@{0}: commit: Fix B
a4184b4 HEAD@{1}: checkout: moving from master to fix-B
a4184b4 HEAD@{2}: reset: moving to a4184b4709e1eaf6fea6623241c570e4df2cd6cf
8fbff6b HEAD@{3}: checkout: moving from feature-A to master
d33a19e HEAD@{4}: checkout: moving from master to feature-A
8fbff6b HEAD@{5}: merge feature-A: Merge made by the 'recursive' strategy.
a4184b4 HEAD@{6}: checkout: moving from feature-A to master
d33a19e HEAD@{7}: checkout: moving from master to feature-A
a4184b4 HEAD@{8}: checkout: moving from feature-A to master
d33a19e HEAD@{9}: commit: Add feature-A
a4184b4 HEAD@{10}: checkout: moving from master to feature-A
a4184b4 HEAD@{11}: commit: Add index
9f89adf HEAD@{12}: commit: 测试文件，用于测试 git 的提交信息内容。
f8d9fbf HEAD@{13}: commit (initial): First commit
```

在日志中，我们可以看到 commit、 checkout、 reset、merge 等 Git 命令的执行记录。只要不进行 Git 的 GC （ Garbage Collection ，垃圾回收），就可以通过日志随意调取近期的历史状态，就像给时间机器指定一个时间点，在过去未来中自由穿梭一般。即便开发者错误执行了 Git 操作，基本也都可以利用 git reflog 命令恢复到原先的状态，所以请各位读者务必牢记部分。

从上面的记录中找到 feature-A 特性分支合并后的状态，对应的哈希值为 8fbff6b 。我们将 HEAD、暂存区、工作树恢复到这个时间点的状态。

```bash
$ git checkout master
切换到分支 'master'
$ git reset --hard 8fbff6b
HEAD 现在位于 8fbff6b Merge branch 'feature-A'
```

之前我们使用 git reset --hard 命令回溯了历史，这次又再次通过它恢复到了回溯前的历史状态。

当前状态如下图所示：

![007.png-15.8kB][7]

### 消除冲突

现在只要合并 fix-B 分支，就可以得到我们想要的状态。

```bash
$ git merge --no-ff fix-B
自动合并 README.md
冲突（内容）：合并冲突于 README.md
自动合并失败，修正冲突然后提交修正的结果。
```

根据信息提示，README.md 文件发生了冲突（ Conflict ）。系统在合并 README.md 文件时， feature-A 分支更改的部分与本次想要合并的 fix-B 分支更改部分发生了冲突。

不解决冲突就无法完成合并，所以我们打开 README.md 文件，解决这个冲突。

- 查看冲突部分并将其解决

打开 README.md 文件，就会发现其内容变成了下面的样子。

```bash
# GitHub 教程

<<<<<<< HEAD
- feature-A
=======
    - fix-B
>>>>>>> fix-B
```

======= 以上的部分是当前 HEAD 的内容，以下的部分是要合并 fix-B 分支的内容。将其修改为想要的样子。

```bash
# GitHub 教程

    - feature-A
    - fix-B
```

如上所示，本次修改让 feature-A 与 fix-B 的内容并存于文件之中。但是在实际的软件开发中，往往需要删除其中之一，所以各位在处理冲突时，务必要仔细分析冲突部分的内容后再行修改。

- 提交解决后的结果

冲突解决后，执行 git add 命令与 git commit 命令。

```bash
$ git add README.md 
$ git commit -m "Fix conflict"
[master 51d3753] Fix conflict
```

由于本次更改解决了冲突，所以提交信息记为 “ Fix conflict ”。

### git commit --amend —— 修改提交信息

要修改上一条提交信息，可以使用 git commit --amend 命令。
我们将上一条提交信息记为 “ Fix conflict ”，但它其实时 fix-B 分支的合并，解决合并时发生的冲突只是过程之一，这样标记时在不妥。于是，我们要修改这条提交信息。

```bash
$ git commit --amend
```

执行上面的命令后，编辑器就会启动。

```bash
 GNU nano 2.5.3 文件： ...sifrage/ousikongjiantest/.git/COMMIT_EDITMSG         

Fix conflict

# 请为您的变更输入提交说明。以 '#' 开始的行将被忽略，而一个空的提交
# 说明将会终止提交。
#
# 日期：  Wed Jun 8 15:52:04 2016 +0800
#
# 位于分支 master
# 要提交的变更：
#       修改：     README.md
#
```

将提交信息的部分修改为 Merge branch 'fix-B'，然后保存文件，关闭编辑器。

```bash
[master 7eb6e6b] Merge branch 'fix-B'
 Date: Wed Jun 8 15:52:04 2016 +0800
```

随后会显示上面这条结果。现在执行 git log --graph 命令，可以看到提交日志中的相应内容也已经修改。

```bash
$ git log --graph
*   commit 7eb6e6bc60f7b3172bcc7a50a0afe41c4225ba85
|\  Merge: 8fbff6b 2722c9a
| | Author: eastossifrage <eastossifrage@gmail.com>
| | Date:   Wed Jun 8 15:52:04 2016 +0800
| | 
| |     Merge branch 'fix-B'
| |   
| * commit 2722c9a28990491041390b589e5d3c82402cf1f1
| | Author: eastossifrage <eastossifrage@gmail.com>
| | Date:   Tue Jun 7 19:04:03 2016 +0800
| | 
| |     Fix B
| |     
* |   commit 8fbff6b5552672579a7f3e768901b129d8950f22
|\ \  Merge: a4184b4 d33a19e
| |/  Author: eastossifrage <eastossifrage@gmail.com>
|/|   Date:   Tue Jun 7 18:35:36 2016 +0800
| |   
| |       Merge branch 'feature-A'
| |   
| * commit d33a19ef349a04927708db4948b5f6f997a86ab1
|/  Author: eastossifrage <eastossifrage@gmail.com>
|   Date:   Tue Jun 7 16:23:22 2016 +0800
|   
|       Add feature-A
|  
* commit a4184b4709e1eaf6fea6623241c570e4df2cd6cf
| Author: eastossifrage <eastossifrage@gmail.com>
| Date:   Mon Jun 6 18:29:35 2016 +0800
| 
|     Add index
|  
* commit 9f89adfddc81fdd8b31c85150006f0ed68dd5340
| Author: eastossifrage <eastossifrage@gmail.com>
| Date:   Mon Jun 6 17:29:43 2016 +0800
| 
|     测试文件，用于测试 git 的提交信息内容。
|     
|     测试文件，仅此而已。
|  
* commit f8d9fbf4ae042ff34bed953dc1cb44161263f87e
  Author: eastossifrage <eastossifrage@gmail.com>
  Date:   Mon Jun 6 17:14:55 2016 +0800
  
      First commit
(END)
```

### git rebase -i —— 压缩历史

在合并特性分支之前，如果发现已提交的内容中有些许拼写错误等，不妨提交一个修改，然后将这个修改包含到前一个提交中，压缩成一个历史记录。这是个会经常用到的技巧，让我们来实际操作体会以下。

- 创建 feature-C 分支

首先，新建一个 feature-C 特性分支。

```bash
$ git checkout -b feature-C
切换到一个新分支 'feature-C'
```

作为 feature-C的功能实现，我们在 README.md 文件中添加一行文字，并且故意留下拼写错误，以便之后修改。

```bash
# GitHub 教程

    - feature-A
    - fix-B
    - faeture-C
```

提交这部分内容。这个小小的变更就没有必要先执行 git add 命令再执行 git commit 命令了，我们用 git commit -am 命令来一次完成这两步操作。

```bash
$ git commit -am "Add feature-C"
[feature-C 0e55046] Add feature-C
 1 file changed, 1 insertion(+)
```

- 修正拼写错误

现在来修正刚才预留下的拼写错误。自行修正README.md文件的内容，修正后的差别如下所示。

```bash
$ git diff
diff --git a/README.md b/README.md
index 805f350..e28c3fc 100644
--- a/README.md
+++ b/README.md
@@ -2,4 +2,4 @@
 
     - feature-A
     - fix-B
-    - faeture-C
+    - feature-C
```

然后进行提交。

```bash
$ git commit -am "Fix typo"
[feature-C 25c9c84] Fix typo
 1 file changed, 1 insertion(+), 1 deletion(-)
```

错字漏字等失误称作typo，所以我们将提交信息记为 “ Fix typo ”。 实际上，我们不希望再历史记录中看到这类提交，因为健全的历史记录并不需要它们。如果能再最初提交之前发现并修改这些错误，也就不会出现这类提交了。

- 更改历史

因此，我们来更改历史。将“ Fix typo ”修正的内容与之前一次的提交合并，再历史记录种合并为一次完美的提交。为此，我们要用到 git rebase 命令。

```bash
$ git rebase -i HEAD~2
```
上述命令可以选定当前分支中包含HEAD（ 最新提交 ）在内的两个最新历史记录为对象。

```bash
  GNU nano 2.5.3 文件： ...ngjiantest/.git/rebase-merge/git-rebase-todo         

pick 0e55046 Add feature-C
pick 25c9c84 Fix typo

# Rebase 7eb6e6b..25c9c84 onto 7eb6e6b (2 command(s))
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

我们将 25c9c84 的 Fix typo 的历史记录压缩到 0e55046 的 Add feature-C里。按照下图所示， 将 25c9c84 左侧的 pick 部分删除，改写为 fixup。

```bash
pick 0e55046 Add feature-C
fixup 25c9c84 Fix typo
```

保存内容。

``` bash
[分离头指针 67eedca] Add feature-C
 Date: Wed Jun 8 16:27:51 2016 +0800
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/feature-C.
```

系统显示 rebase 成功。也就是一下面这两个提交作为对象，将 “ Fix typo” 的内容合并到了上一个提交“ Add feature-C ”中，改写成了一个新的提交。

- 0e55046 Add feature-C
- 25c9c84 Fix typo

现在再查看提交日志时会发现 Add feature-C 的哈希值已经不是 0e55046 了，这证明提交已经被更改。

```bash
$ git log --graph
* commit 67eedca8c8cc1ec8856b87e807b63070f8420cc4
| Author: eastossifrage <eastossifrage@gmail.com>
| Date:   Wed Jun 8 16:27:51 2016 +0800
| 
|     Add feature-C
|    
*   commit 7eb6e6bc60f7b3172bcc7a50a0afe41c4225ba85
|\  Merge: 8fbff6b 2722c9a
| | Author: eastossifrage <eastossifrage@gmail.com>
| | Date:   Wed Jun 8 15:52:04 2016 +0800
| | 
| |     Merge branch 'fix-B'
| |   
| * commit 2722c9a28990491041390b589e5d3c82402cf1f1
| | Author: eastossifrage <eastossifrage@gmail.com>
| | Date:   Tue Jun 7 19:04:03 2016 +0800
| | 
| |     Fix B
...
```

这样一来，Fix typo 就从历史中被抹去，也就相当于 Add feature-C 中从来没有出现过拼写错误。这算是一种良性的历史改写。

- 合并至 master 分支

feature-C 分支的使命告一段落，我们将它与 master 分支合并。

```bash
$ git checkout master
切换到分支 'master'
eastossifrage@eastossifrage:~/ousikongjiantest$ git merge --no-ff feature-C
Merge made by the 'recursive' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

master 分支整合了 feature-C 分支。

## 推送值远程仓库

Git 时分散型版本管理系统，但我们前面所学习的，都是针对单一本地仓库的操作。现在，我们开始接触元再网络另一头的远程仓库。远程仓库顾名思义，时与我们本地仓库相对对立的另一个仓库。让我们先再 GitHub 上创建一个仓库（ousikongjiantest），并将其设置为本地仓库的远程仓库。创建的时候不要勾选 Initialize this repository with a README 选项，主要是为了防止 GitHub 创建仓库时自动生成README文件，从创建之初便与本地仓库失去了整合性。

### git remote add —— 添加远程仓库

再 GitHub 上创建的仓库路径为 “ git@github.com:用户名/ousikongjiantest.git ”。现在我们用 git remote add 命令将它设置成本地仓库的远程仓库。

```bash
$ git remote add origin git@github.com:eastossifrage/ousikongjiantest.git
```

按照上述个时执行 git remote add 命令之后，Git 会自动将 git@github.com:eastossifrage/ousikongjiantest.git 远程仓库的名称设置为 origin (标示符）。

### git push —— 推送至远程仓库

- 推送至 master 分支

如果想将当前分支下本地仓库中的内容推送给远程仓库，需要用到 git push 命令。现在假定我们再 master 分之下进行操作。

```bash
$ git push -u origin master
对象计数中: 22, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (16/16), 完成.
写入对象中: 100% (22/22), 1.95 KiB | 0 bytes/s, 完成.
Total 22 (delta 3), reused 0 (delta 0)
To git@github.com:eastossifrage/ousikongjiantest.git
 * [new branch]      master -> master
分支 master 设置为跟踪来自 origin 的远程分支 master。
```

像这样执行 git push 命令，当前分支的内容就会被推送给远程仓库 origin 的 master 分支。 -u 参数可以在推送的同时，将 origin 仓库的 master 分支设置为本地仓库当前分支的 upstream （上游）。添加这个参数，将来运行 git pull 命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从 origin 的 master 分支获取内容， 省去了另外添加参数的麻烦。

执行该操作后，当前本地仓库 master 分支的内容将会被推送到 GitHub 的远程仓库中。在 GitHub 上也可以确认远程 master 分支的内容和本地 master 分支相同。

- 推送至 master 以外的分支

除了 master 分支之外，远程仓库也可以创建其它分支。现在，我们在本地仓库中创建 feature-D 分支，并将它以同名形式 push 至远程仓库。

```bash
$ git checkout -b feature-D
切换到一个新分支 'feature-D'
```

现在将它 push 给远程仓库并保持分支名称不变。

```bash
$ git push -u origin feature-D
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:eastossifrage/ousikongjiantest.git
 * [new branch]      feature-D -> feature-D
分支 feature-D 设置为跟踪来自 origin 的远程分支 feature-D。
```

现在，再远程仓库的 GitHub 页面就可以看到 feature-D 分支了。

## 从远程仓库获取

### git clone —— 获取远程仓库

- 获取远程仓库

首先 我们还到其它目录下，将 GitHub 上的仓库 clone 到本地。
注意不要与之前操作的仓库再同一目录下。

```bash
$ cd ~
$ mkdir test
$ $ git clone git@github.com:eastossifrage/ousikongjiantest.git
正克隆到 'ousikongjiantest'...
remote: Counting objects: 22, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 22 (delta 3), reused 22 (delta 3), pack-reused 0
接收对象中: 100% (22/22), 完成.
处理 delta 中: 100% (3/3), 完成.
检查连接... 完成。
```

执行 git clone 命令后我们会默认处于 master 分支下，同时系统会自动将origin设置成该远程仓库的标示符。也就是说，当前本地仓库的master 分支与 GitHub 端远程仓库（ origin ）的 master 分支在内容上时完全相同的。

```bash
$ cd ousikongjiantest/
$ git brach -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-D
  remotes/origin/master
```

我们用git branch -a 命令查看当前分支的相关信息。添加 -a 参数可以同时显示本地仓库和远程仓库的分支信息。
结果中显示了 remotes/origin/feature-D，证明我们的远程仓库中已经有了 feature-D 分支。

- 获取远程的 feature-D 分支

我们试着将 feature-D 分支获取至本地仓库。

```bash
$ git checkout -b feature-D origin/feature-D
分支 feature-D 设置为跟踪来自 origin 的远程分支 feature-D。
切换到一个新分支 'feature-D'
```

-b 参数的后面时本地仓库中新建分支的名称。为了便于理解，我们仍将其命名为 feature-D, 让它与远程仓库的对应分支保持同名。新建分支名称后面是获取来源的分支名称。例子中指定的 origin/feature-D，就是说以名为 origin 的仓库（这里至 GitHub端的仓库）的 feature-D 分支为来源，在本地仓库中创建 feature-D 分支。

- 向本地的 feature-D 分支提交更改

现在假定我们是另一名开发者，要做一个新的提交。 在README.md 文件中添加一行文字，查看更改。

```bash
$ git diff
diff --git a/README.md b/README.md
index e28c3fc..f0d9a76 100644
--- a/README.md
+++ b/README.md
@@ -3,3 +3,4 @@
     - feature-A
     - fix-B
     - feature-C
+    - feature-D
```

按照之前学过的方式提交即可。

```bash
$ git commit -am "Add feature-D"
[feature-D 445aeca] Add feature-D
 1 file changed, 1 insertion(+)
```

- 推送 feature-D 分支

```bash
$ git push
对象计数中: 3, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (3/3), 完成.
写入对象中: 100% (3/3), 311 bytes | 0 bytes/s, 完成.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:eastossifrage/ousikongjiantest.git
   21b3215..445aeca  feature-D -> feature-D
```

从远程仓库获取 feature-D 分支，再本地仓库中提交更改，再将 feature-D 分支推送回远程仓库，通过这一系列操作，就可以与其他开发者相互合作，共同培育 feature-D分支，以实现某些功能。

### git pull —— 获取最新的远程仓库分支

现在我们方向刚刚操作的目录，回到原来的那个目录下。这边的本地仓库中只创建了 feature-D 分支，并没有在 feature-D 分支中进行任何提交。然而远程仓库的的 feature-D 分支中已经有了我们刚刚推送的提交。这时我们就可以使用 git pull 命令，将本地的 feature-D 分支更新到最新状态。当前分支为 feature-D 分支。

```bash
$ git pull origin feature-D
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
展开对象中: 100% (3/3), 完成.
来自 github.com:eastossifrage/ousikongjiantest
 * branch            feature-D  -> FETCH_HEAD
   21b3215..445aeca  feature-D  -> origin/feature-D
更新 21b3215..445aeca
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

GitHub 端远程仓库中的 feature-D 分支是最新状态，所以本地仓库中的 feature-D 分支就得到了更新。今后只要需要像平常一样在本地进行提交在 push 给远程仓库，就可以与其他开发者同时在同一个分支中进行作业，不断给 feature-D 增加新功能。
如果两个人同时修改同一部分的源代码，push 时就很容易发生冲突。所以多名开发者在同一分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作。





  [1]: http://static.zybuluo.com/ossifrage/q6kiyio2x9s2hvstos80wuc4/001.png
  [2]: http://static.zybuluo.com/ossifrage/pvpuwbfauizy02x5ripvrpht/002.png
  [3]: http://static.zybuluo.com/ossifrage/v1s33dwppcm6eyccbg7qhzbt/003.png
  [4]: http://static.zybuluo.com/ossifrage/yqlzphgfrspytrkvciwea55f/004.png
  [5]: http://static.zybuluo.com/ossifrage/au51lojijgip2tyndhx7la1z/005.png
  [6]: http://static.zybuluo.com/ossifrage/btmdfjd0nusk2iupdzxjjxvb/006.png
  [7]: http://static.zybuluo.com/ossifrage/1ljjko9b4523ebvnbjbsk40r/007.png
