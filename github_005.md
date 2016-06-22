
<!--
author: 东方鹗
date: 2016-06-22
title: 第五章 尝试 Pull Request
tags: git, github, 你应该会玩github
category: git
status: publish
summary: 按部就班地创建 GitHub 账号并公开自己的源代码并不是什么难事，不过，刚刚接触 GitHub 的人往往不会或不敢使用 Pull Request 功能。Pull Request 是社会化编程的象征。 GitHub 创造的这一功能，可以说给开源开发世界带来了一场革命。不会用这个功能，就等于不会用 GitHub 。
-->

> 按部就班地创建 GitHub 账号并公开自己的源代码并不是什么难事，不过，刚刚接触 GitHub 的人往往不会或不敢使用 Pull Request 功能。
Pull Request 是社会化编程的象征。 GitHub 创造的这一功能，可以说给开源开发世界带来了一场革命。不会用这个功能，就等于不会用 GitHub 。

##  Pull Request 的概要

### 什么是 Pull Request

首先我们来理解什么是 Pull Request 。Pull Request 是自己修改源代码后，请求对方仓库采纳该修改时采取的一种行为。

### Pull Request 的流程

现在假设我们在使用 GitHub 上的一款开源软件。在软件的使用过程中，我们偶然间发现了 BUG。为了继续使用软件，我们手动修复了这个 BUG。如果我们修改的这段代码能被软件的开发仓库采纳，今后与我们同样使用这款软件的人就不会再遇到这个 BUG 。为此，我们要第一时间发送 Pull Request。

在 GitHub 上发送 Pull Request 后，接受方的仓库会创建一个附带源代码的 Issue ，我们在这个 Issue 中记录详细内容。 这就是 Pull Request。

发送过去的 Pull Request 是否被采纳，要由接受方仓库的管理者进行判断。一般只要代码没有问题，对方都会采纳。如果有问题，我们会收到评论。

只要 Pull Request 被顺利采纳，我们就会成为这个项目的 Contributor （贡献者），我们编写的这段代码也将被全世界的人使用。这正是社会化编程和开源开发的一大乐趣。

## 发送 Pull Request 前的准备

Pull Request 图，如下图所示：
![001.png-34.9kB][1]

### 查看要修正的源代码

