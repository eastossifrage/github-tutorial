<!--
author: 东方鹗
date: 2016-06-02
title: 第一章 安装并初始设置 Git
tags: git, github, 你应该会玩github
category: git
status: publish
summary: Git 是由 Linux 的创建者 Linus 开发的，对 Linux 系统的支持是最好的，但是，很长一段时间， Git 只能在 Linux 和 unix 系统上运行。不过，只要你相信 Git 身上的“开源”精神，你会看到奇迹的。现在，Git 已经可以在 Linux、Unix、Mac和Windows这几大平台上正常运行了。
-->


> Git 是由 Linux 的创建者 Linus 开发的，对 Linux 系统的支持是最好的，但是，很长一段时间， Git 只能在 Linux 和 unix 系统上运行。不过，只要你相信 Git 身上的“开源”精神，你会看到奇迹的。现在，Git 已经可以在 Linux、Unix、Mac和Windows这几大平台上正常运行了。

## 安装 Git

### 在 Linux 系统上安装 Git

首先，你可以试着输入 git，看看系统有没有安装 git:

```bash
$ git --version
git version *.*.*
```

如果能出现上面的提示，`git version *.*.*`具体示例为`git version 2.7.4`。说明你的 Linux 系统已经安装了 git。

如果 Linux 系统用英文友好的提示你 Git 没有安装，那你就得从头开始安装了。当然， Linux 系统一般会提示你如何安装的。
如果没有提示，那么你可以用度娘，或者参照如下步骤。

#### 在 Ubuntu16.04 上安装 Git

妈妈再也不用担心我的学习了，～～～ so easy ～～～
```bash
$ sudo apt-get install git
```
安装完成了。

#### 在 Centos6.5 上安装 Git

更简单了，你什么都不要做，Centos6 上自动集成了 Git。

### 在 Mac 上安装 Git

好像也已经自动集成了 Git。本人没有 Mac 本子，深表遗憾，无法亲身证实。

### 在 Windows 上安装 Git

你如果是一个资深的、有开源精神的编程人员，我知道，我还是少在你面前提 Windows，但是，还是容许我这样没有段位的老运维人员吐槽一下 Windows 吧，
@##￥#￥#%@￥@#%@#￥@#......。其实不管怎么说，Windows还是有很多人在使用，这里推荐最简单的方法。下载 msysgit，默认安装即可。 msysgit 是 Windows 版的 Git，从[https://git-for-windows.github.io](https://git-for-windows.github.io)下载。

## 初始化设置 Git

以 ubuntu16.04 系统为例。

### 设置姓名和邮箱地址

```bash
$ git config --global user.name "username"
$ git config --global user.email "email@example.com"
```

这个命令会在“ ./gitconfig ”中以如下形式输出设置文件。

```bash
[user]
    name = username
    email = email@example.com
```

想要更改这些信息，可以直接编辑这个设置文件。但是为了安全期间，还是建议从一开始就认真设置，不要随便返工。

### 提高命令输出的可读性

将 color.ui 设置为 auto 可以让命令的输出拥有更高的可读性。

```bash
$ git config --global color.ui auto
```

" ./gitconfig " 中会增加下面一行。

```bash
[color]
    ui = auto
```
这样以来，各种命令的输出就会变得更容易分辨。

## 小结

本章中，讲解了如何安装 Git，并进行初始化设置。
如果你是一名开发者，今后使用 Git 的情况会必然越来越多。请务必认真进行初始化设置。