请登录[https://ituring.github.io/first-pr/](https://ituring.github.io/first-pr/)网站。该网站的源代码已经在 GitHub 上公开。大家可以将自己的感谢写入源代码，然后发送 Pull Request。

这个网站通过 GitHub 的 GitHub Pages 的功能发布。 GitHub Pages 的网站的源代码位于仓库的 gh-pages 分支。访问仓库页面，我们就可以看到源代码。

记述感想时需要修改 index.html 文件。各位不妨先查看它的源代码，对内容有个印象。

### Fork

大家需要先访问仓库页面，点击 Fork 按钮创建自己的仓库。新建的仓库名为“自己的账户名/first-pr”。我们的例子里命名为hirocastest

### clone

clone 仓库所需的访问信息显示在右侧的中央部分，让我们将它复制下来，把这个仓库 clone 到当前的开发环境中。

```bash
$ git clone git@github.com:eastossifrage/first-pr.git
正克隆到 'first-pr'...
remote: Counting objects: 1560, done.
remote: Compressing objects: 100% (67/67), done.
remote: Total 1560 (delta 36), reused 0 (delta 0), pack-reused 1493
接收对象中: 100% (1560/1560), 389.83 KiB | 325.00 KiB/s, 完成.
处理 delta 中: 100% (1007/1007), 完成.
检查连接... 完成。
$ cd first-pr
```

first-pr 目录下会生成 Git 仓库。这个仓库与我们 GitHub 账户下的 first-pr 仓库状态相同。现在只要在这个仓库中修改源代码进行 push ， GitHub 账户中的仓库就会被修改。

### branch

- 为何要在特性分支中进行作业

当前 Git 的主流开发模式都会使用特性分支。大家要养成创建特性分支后再修改代码的号习惯。在 GitHub 上发送 Pull Request 时，一般都是发送特性分支。这样一来， Pull Request 就拥有了更明确的特性（主题）。让对方了解自己修改代码的意图，有助于提高代码审查的效率。

- 确认分支

``` bash
$ git branch -a
* gh-pages  当前分支
  remotes/origin/HEAD -> origin/gh-pages
  remotes/origin/feature/move-jquery-from-cdn-to-local
  remotes/origin/gh-pages
```

开头加了“remotes/origin/”的是 GitHub 端仓库的分支。我们手头的开发环境只有 gh-pages 分支。

网站中显示的 HTML 位于 /origin/gh-pages 分支。虽然通常情况下最新版代码都位于 master 分支，但由于本次我们使用了 GitHub Pages，所以最新代码位于 gh-pages 分支。

- 创建特性分支
w
我们创建一个名为 work 的分支，用来发送 Pull Request。这个 work 分支就是这次的特性分支。现在创建 work 分支并自动切换。

```bash
$ git checkout -b work gh-pages
切换到一个新分支 'work'
$ git branch -a
  gh-pages
* work   当前分支
  remotes/origin/HEAD -> origin/gh-pages
  remotes/origin/feature/move-jquery-from-cdn-to-local
  remotes/origin/gh-pages
```

查看文件列表，我们可以看到网站中显示的 index.html 文件。

```bash
$ ls
images  index.html  javascripts  params.json  README.md  stylesheets
```

可以用浏览器打开并确认显示。

### 添加代码

用编辑器打开 index.html 文件，以 HTML 形式添加感想。

```bash
...
<p class="impression">画蛇添足以下</p>
...
```

请自由添加感想并用p标签（ Tag ）括起，然后关闭编辑器。

### 提交修改

用git diff 命令查看修改是否已经正确进行。

```bash
$ git diff
diff --git a/index.html b/index.html
index c73e3ae..86c7f5d 100644
--- a/index.html
+++ b/index.html
@@ -88,6 +88,7 @@
 <p class="impression">试一试Pull Request.</p>
 <p class="impression">试一下</p>
 <p class="impression">This is Patrick.</p>
+<p class="impression">画蛇添足以下</p>
 <p class="impression">nice book!~ 2016.5.2 (<a href="https://github.com/SecondJ">@SecondJ</a>)</p>
 <p class="impression">凡事都要动手做一下(2016/05/03)</p>
 <p class="impression">It's my first Pull Request.Thank you for your guide.</p>
```

然后用浏览器打开，查看显示是否正确。然后确认添加的代码，提交至本地仓库。

```bash
$ git add index.html
$ git commit -m "添加我的感想"
[work 11d69c2] 添加我的感想
 1 file changed, 1 insertion(+)
```

### 创建远程分支

要从 GitHub 发送 Pull Request ， GitHub 端的仓库总必须有一个包含了修改后代码的分支。我们现在就来创建本地 work 分支的相应远程分支。

```bash
$ git push origin work
对象计数中: 3, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (3/3), 完成.
写入对象中: 100% (3/3), 336 bytes | 0 bytes/s, 完成.
Total 3 (delta 2), reused 0 (delta 0)
To git@github.com:eastossifrage/first-pr.git
 * [new branch]      work -> work
```

查看分支， /origin/work 已被创建。

```bash
$ git branch -a
  gh-pages
* work
  remotes/origin/HEAD -> origin/gh-pages
  remotes/origin/feature/move-jquery-from-cdn-to-local
  remotes/origin/gh-pages
  remotes/origin/work
```

请打开 GitHub 的"用户名/first-pr"页，确认 work分支是否被创建，已经是否包含我们添加的代码。

## 发送 Pull Request

![002.png-41.3kB][2]

参考上图左侧，切换到 work 分支。点击右侧的 Compare 链接，会跳转至查看分支间差别的页面，如下图所示：

![003.png-84.1kB][3]

查看刚刚进行的更改是否正确。这里显示的的像就是我们本次 Pull Request 中包含的提交。确认想要发送的 Pull Reqeust 的内容差别无误后，请点击 Create pull request 按钮。随后显示的表单用于填写请求对方采纳的评论。如下图所示：

![004.png-45kB][4]

简明扼要地描述本次进行提交的理由。确认没有问题后，点击 Create pull request 按钮。这样一来，Pull Request 的目标仓库中就会新建 Pull Request 和 Issue ，同时该仓库的管理者会接到通知。同时，你应该可以看到类似的界面：

![005.png-88.6kB][5]


-----------------------------------------------------

至此，恭喜各位顺利发送了第一次的 Pull Request 。现在我们发送的源代码还没有被采纳，对方仓库不会有任何变化，所以网页页仍然是原样。现在就等待着管理者采纳你的代码了。

## 让 Pull Request 更加有效的方法

如果有效地运用 Pull Request，这是一门艺术，需要我们唠唠。

### 在开发过程中发送 Pull Request 进行讨论

在软件的设计与实现过程中如果发起讨论，Pull Request 是个非常好的契机。我们虽然可以像上面的例子一样等代码完成后再发送 Pull Request，但再实际开发过程中，这样做很可能导致一个功能再完成后才受到设计或实现方面的指正，从而使代码需要大幅更改或重新实现。

在 GitHub 上，我们可以尽早创建 Pull Request，从审查中获得反馈，让大家在设计与实现方面思路一致，借此逐渐提高代码质量。这个方法在团队开发大型项目时尤其有效，已将 GitHub 运用到实际开发中的团队请务必一试。

这个方法执行起来很简单。只要在想发起讨论时发送 Pull Request 即可，不必等代码最终完成。即便某个功能尚在开发之中，只要在 Pull Request 中附带一段简单代码让大家有个大体印象，就能获得不少反馈。在 Pull Request中尽量加入直观易懂的 Tasklist 语法。

这一方法要求尽早发送 Pull Request，越早效果越明显。另外还有一件事要记住，就是千万不要在 Pull Request 中添加无关的修改。处理与主题无关的作业请另外创建分支，不然会让原本清晰的讨论变得一团糟。

### 明确标出“正在开发过程中”

为防止开发到一般的 Pull Request 被误合并，一般都会在标题前加上“[WIP]”字样。WIP 是 Wokr In Progress 的简写，表示仍在开发过程中。等所有功能都实现之后，再取消这个前缀。

### 不进行 Fork 直接从分支发送 Pull Request

一般说来，在 GitHub 上修改对方的代码时，需要先将仓库 Fork 到本地，然后再进行修改代码，发送 Pull Request。但是，如果用户对该仓库有编辑权限，则可以直接创建分支，从分支发送 Pull Request。利用这一设计，团队开发时不妨为每一位成员赋予编辑权限，免去 Fork 仓库的麻烦。这样，成员在有需要时就可以创建自己的分支，然后直接想master分支等发送 Pull Request。

## 仓库的维护

Fork 或 clone 来的仓库，一旦防止不管就会离最新的源代码越来越远。如果不以最新的源代码为基础进行开发，劳神费力地编写代码也很可能白费力气。最好的办法就时让仓库保持最新状态。

通常来说 clone 来的仓库实际上与原仓库并没有任何关系。所以我们需要将原仓库设置为远程仓库，从该仓库获取（ fetch ）数据与本地仓库进行合并（ merge ），让本地仓库的源代码保持最新状态。如图所示：

![006.png-35.9kB][6]

### 仓库的 Fork 与 clone

将 octocat/Spoon-Knife 作为原仓库，在 GitHub 上进行 Fork ，然后 clone 。

```bash
$ git clone git@github.com:eastossifrage/Spoon-Knife.git
正克隆到 'Spoon-Knife'...
remote: Counting objects: 16, done.
remote: Total 16 (delta 0), reused 0 (delta 0), pack-reused 16
接收对象中: 100% (16/16), 完成.
处理 delta 中: 100% (2/2), 完成.
检查连接... 完成。
$ cd Spoon-Knife
```

### 给原仓库设置名称

我们给原仓库设置 upstream 的名称，将其作为远程仓库。

```bash
$ git remote add upstream git://github.com/octocat/Spoon-Knife.git
```

今后，我们的这个仓库将以 upstream 作为原仓库的标示符。这个环境只需要设定一次。

### 获取最新数据

下面我们从远程仓库获取（ fetch ）最新源代码，与自己仓库的分支进行合并。要让仓库维持最新状态，只需要重复这一工作即可。

```bash
$ git fetch upstream
来自 git://github.com/octocat/Spoon-Knife
 * [新分支]          change-the-title -> upstream/change-the-title
 * [新分支]          master     -> upstream/master
 * [新分支]          test-branch -> upstream/test-branch
$ git merge upstream/master
Already up-to-date.
```

我们通过 git fetch 命令获取最新的数据，然后用 git merge 将 upstream/master 分支与当前分支（ master ）合并。虽然本次示例没有可以合并的内容。但这一操作确实可以将最新的源代码合并至当前分支。

这样一来，当前分支（ master ）就获得了最新的源代码。各位在创建特性分支，编辑源代码之前，建议先将仓库更新到这一状态。一般情况下 master 分支都会获取最新代码，很少需要 Fork 的开发者亲自进行修正。

## 小结

本章我们简单学习了 Pull Request 的发送方法。想必大家已经发现，发送 Pull Request 时不单要敲一敲代码，还需要进行很多其它工作。

在实际开发中， Pull Request 多少都会与传统习惯或规范有些冲突。但是，诸多团队的实践表明 Pull Request 确实有其显著的效果。作为一名投身于开源开发的程序员，应当早适应这一设计。














  [1]: http://www.os373.cn/blog/img/GitHub_05/001.png
  [2]: http://www.os373.cn/blog/img/GitHub_05/002.png
  [3]: http://www.os373.cn/blog/img/GitHub_05/003.png
  [4]: http://www.os373.cn/blog/img/GitHub_05/004.png
  [5]: http://www.os373.cn/blog/img/GitHub_05/005.png
  [6]: http://www.os373.cn/blog/img/GitHub_05/006.png
